# Finding one screen in a large design library

I am a multidisciplinary designer, not an engineer: five years as a digital production designer, graphic design before that, and a lot of content management work. I know enough HTML and CSS to follow a front-end conversation, and I can talk to developers and designers both, and tell either one exactly what I need. I built this with Cursor, an AI coding tool, as much to learn whether AI-assisted coding was something I could use day to day as to solve the problem in front of me.

## The problem

During an internal hackweek at a previous employer, a Figma design library had grown to around a hundred separate files. People needed one specific screen out of it, fairly often. Getting it meant already knowing which file it lived in, or asking whoever had worked on that file last. Neither of those is a way to find something.

## Why a web page and not a chatbot

A colleague had already done the hard, unglamorous part. They had gathered the underlying data, a record of what was in the library and where each screen sat, and they were building a chatbot on top of it that you would ask questions.

Looking at the same data, I thought the interface was the wrong shape for the problem. Finding a screen is a visual task. You usually do not know the words for what you want, you know it when you see it, and most of the time you are choosing between several near identical options. A conversation asks you to describe the thing before you are allowed to look at anything. A page can just show you.

So I made that case, took the same data as my foundation, and built the other version.

## What I built

A single search box. You type a few words, suggestions appear as you type, and one click opens that exact screen in Figma. No knowing which file to open first, no scrolling through a file hoping to recognise something.

The predictive part was deliberate. People almost always arrive with some idea of what they are after, even if they cannot name it exactly, so offering matches from the first few characters saves them finishing the thought. It also quietly teaches you what is in the library, because you see near misses on the way to what you wanted.

Most of my time went on how it behaved rather than whether it worked. Which matches come first. How much context a result needs to show, because a screen name on its own is often not enough to tell two similar screens apart. What the page says when nothing matches, so a dead end still tells you something. How to get from a result to the screen itself in one click instead of three. A light version and a dark one.

None of that is technical. It is the same judgement I use on any piece of production work, applied to a tool instead of a layout.

## What happened to it

Nothing. It was a hackweek build. I demoed it, nobody picked it up, and it never became part of anyone's workflow. I also can't share what was built or the library data behind it: it was made on company time, and that data describes a private design library. So this is a write-up, not a download.

## What I took from it

**A working prototype argues better than a document.** I could have written up why a page beats a conversation for this. Instead people could type a word and watch the right screen open. It did not win in the end, but it was the only version of the argument anyone could actually try, and that is a better position to argue from than a page of reasoning.

**The shape of the interface mattered more than what was behind it.** The data was identical in both versions. The entire difference was whether you had to describe what you wanted or could simply look at it. That decision was not a technical one and it was the most valuable thing I contributed.

**An AI tool builds what you describe, not what you know.** Cursor did whatever I asked, quickly, and never once told me a decision was weak. Because getting it running stopped being the hard part, nearly all of my effort went into wording, ordering, context and the number of clicks. Knowing what good looks like and being able to describe it precisely turned out to be the whole job, and that is the part I was already trained for.
