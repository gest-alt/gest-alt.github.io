---
layout: post
title: Atlanta, Residential Segregation, and The End of Suburban White Flight?
author: Nic Becker
category: visualization
img: https://i.imgur.com/Dr4OSKJ.png
mathjax: true
---

This is a working draft motivated by Kevin M. Kruse's book [White Flight: Atlanta and the Making of Modern Conservatism](https://press.princeton.edu/titles/8043.html), [Brookings analysis on income inequality](https://www.brookings.edu/research/city-and-metropolitan-income-inequality-data-reveal-ups-and-downs-through-2016/), and my birth(place).

It began as a visualization exercise, but I'm slowly working towards something true to the title.


Todo:
* type up analysis of diversity statistic and neighborhood covariates from Opportunity Insights
* add charts showing the significant population increases in Hispanic and Asian populations between 2000 and 2010
* map residential segregation by income
* map residential segregation by economic outcomes

(last updated: 06.20.2019)

### How to read these maps

![Legend](https://i.imgur.com/qUMYeRF.png)

### How the city has changed between 1990 and 2017

<div style="position:relative; width:100%; height:400px;">
  <div id='before' style = "position:absolute; top:0; bottom:0; width:100%;"></div>
  <div id='after' style = "position:absolute; top:0; bottom:0; width:100%;"></div>
</div>

<script>
  mapboxgl.accessToken = 'pk.eyJ1IjoibnBiZWNrZXIiLCJhIjoiY2p1aTBub2I2MTVuejQzbWZxMXRkb2h2ZSJ9.aw6eHFpggwgWAFAbOKMP7Q';
  var beforeMap = new mapboxgl.Map({
    container: 'before',
    style: 'mapbox://styles/npbecker/cjx0ufv6191nh1cpc2z2e015q',
    center: [-84.3880, 33.7490], // starting position [lng, lat]
    zoom: 8.5 // starting zoom
  });

  var afterMap = new mapboxgl.Map({
    container: 'after',
    style: 'mapbox://styles/npbecker/cjx0u2s8o9lle1dpqpuwtiutp',
    center: [-84.3880, 33.7490], // starting position [lng, lat]
    zoom: 8.5 // starting zoom
  });

  var map = new mapboxgl.Compare(beforeMap, afterMap, {
  // Set this to enable comparing two maps by mouse movement:
  // mousemove: true
  });
</script>

### How diversity varies in the city

I calculated the [Multigroup Entropy Index](https://www2.census.gov/programs-surveys/demo/about/housing-patterns/multigroup_entropy.pdf) (or Theil Index) for Atlanta in 2017 to quantitatively estimate diversity and neighborhood segregation. The ***entropy score***, which is used in the calculation of the index, is a representation of "diversity" measuring the relative proportions of different groups within a region. It does not consider distribution across or within the region. *The higher the number, the more diverse an area.*

$$E = \sum_{r=1}^{R} \Pi_r \log(\frac{1}{\Pi_r})$$

> Metropolitan area’s entropy score. ∏<sub>r</sub> represents a racial/ethnic group’s proportion of the whole metropolitan area.

$$E_i = \sum_{r=1}^{R} \Pi_{ri} \log(\frac{1}{\Pi_{ri}})$$

> A Census tract's entropy score. Similarly, ∏<sub>ri</sub> represents a racial/ethnic group’s proportion of the population in tract i.

The ***entropy index***, on the other hand, measures the distribution of groups across neighborhoods and is a representation of segregation. The index is a weighted average deviation of each Census tract’s entropy from the metropolitan area's entropy, expressed as a fraction of the metropolitan area’s total entropy. *It is zero when all areas have the same composition as the entire metropolitan area (i.e., maximum integration), and one when all areas contain one group only (maximum segregation).*

$$H = \sum_{i = 1}^{N}\Big[\frac{t_i(E-E_i)}{ET}\Big]$$

>  t<sub>i</sub> refers to the total population of tract i, T is the is the metropolitan area population, n is
the number of tracts, and E<sub>i</sub> and E represent tract i's diversity (entropy) and metropolitan area
diversity, respectively.

 <!-- static map:
<img alt='static Mapbox map test' src='https://api.mapbox.com/styles/v1/npbecker/cjx0w4ro28y5x1dozr9cnor9o/static/-84.3880,33.7490,8.5/600x400@2x?access_token=pk.eyJ1IjoibnBiZWNrZXIiLCJhIjoiY2p1aTBub2I2MTVuejQzbWZxMXRkb2h2ZSJ9.aw6eHFpggwgWAFAbOKMP7Q'>
-->

<div style="position:relative; width:100%; height:400px;">
  <div id='diversity_map' style = "position:absolute; top:0; bottom:0; width:100%;"></div>
  <select id="diversityselector" style = "position:absolute; top:10px; left:10px; outline: none; font-family: inconsolata; border: 8px solid transparent">
    <option class="year1" value="2017-diversity">2017</option>
    <option class="year2" value="2010-diversity">2010</option>
    <option class="year3" value="2000-diversity">2000</option>
    <option class="year4" value="1990-diversity">1990</option>
  </select>
</div>

> Demographic data for 1990, 2000, and 2010 were taken from the decennial census. Data for 2017 uses population estimates from the 5-year American Community Survey.

<script>
  mapboxgl.accessToken = 'pk.eyJ1IjoibnBiZWNrZXIiLCJhIjoiY2p1aTBub2I2MTVuejQzbWZxMXRkb2h2ZSJ9.aw6eHFpggwgWAFAbOKMP7Q';
  var diversity_map = new mapboxgl.Map({
    container: 'diversity_map', // container id
    style: 'mapbox://styles/npbecker/cjx0w4ro28y5x1dozr9cnor9o', // stylesheet location
    center: [-84.3880, 33.7490], // starting position [lng, lat]
    zoom: 8.65 // starting zoom
  });

  diversity_map.addControl(new mapboxgl.FullscreenControl());

  const diversity_dropdown = document.getElementById('diversityselector');

  var previous_diversity;

  diversity_dropdown.addEventListener('change', (e) => {
    var clicked_year = e.target.value;
    console.log(clicked_year);
    e.preventDefault();
    e.stopPropagation();
    diversity_map.setLayoutProperty(clicked_year, 'visibility', 'visible');
    diversity_map.setLayoutProperty(previous_diversity, 'visibility', 'none');
    previous_diversity = clicked_year
  });
</script>

### Dot distribution maps for the past 30 years

<!-- I'm putting all the css in html tags because I don't know what I'm doing and I'm winging all of this shhhhh -->

<div style="position:relative; width:100%; height:400px;">
  <div id='map' style = "position:absolute; top:0; bottom:0; width:100%;"></div>
  <select id="yearselector" style = "position:absolute; top:10px; left:10px; outline: none; font-family: inconsolata; border: 8px solid transparent">
    <option class="year1" value="2017">2017</option>
    <option class="year2" value="2010">2010</option>
    <option class="year3" value="2000">2000</option>
    <option class="year4" value="1990">1990</option>
  </select>
</div>

> Demographic data for 1990, 2000, and 2010 were taken from the decennial census. Data for 2017 uses population estimates from the 5-year American Community Survey.

<script>
  mapboxgl.accessToken = 'pk.eyJ1IjoibnBiZWNrZXIiLCJhIjoiY2p1aTBub2I2MTVuejQzbWZxMXRkb2h2ZSJ9.aw6eHFpggwgWAFAbOKMP7Q';
  var map = new mapboxgl.Map({
    container: 'map', // container id
    style: 'mapbox://styles/npbecker/cjx0u2s8o9lle1dpqpuwtiutp', // stylesheet location
    center: [-84.3880, 33.7490], // starting position [lng, lat]
    zoom: 8.65 // starting zoom
  });

  map.addControl(new mapboxgl.FullscreenControl());

  const dropdown = document.getElementById('yearselector');

  var previous;
  window.onload=function()
  {
      previous = document.getElementById("yearselector").value;
      previous_diversity = document.getElementById("diversityselector").value;
  }

  dropdown.addEventListener('change', (e) => {
    var clicked_year = e.target.value;
    e.preventDefault();
    e.stopPropagation();
    map.setLayoutProperty(clicked_year, 'visibility', 'visible');
    map.setLayoutProperty(previous, 'visibility', 'none');
    previous = clicked_year
  });
</script>

### White flight in earlier decades

Atlanta once championed public school desegregation. In 1961, Mayor Hartsfield told anyone who would listen that Atlanta was the city that was *"too busy to hate"*. The details of this are chronicled in Kruse's *White Flight* mentioned above, but it basically boils down to this: school desegregation and white transfer requests were drivers of white Atlanta withdrawing to the suburbs. Segregationists advocated "to maintain freedom of association," shaping what Kruse argues is the beginning of a conservative emphasis on negative freedoms that we still see today (i.e. individual preferences at the expense of public equity).

Soon after the Mayor's coinage, Atlanta saw itself become the city too busy *moving* to hate. In the 1960s, the white population within the city limits dropped by 60,000. The next decade another 100,000 fled. The following maps show the proportion of black residents in Atlanta and its vicinity.
<!-- Todo: population maps, p5 of white flight details tens of thousands of whites leaving the city in the 60s and 70s. -->

![Population maps from Kevin M. Kruse's book White Flight](https://i.imgur.com/LzuUF7t.png)

> Taken from Kruse's book. [Click here](https://i.imgur.com/LzuUF7t.png) for a bigger  version.

Racist housing policy also had a significant role in shaping Atlanta's current demographic landscape. The roots of this are summarized in the now infamous redlining maps of the Home Owners' Loan Corporation.

![](https://www.atlantastudies.org/wp-content/uploads/2017/08/Rhodes_HOLC-Scan.jpg)

> [Source: Geographies of Privilege and Exclusion, Jason Rhodes](https://www.atlantastudies.org/2017/09/07/jason-rhodes-geographies-of-privilege-and-exclusion-the-1938-home-owners-loan-corporation-residential-security-map-of-atlanta/)

It's interesting to consider this map with 2017 demographics in mind:

<style>
  .map-overlay {
  	font: bold 12px/20px 'inconsolata';
  	position: absolute;
  	width: 30%;
  	top: 0;
  	left: 0;
  	padding: 10px;
  }

  .map-overlay .map-overlay-inner {
  	background-color: #fff;
  	border-radius: 3px;
  	padding: 5px 10px 5px 10px;
  	margin-bottom: 10px;
  }

  .map-overlay label {
  	display: block;
  	margin: 0 0 0px;
  }

  .map-overlay input {
  	background-color: transparent;
  	display: inline-block;
  	width: 100%;
  	position: relative;
  	margin: 0;
  	cursor: ew-resize;
  }
</style>

<div style="position:relative; width:100%; height:400px;">
  <div id='overlay_map' style = "position:absolute; top:0; bottom:0; width:100%;"></div>
  <div class='map-overlay top'>
    <div class='map-overlay-inner'>
      <label>Overlay opacity: <span id='slider-value'>75%</span></label>
      <input id='slider' type='range' min='0' max='100' step='0' value='75' />
    </div>
  </div>
</div>

<script>
  mapboxgl.accessToken = 'pk.eyJ1IjoibnBiZWNrZXIiLCJhIjoiY2p1aTBub2I2MTVuejQzbWZxMXRkb2h2ZSJ9.aw6eHFpggwgWAFAbOKMP7Q';
  var overlay_map = new mapboxgl.Map({
    container: 'overlay_map', // container id
    style: 'mapbox://styles/npbecker/cjx0u2s8o9lle1dpqpuwtiutp', // stylesheet location
    center: [-84.3730, 33.7720], // starting position [lng, lat]
    zoom: 10.0 // starting zoom
  });

  y2 = 33.852824;
  y1 = 33.689320;
  x1 = -84.487325;
  x2 = -84.250155;

  overlay_map.on('load', function() {
      overlay_map.addSource("HOLC-map", {
          "type": "image",
          "url": "https://i.imgur.com/ovuvNJi.png",
          "coordinates": [
              [x1, y2],
              [x2, y2],
              [x2, y1],
              [x1, y1]
          ]
      });

      overlay_map.addLayer({
          "id": "overlay",
          "source": "HOLC-map",
          "type": "raster"
      }, "road-label");

      overlay_map.setPaintProperty('overlay', 'raster-opacity', parseInt(75, 10) / 100);

      slider.addEventListener('input', function(e) {
      // Adjust the layers opacity. layer here is arbitrary - this could
      // be another layer name found in your style or a custom layer
      // added on the fly using `addSource`.
      overlay_map.setPaintProperty('overlay', 'raster-opacity', parseInt(e.target.value, 10) / 100);

      // Value indicator
      sliderValue.textContent = e.target.value + '%';
      });

  });

  overlay_map.addControl(new mapboxgl.FullscreenControl());

  var slider = document.getElementById('slider');
  var sliderValue = document.getElementById('slider-value');

</script>

My maps were inspired by the [Washington Post](https://www.washingtonpost.com/graphics/2018/national/segregation-us-cities/).
