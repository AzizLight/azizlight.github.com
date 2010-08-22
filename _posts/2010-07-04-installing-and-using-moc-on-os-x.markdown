---
layout: post
title: Installing and using moc on OS X
---

Before I became an Apple fan-boy and after I had enough of Windows, I used GNU/Linux distributions for about three years (Ubuntu mostly, but I tried a lot of other distros too). It's during that period that I became obsessed by command-line applications. At the time, I tried ALL the command-line music players, but only two of them stood out: moc and herrie.

herrie is pretty good, but it was missing one **very** important feature that moc has: it can't run in the background. That's right, moc is more than a music player, it's a music server. What that means is that once moc runs, you can close all terminal windows and moc will still run. As a minimalism enthusiast, I can say that moc is really the **perfect** music player.

When I started using a Mac, I was amazingly surprised to see that *most* of the command-line tools I was addicted to were available via MacPorts, including moc. However, until a couple days ago, I was not able to use it due to an error &mdash; I didn't really try hard to be honest. Anyway, here is how to install and use moc on OS X.

### Installing moc

First make sure you have MacPorts installed. Open an iTerm (or Terminal.app) and type the following command:

{% highlight console %}
sudo port install moc +autojack +vorbis
{% endhighlight %}


Now if you try to type `moc` in a terminal you will get an error saying that the `moc` command doesn't exist. The executable is called `mocp`. However, `mocp` is a client and it needs a driver to run. `jack` is such a driver and it was installed when you installed moc. To avoid having to run jack every time you want to run moc, I created a small script that does it for you:

{% highlight bash %}
#!/bin/bash

# /!\ WARNING /!\
# ---------------
# DO NOT PUT THE CONTENTS OF THIS SCRIPT INTO
# A FUNCTION OR ELSE MOC WILL STOP RUNNING AS
# SOON AS YOU CLOSE THE TERMINAL WINDOW IN WHICH
# IT WAS FIRST LAUNCHED!!

number=$(ps aux | grep jackd | grep -v grep | wc -l)

# if jackd is not running, launch it because moc needs it.
# the -T option makes sure that jack quits when mocp quits
# so that it doesn't eat up cpu for nothing
if [[ ! $number -gt 0 ]]
then
	jackd -T -d coreaudio &> /dev/null &
fi

mocp
{% endhighlight %}
gist: [464586](http://gist.github.com/464586)
{: .label }

Save that code in a file called `moc` and put it somewhere in your `$PATH` &mdash; I put all the script that I write in `~/bin`. The `moc` command is now available and you don't ever need to worry about `jack`.

### Using moc

Type `moc` in iTerm (or Terminal.app) and moc should appear with a very ugly BSoD-like blue theme. To change the theme, type `T` (that's `shift-t` not just `t`) and select the theme you like (Validate with &#x21A9;); press `esc` to go back to the main screen. To see a list of all the shortcuts, type `?`. Here is a very basic list of the ones a I use the most:

{% highlight text %}
q               Detach MOC from the server
Q               Quit
UP/DOWN         Move up or down in the menu
A               Add a folder to the playlist
a               Add a file to the playlist
C               Clear the playlist
TAB             Switch between playlist and file list
]               Silent seek forward 5 seconds
[               Silent seek backwards 5 seconds
R               Toggle repeat
S               Toggle shuffle
n               Play next file
b               Play previous file
ESC             Go back to the main screen
?               Show the list of all the keyboard shortcuts
{% endhighlight %}

Press `Q` to quit moc. If you open moc again, you will see that the default theme is used again. Before I go any further, I would like to show a theme that I found on the internet because I don't really link any of the default themes (except for `transparent-background` which is very similar to the one I will show you):

{% highlight text %}
# Copy what's below and save it in ~/.moc/themes/moc-orpheus
# moc-orpheus is the name of the file; don't give it an extension.
# Also, create the themes folder if it doesn't exist.
# I found this theme at this address:
# http://nic-nac-project.org/~orveldv/wiki/doku.php?id=moc
# A couple ather themes are also available there.

background           = black    black   normal
frame                = blue     black   bold
window_title         = black    black   bold
directory            = cyan     black   normal
selected_directory   = cyan     black   bold
playlist             = white    black   normal
selected_playlist    = cyan     black   bold
file                 = green    black   normal
selected_file        = green    black   bold
marked_file          = yellow   black   bold
marked_selected_file = green    black   bold
info                 = blue     black   bold
status               = black    white   normal
title                = yellow   black   bold
state                = green    black   bold,blink
current_time         = white    black   normal
time_left            = black    black   bold
total_time           = green    black   normal
time_total_frames    = black    black   bold
sound_parameters     = white    black   normal
legend               = green    black   normal
disabled             = black    black   bold
enabled              = white    black   normal
empty_mixer_bar      = white    black   normal
filled_mixer_bar     = black    white   normal
empty_time_bar       = black    black   normal
filled_time_bar      = black    white   bold
entry                = white    black   normal
entry_title          = black    white   normal
error                = yellow   black   bold
message              = yellow   black   bold
plist_time           = black    white   normal
{% endhighlight %}
gist: [464590](http://gist.github.com/464586)
{: .label }

You have two choices to set the default theme:

1. Edit the `moc` script you created above and append `-T moc-orpheus` to the `mocp` command on the last line.
2. Create a config file and put the name of the theme you like there &mdash; that's the solution that I prefer.

I will explain how to proceed with the config file choice. Create a file named `config` (no extension) in `~/.moc` and paste the following line in it:

{% highlight bash %}
# /!\ WARNING /!\
# ---------------
# YOU NEED TO INSERT AT LEAST ONE BLANK LINE
# AT THE BOTTOM OF THE FILE OTHERWIZE YOU WILL
# GET A FATAL ERROR AND WON'T BE ABLE TO LAUNCH MOC!

# Default theme.
Theme = moc-orpheus

# Turn on repeat by default.
Repeat = yes
{% endhighlight %}
gist: [464593](http://gist.github.com/464586)
{: .label }

There is an sample config file in `/opt/local/var/macports/software/moc/2.4.4_0+autojack+vorbis/opt/local/share/doc/moc/` with all the possible configuration variables that you can set.

> If you installed moc without any variants, replace `2.4.4_0+autojack+vorbis` by `2.4.4_0`

In the same folder as the sample config file, there is a sample keymap file. If you want to change any keyboard shortcut, create a `keymap` file in `~/.moc` and set your new keyboard shortcuts as demonstrated in the sample keymap file.

### <del>One</del> Two more <del>thing</del> things...

First, let's take care of the **GeekTool** integration. I <del>created</del> modified a script (see the "Let me give credit where credit is due" section for more details) to display info about the current song using GeekTool:

{% highlight bash %}
#!/bin/bash

# First let's check if moc is running...
if [[ $(ps aux | grep mocp | grep -v grep | wc -l) -gt 0 ]];
then
	
	out=$(/opt/local/bin/mocp -i)
	
	# Parse mocp output.
	while IFS=: read -r field value; do
		case $field in
			Artist) artist=$value;;
			Album) album=$value;;
			SongTitle) title=$value;;
		esac
	done <<< "$out"
	
	if [[ $1 ]]
	then
		case "$1" in
			'artist'|'ARTIST'|'Artist')
				echo $artist
			;;
			'song'|'SONG'|'Song')
				echo $title
			;;
			'album'|'ALBUM'|'Album')
				echo $album
			;;
			*)
				echo "$1"
			;;
		esac
	else
		echo "$title by $artist (album: $album)"
	fi
