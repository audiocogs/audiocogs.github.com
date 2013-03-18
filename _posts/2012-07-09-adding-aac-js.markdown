---
title: "Adding AAC.js to Our Codecs Arsenal"
date: July 09, 2012
layout: post
author: Devon Govett (@devongovett)
---

{% include ofmlabs-archive.markdown %}

Today, we are releasing [AAC.js](https://github.com/audiocogs/aac.js), our newest JavaScript audio codec written on top of [Aurora.js](https://github.com/audiocogs/aurora.js).

Advanced Audio Coding (AAC) is a standardized, high quality lossy audio codec, designed as the successor to the MP3 format. AAC is now one of the most widely deployed audio codecs, and such names as the iTunes Store distribute music in the AAC format.

AAC can be played in a limited number of browsers using the standard HTML5 &lt;audio> element, but some browsers choose not to support the format for various reasons.  AAC.js enables playback and other tasks that might need decoding in all browsers, using JavaScript.

Currently, AAC.js supports the Low Complexity profile, which is the most common profile in use today. Support for the Main, High Efficiency (Spectral Band Replication) and High Efficiency v2 (Spectral Band Replication + Parametric Stereo) profiles is planned. Other profiles, such as the low delay, and error resilient profiles are not supported, but we'd love pull requests if you feel motivated to implement them!

Since releasing [FLAC.js](https://github.com/audiocogs/flac.js) and [Aurora.js](https://github.com/audiocogs/aurora.js) a few weeks ago, we've seen lots of interest from the community in writing more codecs and using Aurora in other ways.  We added a [Known Uses](https://github.com/audiocogs/aurora.js/wiki/Known-Uses) page to the Aurora.js wiki to track uses of Aurora and the codecs people have written for it.  If you wrote something using Aurora, and want us and the world to know about it, be sure to add it to that page!

AAC.js is just another reason why building audio applications in the browser is continuing to get easier.  Armed with a suite of JavaScript audio codecs, your audio editors, DJ apps, Digital Audio Workstations and more can now be built in the browser more easily, and with support for more codecs, the user experience will be even better.  AAC is a common format for users to have their music in, and we hope AAC.js will improve web audio applications.

Be sure to [check out the demo](http://audiocogs.org/codecs/aac/), to which we've added the ability to play music off of your own hard drive, and also the code for AAC.js on [Github](https://github.com/audiocogs/aac.js).
