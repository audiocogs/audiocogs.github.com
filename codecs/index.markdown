---
title: Codecs
layout: codecs-index
---

Web browsers are becoming more and more powerful, and new APIs like the [Web Audio API][web-audio] and [Audio Data API][audio-data] are making the web an ever more interesting and dynamic place. At [Audiocogs](/) we are invested in improving the state of audio on the web, and with [JSMad][jsmad] showed that decoding audio purely in JavaScript is possible thanks to these APIs and the hard work of browser makers and spec authors. Now we've done it again &mdash; not just once, but _three_ more times! With these, it is possible to play MP3, [Apple Lossless][apple-lossless], FLAC, and AAC even in browsers without native support.

With [JSMad](/codecs/mp3) we showed that decoding audio in JavaScript is possible, courtesy of these APIs and the hard work of browser creators and spec authors. After that, we ported the recently open sourced Apple Lossless decoder to JavaScript as [alac.js](/codecs/alac). However, we decided that wasn't enough, so we rolled out [flac.js](/codecs/flac). Then, suddenly, [aac.js](/codecs/aac) appeared.


[web-audio]: https://dvcs.w3.org/hg/audio/raw-file/tip/webaudio/specification.html
[audio-data]: https://wiki.mozilla.org/Audio_Data_API
[jsmad]: https://github.com/audiocogs/jsmad
[apple-lossless]: http://alac.macosforge.org/
