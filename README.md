# design-library-case-study

# Finding twenty times more screens in a sprawling design library

During an internal hackweek at a previous employer, I built a small tool to make a very large Figma design library searchable. It had grown to around a hundred separate files, and finding a specific screen meant knowing which file it lived in, then scrolling. The usual answer was to ask whoever had touched that file most recently.

What I wanted was an index: type a few words, get a link that opens the exact frame in Figma.

## The flat scan that nearly ended it

Figma has a public REST API that returns a file's contents as a tree of nodes. My first version asked each file for its pages, walked each page's children, and wrote every frame it saw to a JSON index.

It found 118 frames across the entire library.

That was obviously wrong — I could open one file by hand and count more frames than that on a single page. I spent most of a day assuming I had hit a rate limit or missed a pagination parameter, because the requests were succeeding and the data looked well-formed.

## The insight: the tree is deeper than it looks

The frames were not direct children of the pages. They sat inside section nodes — and sections can contain further sections, nested as deep as whoever built the file wanted. That is how people organize a file once it gets big.

My scan only read one level down from each page. Every section it met, it treated as a leaf and moved past, skipping everything inside. The 118 frames were the handful somebody had left loose at the top level.

The fix was to stop iterating and start recursing: visit a node, and if it has children, descend, collecting frames at any depth rather than only the first.

Same API, same files, same access. The recursive traversal found 2,310+ frames — roughly twenty times as many.

## The second problem, visible only once I could see everything

Many of the newly discovered frames had names useless for searching: generic defaults like `Frame 412`, or a component's own name repeated dozens of times in one file. Finding them was now possible; finding the *right* one still wasn't.

The recursive walk already knew the path it had taken to reach each frame, so it also knew the frame's enclosing group — and those groups were usually named descriptively, because a person had named them deliberately. When a frame's own name was generic, I labeled it with its nearest meaningfully named ancestor instead. That turned thousands of interchangeable names into text a search box could work with.

## What happened to it

Nothing. It was a hackweek build. I demoed it, nobody picked it up, and it never became part of anyone's workflow — not adopted, never shipped. I also can't publish the code or the index: it was built on company time, and the index is effectively a map of a private design library. That's why this is a write-up rather than a repository.

## What I took from it

**A number that looks wrong usually is wrong.** The API was never the constraint. I spent a day debugging my requests when the bug was in my assumption about the response's shape.

**Reach for recursion when the data is a tree.** It usually is — design files, file systems, nested documents. A flat pass over a tree doesn't fail loudly; it quietly returns a plausible-looking fraction and lets you believe it.

**Discovery and labeling are separate problems.** Finding everything is what made the naming problem visible, and naming was the difference between a list and a usable tool.

The traversal is the transferable part. It isn't specific to any one library — it follows from the API and from how people organize files in it. That's the piece I'd write again.
