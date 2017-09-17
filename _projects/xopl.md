---
title: "XOPL"
subtitle: "3D Visualization of Exoplanet Data"
layout: project
quickdesc: "XOPL is a 3D visualization of all the confirmed exoplanets that had been discovered in the universe at the time of making this project."
technologies:
    - Javascript
    - WebGL
    - Python
    - Angularjs
liveproject: http://xoplapp.appspot.com/
priority: 2
thumbnail: imgs/xoplthumb.png
github: https://github.com/DerekRies/xopl-web
---

<div class="text-center big-figure">
    <figure class="figure">
        <img src="http://influenztial.appspot.com/app/img/xopl1.jpg">
        <figcaption class="figure-caption text-center">Viewing HD 40307 in XOPL</figcaption>
    </figure>
    <a href="{{page.liveproject}}" class="btn btn-lg btn-primary"><i class="fa fa-globe"></i> View Live Project</a>
    <a href="{{page.github}}" class="btn btn-lg btn-secondary"><i class="fa fa-github"></i> View on Github</a>
</div>

## Looking At Exoplanets

XOPL is a 3D visualization of all the confirmed exoplanets that had been discovered in the universe at the time of making this project. Most people can't get interested in Science, Astronomy/Space specifically, because it's just not "sexy" enough. Go ahead check out the data that NASA provides [here](https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=planets), sexy right?

##### What's an Exoplanet?

<blockquote class="blockquote">
    An extrasolar planet is a planet outside of our solar system that orbits a star. The first scientific detection of an exoplanet was in 1988, but the first confirmed detection did not come until 1992. As of 8 September 2017, there are 3,667 planets in 2,747 systems, with 616 systems having more than one planet.
    <footer class="blockquote-footer">
        Exoplanet Article on 
        <a href="https://en.wikipedia.org/wiki/Exoplanet"><cite title="Wikipedia Exoplanet">Wikipedia</cite></a>
    </footer>
</blockquote>

## The Goal of This Project

To encourage people to get interested in science and space by offering an aesthetically pleasing and engaging experience! Technically, to create a simulation driven by the data collected by NASA and other agencies, that people could explore and in the process learn more about other worlds and astronomy. Stars vary by size and color according to their mass, temperature, and radius.

## Features

##### Star Colors and Size

Not all stars are the same size or color. Some are large and cool, others small and hot. Stars are colored by their temperature in Kelvin. A Star Type M, Red Dwarf, might be around 3,500-5000K, while a Type O (Blue Star) could be upwards of 25,000K. Our star is a type G2V yellow dwarf with a temperature around 5778K.

<div class="text-center big-figure">
    <figure class="figure">
        <img src="{{site.url}}/imgs/xopl-hat-p-2.jpg" title="HAT-P-2, A Hot Blue Star in XOPL">
        <figcaption class="figure-caption text-center">HAT-P-2, A Hot Blue Star in XOPL</figcaption>
    </figure>
</div>

<div class="text-center big-figure">
    <figure class="figure">
        <img src="{{site.url}}/imgs/xopl-gj-581.jpg" title="Gliese 581, a much cooler Red Dwarf with more planets">
        <figcaption class="figure-caption text-center">Gliese 581, a much cooler Red Dwarf with more planets</figcaption>
    </figure>
</div>

##### Accurate Orbits

In XOPL the orbit lines that are drawn reflect the path of the planets orbit, taking into account the semimajor axis, orbit eccentricity, and orbital speed.

##### Smooth Camera

In order to keep the app feeling smooth and reactive, changing star systems animates between the two stars (Original Star -> New Star), and the camera can smoothly animate between different positions.

## What I Would Like to Add

Hopefully I have a chance to rewrite this application from scratch, and to update it a bit ([Helios]({{site.url}}/projects/helios.html) is kind of a rewrite, but was written for a hackathon and so it suffers from only having had a day or two to write it). If I ever do get around to rewriting this project here's what I'd like to include in the next version:

##### Better Graphics

This was my first project with WebGL and at the time I didn't have very much experience writing shaders. Now I'd like to go back and make something look really frickin cool! (The Stars in [Helios]({{site.url}}/projects/helios.html) are a bit better)

##### Skyboxes With Other Stars

The current application doesn't even have a skybox, so including one in the next version is a must. Ideally, the skybox would have the other stars in the database semi-visible in the right background location and you would be able to hover over them to see how far away they are and click to visit.

##### Procedural Planet Generation

In this version, planets are textureless green sphere, meh. If I had the time, I'd like to procedurally generate planetary textures based on some of the characteristics we have on the planet. Things like:
 - Is it a gas giant or a rocky world?
 - Is it covered in water?
 - Does it have a noticeable atmosphere?

##### Varying Orbital Planes

As we've discovered more and more planets, we've realized that there's nothing saying planets all have to be in roughly the same orbital plane. It turns out most planetary systems do have their planets in roughly the same plane, due to their formation in the proto-planetary disk. **But** some systems have been discovered with radically different orbital planes, so it would be cool to model this appropriately in the next version.

## Building XOPL

I used python to convert the NASA csv files (at the time this was all they had) and turn them into a JSON file with information about all the systems out there. Then I set up an Angularjs application that used a custom directive that could display Stellar Systems, and communicated between the app and this directive via a Service.