fi
{% endhighlight %}
gist: [464598](http://gist.github.com/464586)
{: .label }

With this script, you can selectively display the song title, the artist or the album of the song currently playing in moc. For the sake of this example, I will refer to the script above as "mi" (which is actually the name I gave it on my mac). mi takes one optional parameter:

* `song` &mdash; displays the name of the song.
* `artist` &mdash; displays the name of the artist.
* `album` &mdash; displays the name of the album.
* Anything else will be outputted as text; this could be used to create labels even though it's much easier to just use `echo` for that.
* No parameter &mdash; if no argument is passed, the script will display the song, the artist and the album.

I created four geeklets that you can download [here](http://azizlight.me/s/mocgeeklets). You will need to have the script above saved as `mi` in `~/bin` or else you are going to have to either edit the geeklets or create new ones.

Finally, I worked out a way to enable Growl support. However, I tried hard and could not launch the growl script and moc at the same time without ending up having a bunch of errors. So the only solution I found is to launch the growl script manually after launching moc. After that, the script runs in the background and quits at the same time as moc. Here is the script:

{% highlight bash %}
#!/bin/bash

while out=$(mocp -i); do

    # Parse mocp output.
    while IFS=: read -r field value; do
        case $field in
            Artist) artist=$value;;
            Album) album=$value;;
            SongTitle) title=$value;;
        esac
    done <<< "$out"

    # Don't do anything if we're still on the same song.
    [[ "$artist-$album-$title" = "$current" ]] && { sleep 1; continue; }

    # Growl notify this information
	if [[ $album && $artist && $title ]]; then
		growlnotify -t "moc: $title" -n "mocp" -m "by $artist"$'\n'"(album: $album)"
	fi

    # Remember the current song.
    current="$artist-$album-$title"

done
{% endhighlight %}
gist: [465244](http://gist.github.com/464586)
{: .label }

Save this script in `~/bin` as `mi-growl.sh` (or whatever you want to call it). You should run this script with this command if you want it to run in the background without outputting any errors:

{% highlight console %}
mi-growl.sh &> /dev/null &
{% endhighlight %}

However, it's a pain to run this command everytime you want to enable growl support for moc, so I created an alias for it. I also added a bunch of other aliases that I use while using moc:

{% highlight bash %}
alias mg="mi-growl.sh &> /dev/null &" # launch growl support
alias mof="mocp -f" # next
alias mor="mocp -r" # prev
alias mop="mocp -G" # play/pause
alias mos="mocp -s" # stop
alias mox="mocp -x" # exit
{% endhighlight %}
gist: [465247](http://gist.github.com/464586)
{: .label }

Put those aliases either in `.bash_profile`, `.bashrc`, `.bash_aliases`... it depends on your setup, I use oh-my-zsh and I've put them in my custom aliases file there.

### Bugs

No matter how hard I try, I can't manage to eliminate the bugs, and there seem to be one or two of them that are kind of annoying when using moc on OS X. The most annoying one that I found, is when moc stays open with a song paused for a long time and then you try to resume that song, moc will...well the song won't play, you'll have to quit moc, kill the server with a bunch of `killall mocp` calls, close the terminal window, etc. In other words, I have no clue what happens, sometimes it just stops working. But if you ask me, it's totally worth the headache since moc is definitely the most minimalistic user-friendly terminal music player.

### Let me give credit where credit is due

**[lhunath](http://www.lhunath.com/)** from the `#bash` channel on the `Freenode` network wrote the growl script. He didn't even have moc or growl installed so he could not do any kind of testing, which is amazing if you ask me! I also modified a bit his script to create the geektool version (I probably butchered it too...)

### Related links

* [moc](http://moc.daper.net/): The official website.
* [moc themes](http://nic-nac-project.org/~orveldv/wiki/doku.php?id=moc)
* [MacPorts](http://www.macports.org/)
* [GeekTool](http://projects.tynsoe.org/en/geektool/)
* [Growl](http://growl.info/)