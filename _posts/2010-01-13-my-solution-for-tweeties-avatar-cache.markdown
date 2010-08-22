---
layout: post
title: My solution for Tweetie's avatar cache
---

<p>I love Tweetie. I tried about all the most famous Twitter clients (except most of the AIR based ones, I don't like Adobe AIR), and Tweetie is the best one imho. There are some other good ones though: Nambu, Kiwi, Twitterific, ... that's it. Tweetdeck is completely bloated.</p>
<p>Anyway, the only thing that really sucks in Tweetie is the fact that it doesn't provide an easy way to delete the cached profile images. The consquence of this is that when somebody changes his avatar, the change takes at least three days to appear in Tweetie. Unless you delete the cached images manually.</p>
<p>My solution was to use AppZapper, which prevents me from search the folder myself. You could replace AppZapper by any other application removal app; mac.appstorm did <a href="http://mac.appstorm.net/roundups/utilities-roundups/6-ways-to-correctly-delete-applications/">a nice roundup</a> a while ago.</p>
<p>If you don't want to install a new application, here is the path of the folder you need to delete:</p>
<p><code>~/Library/Caches/com.atebits.tweetie.profile-images</code></p>
<p>One problem remains: a while ago, Twitter had a bug that made newly uploaded profile pictures broken. For some reason Tweetie is the only application that doesn't show those pictures (so they're broken in Tweetie only??), so the people with broken avatar should re-upload them.</p> 