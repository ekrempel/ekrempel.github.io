---
layout: post
title: Changing function names in LaTeX
---

I'm in the middle of writing my diploma thesis in computer science. I use Latex for my thesis and I like it most of the time. At home I have a PC with Ubuntu, at work I have a Win7 PC. I like booth systems and I think both have their advantages. Of course the 2 different OS bring some additional challenges. The first was the different encoding of the *.tex files. Ubuntu uses UTF-8 and Windows some weird stuff I can't remember the name. So whenever I make an new file at work it gets encoded Windows stile and all the Linux files are encoded in UTF-8. Luckily booth my editors can handle separate encodings for every file in the Latex project. I recommend  [TeXnicCenter](http://www.texniccenter.org/) for Windows and [Kile](https://kile.sourceforge.io/) for Ubuntu.

Today a new challenge occurred. I use algorithm2e for some pseudo code inside my work. Everything worked fine at first. But then I edited the style of my code blocks and the bad thing happened. I use **\IncMargin{1em}** to increase the space on the left side of the code. At home I use a slightly older version of the algorithme2 package than at work. The problem is, the developers changed the name of their control sequence. In versions prior to 4.01 it was called **\incmargin{}** and in the newer version it is **\IncMargin{}**. This results in a nasty error message when compiling at home:


**! Undefined control sequence.**
**l.179 \IncMargin**
**{1em}**

Unfortunately the new version isn't in the Ubuntu repository. This won't change until the Ubuntu people make the switch from Texlive 2009 to 2010, which can easily take another year. Updating the Tex system without the package management isn't a good idea.  So I looked for a solution without changing a hole lot in my setup. The solution was simple:

1. Go to the [algorithm2e](https://www.ctan.org/tex-archive/macros/latex/contrib/algorithm2e/) website.
2. Download the algorithm2e.sty.
3. Store it inside your latex project folder.

When compiling the Tex system is looking inside the active folder for *.sty files before it tries to find them in the system. So you can override the used *.sty for a single project without changing your system. This might be a dirty hack, but I'm short on time. But there is one thing we all should learn from this:

**"Don't change your functions names unless you absolutely have to!"**