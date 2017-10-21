---
layout: post
title: "Blog Upgrading Plan"
date: 2017-03-19
excerpt: "Building Jekyll Blog Project - Quick Progress Tracking"
project: true
tags: [project]
comments: true
---

## Charts
Figure out the way to apply charts and what use cases that I really need a chart to visualize the data for me.

First thought: [plotty](https://plot.ly/) ... but no, it's in python and i don't know how to integrate it into a Jekyll blog. A few google search should give me the answer maybe.
Or.. 
Found another solution: [Highcharts](http://www.highcharts.com/) all written in JavaScript and the data in JSON format.

<figure>
	<img src="http://i.imgur.com/JvjLE8B.jpg">
	<figcaption>The charts seem nice to me.</figcaption>
</figure>

Update 03-23-2017: Added Highcharts, feel like I don't need the charts anymore lol. Gonna leave it there until I need it for any reason. 
{: .notice}

<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
<style type="text/css">
#container {
	min-width: 310px;
    max-width: 800px;
    height: 400px;
    margin: 0 auto
    }
</style>

<script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/modules/exporting.js"></script>

<div id="container"></div>

<script type="text/javascript">

Highcharts.chart('container', {

    title: {
        text: 'Demo chart with random value, 2010-2016'
    },

    subtitle: {
        text: 'Demo chart for my blog'
    },

    yAxis: {
        title: {
            text: 'Productivity'
        }
    },
    legend: {
        layout: 'vertical',
        align: 'right',
        verticalAlign: 'middle'
    },

    plotOptions: {
        series: {
            pointStart: 1
        }
    },

    series: [{
        name: 'Total',
        data: [43934, 52503, 57177, 69658, 97031, 119931, 137133, 154175]
    }, {
        name: 'Dev 1',
        data: [24916, 24064, 29742, 29851, 32490, 30282, 38121, 40434]
    }, {
        name: 'Dev 2',
        data: [11744, 17722, 16005, 19771, 20185, 24377, 32147, 39387]
    }, {
        name: 'Dev 3',
        data: [null, null, 7988, 12169, 15112, 22452, 34400, 34227]
    }, {
        name: 'Dev 4',
        data: [12908, 5948, 8105, 11248, 8989, 11816, 18274, 18111]
    }]

});
</script>

---

## Comment System
This one should upgrade soon, right now I'm using a temporary "fast-food" plugin of Facebook. Heard they give a better comment system for blog by developing an application to integrate the comment plugin instead of this quick solution that I used.

Update 03-26-2017: Figured out. Wrote some lines of jquery to change the data-href value and Facebook Comment Plugin works fine now. 
{: .notice}

---

## Google Analytics
I thought I need it, but for now it seems like it doesn't help anything so gonna keep this here as a reminder.

04/21/2017 Got it here for no reason. Kinda easy to apply.
{: .notice}

---

## Syntax Section
This section is for me to try out the markdown syntax and Moon theme components.
