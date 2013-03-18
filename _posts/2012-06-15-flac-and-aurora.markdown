---
title: "Introducing FLAC.js: A Pure JavaScript FLAC Decoder"
date: June 15, 2012
layout: post
author: Jens Nockert (@jensnockert) and Devon Govett (@devongovett)
---

{% include ofmlabs-archive.markdown %}


Today Official.fm Labs is relesing our JavaScript [FLAC decoder](https://github.com/audiocogs/flac.js). FLAC is the "[Free Lossless Audio Codec](http://flac.sourceforge.net/)" which is probably the most common lossless audio codec around.

We have been waiting for a flashy demo to use it in for a long while, but we decided that you have waited long enough and wired it up with a song into a [streaming audio player](http://audiocogs.org/codecs/flac/). Thanks to [fONKSQUISh](http://www.myspace.com/fonksquish) for allowing us to use their songs. **Update**: if you use the [online demo](http://audiocogs.org/codecs/flac) chose a FLAC file from your hard drive for playback.


## What is interesting about a JavaScript FLAC decoder?

The main thing is that it runs on a lot of platforms and decodes FLAC encoded audio. The **decoder** by itself _should_ run on any platform that supports typed arrays, but we have only tested it on platforms that support an Audio API, like the Mozilla Audio Data API, and Google's Web Audio API. That means that it should work in Firefox, Chrome, and Webkit with Web Audio enabled.

We hoped that we could say that it runs on the iOS 6 beta, but we're having problems getting the Web Audio API to work reliably. However the decoder itself does appear to work. Hopefully by the time iOS 6 ships this fall, the Web Audio API will be more reliable and our codecs will begin to work on mobile devices.

Even without a real audio API, you could use it together with an HTML5 Audio tag, but then you would lose the realtime aspect since you cannot stream data into an Audio tag from JavaScript.  You would have to decode the entire file first, and then play it back, which is slow and a bad experience.  We're crossing our fingers that more browsers will begin to support the Web Audio API (which is on track to standardization now) - that's you, Opera and Internet Explorer!

We have already shown with [JSMad](https://github.com/audiocogs/jsmad) and [ALAC.js](https://github.com/audiocogs/alac.js) that decoding audio in JavaScript is possible and actually quite performant.  We think that this is a good way to add support for just about any audio codec possible to browsers and gain cross browser support.  The HTML5 Audio tag is great, but codec support issues are very real and encoding multiple formats is unacceptable.  We know that browsers will never agree to support every codec possible, but with a baseline of the Web Audio API supported, we can support whatever codecs we please via a JavaScript decoder.

Additionally, JavaScript audio decoding opens up a number of doors for previously impossible web applications, such as DJ apps, Garageband-esque apps, audio editors and more.  Let us know what you build with our decoders!  We're excited to see the doors they open.

The [FLAC decoder](https://github.com/audiocogs/flac.js) is released under the LGPL license (following the original license from FFmpeg), which means that you can use it freely; however, if you modify the FLAC decoder itself, then you need to provide the source to your users.

## Aurora.js

We've been working on a nice little framework called [Aurora.js](https://github.com/audiocogs/aurora.js) that we have been using to write our decoders so far.  Aurora handles common tasks for you such as dealing with binary data, and the decoding pipeline from source to demuxer to decoder, and finally to the audio hardware itself by abstracting browser audio APIs.  Aurora is designed to be easily extendible with more codecs, and that is exactly what we have been doing.  JSMad was written before Aurora existed, and since then, we've converted it to use Aurora in the form of [MP3.js](https://github.com/devongovett/mp3.js).  Additionally, we have [ALAC.js](https://github.com/audiocogs/alac.js) and now [FLAC.js](https://github.com/audiocogs/flac.js).  We have at least one more in the pipeline to release shortly!

The result of all of this, is that the Aurora framework makes it very nice to write demuxers and decoders for various container formats and codecs respectively.  It also makes it easy to extract various information about the format, duration, and metadata from audio files, and includes a high level player API that, in our opinion, is easier to work with than the HTML5 Audio tag.

You could use it for compressing samples for your game or synth, or building an awesome streaming music service. If you're interested in extending Aurora with your own demuxers and decoders (and we would love if you did), you should check out the [documentation](https://github.com/audiocogs/aurora.js/wiki) for the framework, and definitely read the [source code](https://github.com/audiocogs/aurora.js/)!  It is written in [CoffeeScript](http://coffee-script.org/) but we've worked to make it easy to use in regular JavaScript as well, and we have written demuxers and decoders in both languages.  We're already working on an AAC decoder, and we'd love to see an Ogg Vorbis decoder or anything else the community comes up with!

## Conclusion

The Web Audio API opens up many doors to us to build amazing audio applications in the browser.  Many of those applications will need to use compressed audio data, and we've been implementing the codecs to make that happen.  Be sure to check out the [demo](http://audiocogs.org/codecs/flac/) of [FLAC.js](https://github.com/audiocogs/flac.js) and write your own decoders using [Aurora.js](https://github.com/audiocogs/aurora.js).  We're excited to see the amazing apps you build!
