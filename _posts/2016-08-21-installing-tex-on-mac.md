---
layout:     post
title:      Installing (La)TeX on Mac, the Sane Way
date:       2016-08-21
summary:    MacTeX is a fat, fat cow, and BasicTeX, by contrast, is starved.  Here's how to get LaTeX up and running with automatic dependency installation on MacOS.
categories: TeX LaTeX installation MacOS
---
<center><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/LaTeX_logo.svg/200px-LaTeX_logo.svg.png"></center>

If you're here, you probably know what \\(\LaTeX\\) is.  But just in case you're not quite sure, LaTeX is the industry and academy standard for typesetting technical documents.  It's used in the first sentence in this paragraph to display the logo, and it is probably what was used to write any research paper that you have run across containing a formula.  (If you're still using Microsoft Word to do formulas, please stop.)

That being said, LaTeX (and its parent, TeX) is a relic of times past.  At the time of this article, there are [5,178 packages](https://www.ctan.org/) available for download depending on the functionality you want.

<hr>
## LaTeX installation on MacOS is outdated
If you're on Windows, you can simply use [MiKTeX](http://miktex.org/), and any dependencies will be automatically downloaded as you need them.  How nice! On MacOS, however, your options are to either accept bloat or tedious, tedious pain.  You can:

* Install [MacTeX](https://tug.org/mactex/mactex-download.html) which will include every package, and work.  As impressive as that is, that's roughly 3-4 gigabytes split among over 100k files on your disk.

I'm currently trying to compile my [resume](http://www.github.com/ryan-holben/resume), and I'd rather not let my TeX installation sequester 3% of my SSD to produce a single PDF.  So that leaves us with...

* [BasicTeX](https://tug.org/mactex/morepackages.html), which is about 100 megabytes and contains so few packages that you'll be manually installing every package as needed, one at a time.

I've tried this.  You will be appalled by how many packages your little document requires.  Don't do this.

It turns out there's a package we can install that'll take care of dependencies for us.  Why isn't this a built-in feature, or at least well-publicized?  Who knows.

## Installation steps

These steps start with the minimal BasicTeX installation as well as several GUI applications, and then automatically adds packages as you need them.  All work is done in the terminal, unless noted otherwise.


### Command line tools

1. Get [Homebrew](http://brew.sh/) if you don't have it already.

    `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

1. Get [Cask](https://caskroom.github.io/) for Homebrew.  This lets Homebrew install MacOS apps.

    `brew tap caskroom/cask`

1. Get [BasicTeX](http://macappstore.org/basictex/).

    `brew cask install basictex`

    You now have a LaTeX installation!  But let's make things a little more user-friendly and modern.

1. Update the TeX Live Package Manager `tlmgr`.  (Note: Anything using `tlmgr` will probably require sudo.)

    `sudo tlmgr update --self`

1. Get [texliveonfly](https://www.ctan.org/pkg/texliveonfly).  This is the utility that automatically grabs packages for us.

    `sudo tlmgr install texliveonfly`

### GUI applications

1. Now we'll leave the command line for a bit.  First, get the [TeX Live Utility](http://amaxwell.github.io/tlutility/) for a GUI package manager.

1. Open TeX Live Utility, and update all packages: ⇧⌘U

    If the Utility asks you if you'd like to update automatically, you'll probably want to say yes.  It may not ask you until the second launch.

1. For a dedicated *TeX editor, I use [TeX Shop](http://pages.uoregon.edu/koch/texshop/obtaining.html).  There are other options out there as well.  __If you're new to LaTeX, consider using [LyX](https://www.lyx.org/).__  It's a WYSIWYG LaTeX editor, which lets you code as little or as much as you like as you learn the ropes.

### Compiling your document

1. The first time you try to compile a document, your installation will probably have to download some packages.  For me, I ran the following command in the folder containing `Resume.tex`:

    `sudo texliveonfly -c xelatex Resume.tex`

    The `-c xelatex` was required because my document was a XeLaTeX document.  Most documents won't need this.

1. Uh oh, although the utility fetched a bunch of relevant packages, it still didn't work!  Isn't this fun?  If this happens to you, carefully look at your error output.  Mine complained about missing fonts.  However, a google search of the first missing font's name led me to the `lm-math` package.  A quick call to `sudo tlmgr install lm-math`, and everything worked beautifully.

1. Now that I've gotten all my packages, I can do all my editing and compiling in TeX Shop, without the command line!

1. In the future, I may occasionally need to go back to the command line to run `sudo texliveonfly somedoc.tex` to grab new packages.
