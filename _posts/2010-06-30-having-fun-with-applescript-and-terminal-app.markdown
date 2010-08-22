---
layout: post
title: Having fun with Applescript and Terminal.app
---

Last week-end I decided that I wanted to go back to learning a little bit of ruby for a couple of days. PHP can become pretty boring at times (PHP 5.3 changes that a bit, closures are cool), and besides I love learning new programming languages. Anyway, back to the subject, I usually use a *dark* theme for Terminal.app, sometimes I make it a bit transparent to increase luminosity. However, when using *irb*, I like to use a brighter theme (i.e.: white background). The crappy solution would be to use the mouse to open a new window with a different theme, I don't want to do that. Instead, I have been researching a way to achieve my goal without touching the mouse, or leaving the terminal for that matter. There are a couple of solutions that involve AppleScript. But before we get into it, let me make a small observation on AppleScript:

I do not know how to use AppleScript very well at all but my understanding of it is that it basically simulates mouse gestures or keyboard shortcuts/sequences. In other words, in it's most basic form, AppleScript lets you access menubar items without touching the mouse.

### Open a new Terminal.app window using AppleScript

First let's do it with the mouse. Let's open a new window with the *Basic* theme. To do so, you need to select the following menubar item:

> Shell &#x25B8; New Window &#x25B8; Basic

The following AppleScript script will do the same thing:

{% highlight applescript %}
tell application "Terminal" to activate

tell application "System Events"
	tell process "Terminal"
		tell menu item "Basic" of menu "New Window" of menu item "New Window" of menu "Shell" of menu bar item "Shell" of menu bar 1
			click
		end tell
	end tell
end tell
{% endhighlight %}
gist: [458179](http://gist.github.com/458179)
{: .label}

Nice and easy. But what if you want to open several windows with each different color themes without touching the mouse? **The solution:** Window Groups

### Open a Window Group using AppleScript

**The first thing to do is to create a new window group**.

1. Close the terminal windows that you don't want and open new ones with a different color theme, position them, resize them, enjoy yourself until you are fully satisfied.
2. Once you're done, you need to save the current *state* of Terminal.app as a window group.    
	
	* To do so, click the **Window &#x25B8; Save Windows as Group&hellip;** menu bar item and give a name to your new window group.      
	*For the sake of this example, I will call the window group <strong>Basic</strong>.*

To open the newly created window group, you need to click on the following menubar item:

> Window &#x25B8; Open Windows Group &#x25B8; Basic

Here is the AppleScript version of that mouse gesture:

{% highlight applescript %}
tell application "Terminal" to activate

tell application "System Events"
	tell process "Terminal"
		tell menu item "Basic" of menu "Open Window Group" of menu item "Open Window Group" of menu "Window" of menu bar item "Window" of menu bar 1
			click
		end tell
	end tell
end tell
{% endhighlight %}
gist: [458195](http://gist.github.com/458195)
{: .label}

Now here is the most important question that remains unanswered:

> How can I use those scripts from within Terminal.app?

### Using AppleScript from the command-line

Here are the steps to follow to use AppleScript scripts as shell scripts from the command-line. *Note that those step are to be repeated for each script.*

First create a new file and **on the first line** copy the following code (called the **shebang**):

{% highlight sh %}
#!/usr/bin/osascript
{% endhighlight %}

After that line (2nd line, 3rd line, 42nd line, it doesn't matter as long as it is after the **shebang**), copy **one** AppleScript script and save the file somewhere in your path (i.e.: `~/bin`); give it a simple name with no extension and make it executable. *For the sake of this example I am going to call the file <strong>basic</strong>*

{% highlight console %}
chmod a+x basic
{% endhighlight %}

You can now use your script from the command-line by typing its name:

{% highlight console %}
basic
{% endhighlight %}

That's it!

### Other ways to use AppleScript scripts from the command-line

If the **shebang** method doesn't work, then you are probably doing something wrong; **check that the *shebang* is the first line in the script, that means no whitespace before!** However, if you do not like that method, there are several other ways to do it that I will describe *very* briefly:

* Compile and save the individual scripts as *scripts* using the *AppleScript Editor* and run them from the command-line using the `osascript` command.
* Create aliases to open the AppleScript scripts you want.
* If you are using zsh you can use a suffix alias.

### Customize the AppleScript scripts

As you can see, the AppleScript syntax is pretty straightforward and easy to customize. However, there is an important detail you need to pay attention to: for each menu item you want to "select" you need to "duplicate" its name. A little example will probably make this statement a bit more clear. Let's modify the first script so that it opens a new *Homebrew* tab; replace that line:

{% highlight applescript %}
tell menu item "Basic" of menu "New Window" of menu item "New Window" of menu "Shell" of menu bar item "Shell" of menu bar 1
{% endhighlight %}

&hellip;with that line:

{% highlight applescript %}
tell menu item "Homebrew" of menu "New Tab" of menu item "New Tab" of menu "Shell" of menu bar item "Shell" of menu bar 1
{% endhighlight %}

So you see, the names `"New Tab"` and `"Shell"` are repeated twice. Here is the full script:

{% highlight applescript %}
tell application "Terminal" to activate

tell application "System Events"
	tell process "Terminal"
		tell menu item "Homebrew" of menu "New Tab" of menu item "New Tab" of menu "Shell" of menu bar item "Shell" of menu bar 1
			click
		end tell
	end tell
end tell
{% endhighlight %}
gist: [458239](http://gist.github.com/458239)
{: .label}

To use this script on the command-line, just follow the instructions above&#x261D;

### Let me give credit where credit is due

**frogor** and **Tomis** from the **#macosx** channel on the **Freenode** network (irc.freenode.net) helped me a lot. In fact, they did all the work, the explaining, the coding, everything.