---
layout: post
title: Tribute to fractal geometry
author: Nic Becker
category: digital fabrication
img: http://i.imgur.com/k8UpbPx.png
---

Looking at topographic maps reminded me of the branching patterns of electrical breakdown in material or air. The project entails two parts: 3D printed terrain and Lichtenberg figures/wood staining.

The terrain maps shown below are located at Tallulah Gorge State Park in north Georgia. Since the area isn't actually that big, or deep, finding decent elevation data was tricky.

I first tried using Derek Watkin's [insanely well made downloader](http://dwtkns.com/srtm30m/) for Shuttle Radar Topography Mission data. Unfortunately, after playing around with it, I learned that 30 meters did not provide a high enough resolution to get a decent map of the area. The [U.S. Geological Survey National Map](https://viewer.nationalmap.gov/basic/), on the other hand, provides digital elevation data up to 1/9 arcsecond (insane...). I clearly did not need that degree of accuracy for a 4x6in print, nor do I have the computing power to process it. I settled on the 1/3 arcsecond GridFloat format.

First, I isolated a boundary around Tallulah Gorge. This is easily done using the QGIS clipping tool.

![QGIS](http://i.imgur.com/H4jcGdA.jpg)

The resulting DEM file then must be converted to an stl in 3DEM.

![3DEM](http://i.imgur.com/idhWiaB.jpg)

Once I had an stl, it was just a matter of upscaling the z axis to exaggerate the gorge and extruding a level base.

![AccuTrans](http://i.imgur.com/U1oQDes.png)

![AccuTrans extrusion](http://i.imgur.com/k8UpbPx.png)

It begins...

Since I'm terrible at carpentry, the next step for me was coming up with a way to make the box look nice. If you look at the first DEM image above, the terrain patterns look a lot like Lichtenberg figures. I borrowed a microwave transformer from a broken microwave at school (yes, I asked), and am planning to burn the box sometime next week.

### Update [12/14/16]

I finally managed to fully print the terrain map in gold/green ABS filament. Problems with warping and plate adhesion required me to attempt the print several times over the course of a few days. It was a pain to do over exam week, but I'm really happy with how it turned out.

![](https://media.giphy.com/media/CHWSuxyTtWQW4/giphy.gif)

The lichtenberg figures also turned out pretty nice. There are a few visual cues that indicate the cool pattern/too burnt line that took me a few attempts to pick up on. I may try it again on a different box for the final gift.

![](http://i.imgur.com/wHX9aM3.jpg)

The next step is to sand down the box to remove any unwanted burn marks and then stain it.

### Update [12/17/16]

![](http://i.imgur.com/dcIL6ad.jpg)

![](http://i.imgur.com/QtwY3wi.jpg)

Sanded with 220, 400, then 600 grit. One coat of Red Chesnut stain. Three coats of clear gloss polyurethane.

and the original idea for reference:

![roughs](https://i.imgur.com/j82GYJQ.jpg)

### Resources

* [Making Tiny Worlds: from DEM to STL](http://www.the3dprintedfuture.com/shapespeare/)
* [Make Mountains in Blender [alterate method]](http://johnflower.org/tutorial/make-mountains-blender-height-maps)
* [90m SRTM tile grabber](http://dwtkns.com/srtm/)
* [30m SRTM tile grabber](http://dwtkns.com/srtm30m/)
* [USGS National Map](https://viewer.nationalmap.gov/basic/)
* [Shuttle Elevation Data](http://www2.jpl.nasa.gov/srtm/)
