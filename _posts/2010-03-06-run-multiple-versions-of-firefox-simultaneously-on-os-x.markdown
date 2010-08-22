---
layout: post
title: Run multiple versions of Firefox simultaneously on OS X
---

Before last week, I relied on tools like Browsershots to test my websites in different browsers. It was highly ineffective because everytime I took a screenshot I had to wait for the image to generate and when trying to fix little graphical bugs...let's just say that it's not a reliable solution. I decided to find a way to install different version of Firefox and run them at the same time. I found the tricks a other sites but the information was scattered so I decided to regroup everything here. Here is how I did it.

### Install older versions
The first thing to do is to install older versions of Firefox without touching your current install. Got to [Mozilla's FTP server](ftp://ftp.mozilla.org/pub/mozilla.org/firefox/releases/) and download the versions you're interested in; I downloaded the latest versions of Firefox 2.0 and Firefox 3.0, the links are at the bottom of this post. **However, be careful, don't install anything just yet.** What you have to do is mount the disk images, drag the Firefox executable on your Deskop, and rename it to something else. ie: Firefox 2.0 and Firefox 3.0. Once you've done that, you can drag the executables to the Applications folder wihtout overwritting anything.

### Run the different versions simultaneously
To run multiple versions of Firefox at the same time, you have to download and install a little application called [MultiFirefox](http://davemartorana.com/multifirefox/). The application will ask you to create a new profile. Basically you have to create one additional profile for each instance of Firefox you want to run simultaneously, so two new profiles in my case.

All done! You can now test your websites efficiently in every version of Firefox.

### Related links
* [Mozilla FTP server](ftp://ftp.mozilla.org/pub/mozilla.org/firefox/releases/)
* [Latest Firefox 2.0 English (en-US) version (v2.0.20)](ftp://ftp.mozilla.org/pub/mozilla.org/firefox/releases/2.0.0.20/mac/en-US/Firefox%202.0.0.20.dmg)
* [Latest Firefox 3.0 English (en-US) version (v3.0.18)](ftp://ftp.mozilla.org/pub/mozilla.org/firefox/releases/3.0.18/mac/en-US/Firefox%203.0.18.dmg)
* [MultiFirefox](http://davemartorana.com/multifirefox/)
