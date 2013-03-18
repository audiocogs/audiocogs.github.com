---
title: Problems with a 'pure Javascript' implementation of H.264
date: May 9, 2012
layout: post
author: Jens Nockert (@jensnockert)
---

This was [originally posted](http://blog.aventine.se/post/22679577526/broadway-and-h264) on [aventine.se](http://aventine.se).


I have written a lot of audio decoders in Javascript, and helped write a few more. I have never tackled video for a few reasons, and I'll try to sum up why there will probably never be one implemented in 'pure' Javascript, and the methods with which I think it will be implemented instead.

Even the most high-end Audio codecs are also designed to work on really low-end DSP devices. ALAC (Apple Lossless Audio Codec) for example, decodes stereo fine in software on one of the 90 MHz ARM 7TDMI cores in the original iPod. AAC requires a bit more, but it is still within the reach of software on a relatively slow processor, like a Pentium or G3. A modern ARM processor can decode MP3 at a clock-speed of mere 10MHz, and with a bit more, AAC, which essentially is the most demanding codec that you'll meet on the web.

Video codecs on the other hand are an entirely different story. The 2.4GHz Core 2 Duo in my laptop (a Macbook Pro) has serious problems decoding high-end (1080p Hi10P for example) H.264 in with FFmpeg. My desktop, a reasonably modern Xeon quad-core, handles these videos fine using FFmpeg, but with significant load. Note that this is with an implementation that is hand-optimized with assembly. To improve the situation, we cannot depend on hardware support either, because it is often out of date. No graphics card in my collection support this profile in hardware yet for example.

On top of these problems, there are some serious limitations in Javascript/ECMAScript that makes it a bad platform for video decoding. And while it is a very cool demo of emscripten, these are some of the reasons why I don't think that Broadway.js will ever be able to decode H.264 in any sort of sane capacity using merely emscripten and some minor optimizations done by hand without a radically different Javascript engine to support it.


Floating-point
--------------------------------------------------------------------------------

Essentially all operations in Javascript operate on floating-point numbers, and this is not likely to change in the future. For audio codecs, this is not really a problem since they tend to be designed in a way that you can implement them as both fixed-point and floating-point.

Video codecs on the other hand tend to rely a lot on fixed-point for optimization, H.264 is even optimized to avoid needing floating-point as much as possible. Even the discrete cosine transform and motion compensation in H.264 is modified to operate on fixed-point numbers instead of floating-point.

The reason for this is that modern processors can often process fixed-point operations much faster, especially the 8 and 16 bit operations that are the most common. These short integer instructions often have at least 4 times faster thoroughput than double precision floating-point. Certain complex instructions like division make the difference irrelevant, and in many cases require fallback to floating-point, but these operations are extremely uncommon in H.264.


SIMD
--------------------------------------------------------------------------------

This is before the SIMD penalty is added for Javascript, because current Javascript engines utilize only scalar operations, a significant part of the execution hardware (1/2 to 1/4) spends most of the time idling.

Most decoders utilize these SIMD instructions, which gives them access to 8-16 times more throughput per core for simple operations. And on top of that, there are special instructions for optimizing MPEG codecs, giving a quite measurable speedup on top of that, which you are unlikely to be able to utilize without hand-optimized code.


Threads
--------------------------------------------------------------------------------

To provide the final blow against current Javascript, there is very little possibility for shared memory multicore programming in a browser. Workers are not good enough to do this, I haven't actually measured this as I do not plan to implement a video decoder with workers, but I think that the cost of communication and latency is currently too high for it to make sense.

Only using a single core on a processor that has 2-8 is another problem that would keep a Javascript implementation from ever competing with a native implementation.


Solution
--------------------------------------------------------------------------------

There are two obvious solutions to all of these problems that are being prototyped on the web right now, WebCL and Rivertrail. Both of these are designed to solve the threading problem mainly, which is likely not the biggest issue, but it is still significant.

Rivertrail could solve most of these problems since it is currently based on Intel's OpenCL runtime, which has good optimizers. It isn't designed for this very specialized task, and while it does allow you to reduce precision, it doesn't allow direct access to integer or media instructions, but it is a much better option than pure Javascript and with the addition of an integer API to Javascript, this could easily turn into the preferred method.

WebCL (OpenCL for the web) on the other hand, already solves most or all of these problems since it is essentially a massively parallel C with SIMD and device-specific extensions. It even allows for the GPU to pick up most of the burden, which is in many cases preferable to running on the CPU due to the extra computational power available.

There are probably other solutions as well, but just hoping that single-threaded Javascript with double precision floating-point will ever be enough is naïve and counter-productive in my opinion. Especially on mobile devices, which have special concerns, WebCL is in a great position to solve these too in the future.

And while I would love to be proved wrong about this, I don't think I will be for a long while, and at that point, there will be more advanced codecs and higher resolutions around to target.

