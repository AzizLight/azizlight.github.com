---
layout: post
title: Switching to Vim
---

You know how sometimes people get religious about the text editor they use? Especially Vim and Emacs users. Well I was one of those user, except that I was a Textmate fanatic; until three weeks ago.

Let's rewind about four months. Vim was getting a lot of attention, mainly because of [Nettuts' new tutorial series about Vim][2] and [Steve Losh's blog post][1]. I had also read [Yehuda Katz' blog post](http://yehudakatz.com/2010/07/29/everyone-who-tried-to-convince-me-to-use-vim-was-wrong/) in July 2010, which really
motivated me to try learning how to use Vim.

During the next two days, I spent my time learning the basics and configuring my new editor. That second part (the configuration) was really annoying because I didn't want to learn how to configure the editor (at least not right away), I wanted to learn how to use it. While I could have adapted myself to the editor more, I really missed the snippets and commands that were shipped with Textmate, and the numerous ones that I created myself or found on the InterWebs. I lasted two days, and then I came back to Textmate.

Not long after that, the "CodeIgniter Community Implosion" happened. I won't talk about it in this post, or ever, but I will say that it's the straw that broke the camel's back. I wanted to learn Ruby for a long time, I had started, then stopped, numerous times, but then I grew tired of PHP.

I resumed my Ruby education in mid-December, in Textmate, and I enjoyed every single bit of it. But then I realized that I wasn't using Textmate the way I used to when I wrote PHP code. Textmate became replaceable.

Then I came across this [blog post by Henrik Nyh][3], which contained a revelation in it: Janus, a distribution of Vim plugins and config files that could completely abstract the whole setup process that put me off during my first try in September. Janus was a game changer. And since I remembered the basics a bit, the learning process was greatly simplified.

From this point on, I reviewed the basics quickly and started actually using Vim instead of learning how to use it. If I didn't know how to do something, I would google it (on [DuckDuckGo](http://duckduckgo.com)!) or ask a question on the Vim IRC channel on the Freenode server. At the time, I was following the [Ruby on Rails Tutorial][4] Screencasts in parallel with the online book, and I tried to follow the videos without pausing to force me to using the editor as efficiently and as fast as possible. It helped **A LOT**! And by *"as efficiently and as fast as possible"*, I meant no arrow keys, no mouse, hands on the home row of the keyboard. Since I can't touch type, this was and still is a big challenge for me but I am getting better at it. I also watched [Derek Wyatt's tutorial videos][5], which contained a lot of good tips (approximatively one every two seconds).

As of today, Vim is my main text editor, and I will probably become religious about it too, the same I was with Textmate before, and Jedit a very long time ago.

The nice thing about this is that it opens the door to a lot of other cool stuff like [Vmail](http://danielchoi.com/software/vmail.html) and [Vimperator](http://vimperator.org/vimperator). All of a sudden I started using Vim's shortcuts all over the place, and love it!

So If you are a Textmate user, and you want to move on, I strongly believe that the MacVim + Janus combination is really the best option.

One advice that I can give after this little adventure of mine, is to
use Vim the way you use any other editor and gradually stop using the
mouse and the arrow keys. When you can't figure out how to do something,
head to DuckDuckGo or StackOverflow, or ask a question on IRC. Finally,
and this helped me a lot, create a new file in Vim, and log the result
of every research you made when you were stuck. This will force you to
write something relevant in Vim, and you will end up with a personal
cheat sheet.

To end this blog post, I will post a list of resources about Vim that helped me or will help me to get better Also, I intentionally will not list MacVim because I really believe it is much easier to install it using Homebrew as described in Henrik's blog post.

**Links**:

- [Janus](https://github.com/carlhuda/janus)
- [The ultimate Vim configuration](http://amix.dk/vim/vimrc.html)
- [Vim Tips Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki)
- [Gary Bernhardt's vimrc](https://github.com/garybernhardt/dotfiles/blob/master/.vimrc)
- [Ryan Bate's vimrc](https://github.com/ryanb/dotfiles/blob/master/vimrc)
- [Vim Scripts](http://www.vim.org/scripts/index.php)
- [My Vim config files](https://gist.github.com/810962)

**Blog posts**:

- [Venturing into Vim][2]
- [Coming Home to Vim][1]
- [TextMate to Vim with training wheels][3]
- [A Starting Guide to VIM from Textmate](http://blog.danielfischer.com/2010/11/19/a-starting-guide-to-vim-from-textmate/)
- [VimCasts](http://vimcasts.org/)
- [Vim Recipes](http://vim.runpaint.org/)
- [Vim Golf](http://vimgolf.com/)

**Twitter**:

- [Vim Links](http://twitter.com/#!/VimLinks)
- [Vim Tips](http://twitter.com/#!/vimtips)
- [Vim for my grandma](http://twitter.com/#!/vcotwdorso)

[2]: http://net.tutsplus.com/tutorials/other/venturing-into-vim-new-premium-video-series/ "Venturing into Vim"
[1]: http://stevelosh.com/blog/2010/09/coming-home-to-vim "Coming Home to Vim"
[3]: http://henrik.nyh.se/2011/01/textmate-to-vim-with-training-wheels "TextMate to Vim with training wheels"
[4]: http://railstutorial.org/ "Ruby on Rails tutorial"
[5]: http://www.derekwyatt.org/vim/vim-tutorial-videos/ "Vim Tutorial Videos by Derek Wyatt"
