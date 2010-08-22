---
layout: post
title: Adobe (Conversion?) Error in Snow Leopard
---

Yesterday I was bored and wanted to try something new. I began learning Objective-C. First thing that I got when I compiled and ran the `Hello, World!` program is an error:

{% highlight text %}
Error loading /Library/ScriptingAdditions/Adobe Unit Types.osax/Contents/MacOS/Adobe Unit Types:  dlopen(/Library/ScriptingAdditions/Adobe Unit Types.osax/Contents/MacOS/Adobe Unit Types, 262): no suitable image found.  Did find:  /Library/ScriptingAdditions/Adobe Unit Types.osax/Contents/MacOS/Adobe Unit Types: no matching architecture in universal wrapper TextApp: OpenScripting.framework - scripting addition "/Library/ScriptingAdditions/Adobe Unit Types.osax" declares no loadable handlers.
{% endhighlight %}

Ugly as it is, it's also very simple to fix, just follow the instructions on [that page](http://kb2.adobe.com/cps/516/cpsid_51615.html)