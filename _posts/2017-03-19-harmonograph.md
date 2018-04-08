---
layout: post
title:  Harmony and The Harmonograph
author: Nic Becker
category: Program
img: https://imgur.com/p5mTEt6.png
---
![](https://imgur.com/0b4gMWj.png)
*From [Harmonograph - A Visual Guide to the Mathematics of Music (Ashton)](https://www.scribd.com/doc/147969892/Anthony-Ashton-Harmonograph-A-Visual-Guide-to-the-Mathematics-of-Music-cleaned)*

There's a secret visual beauty in the sound that pervades daily life. Distortions in our atmospheric soup form patterns, surfaces, and shapes that our eyes will never see. Even guessing at the pressure patterns that emerge from a playing violin is mind-boggling—yet one thing is certain: the sight would be awe-inspiring.

Thankfully, sinusoids are everywhere in the physical world. And we can create something visual that is somewhat isometric to sounds and harmony. Some examples of this include [Chladni plates](https://www.youtube.com/watch?v=lRFysSAxWxI) and the [Kaleidophone](https://en.wikipedia.org/wiki/Kaleidophone).

Harmonographs concern [**Lissajous figures**](https://en.wikipedia.org/wiki/Lissajous_curve), which I came across earlier this year in a wonderful video describing [just intonation and equal temperament](https://www.youtube.com/watch?v=6NlI4No3s0M). My program simulates both a lateral *and* rotary harmonograph (illustrated above) using different combinations of pendulums [see resources below].

![Cycling through some intervals on a lateral harmonograph](https://imgur.com/IgCSB3C.gif)
*Cycling through some intervals on a lateral harmonograph.*

So how does this relate to music? Intervals are fundamental to how we think of notes, melody, and harmony. Every interval (e.g. a minor third, a perfect fifth) is measured by the ratio of two frequencies. If we allow the pendulums within a harmonograph to reflect these frequency ratios, beautiful symmetries arise. Note that all of the images here are the result of damped oscillation, meaning friction is simulated. Otherwise, we would only see one tracing of the lissajous curve.

The following images are in no particular order—two are common intervals, two are simulations with randomish parameters. I'll let you guess which is which (frequencies are shown in the right control panel).

![](https://imgur.com/2vDyYEY.png)
![](https://imgur.com/p5mTEt6.png)
<!-- ![](https://imgur.com/UemTvRU.png) boring -->
![](https://imgur.com/4IB9Omv.png)
![](https://imgur.com/skcpxJh.png)

**Helpful resources**

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/9c6eb3f0406b6c849767add602b00fbbed82676d)

[Wikipedia](https://en.wikipedia.org/wiki/Harmonograph#Computer-generated_harmonograph_figure) gives the equation for a damped pendulum.
From there, it's just a matter of deciding how many pendulums and degrees of freedom per pendulum that you want in your simulation. I found it useful to look at physical harmonographs. Here are my favorites:
* http://www.karlsims.com/harmonograph/
* http://paulbourke.net/geometry/harmonograph/
* https://johncarlosbaez.wordpress.com/2014/07/18/the-harmonograph/

*This project placed runner up out of 70+ submissions in the CS 106A graphics contest*
