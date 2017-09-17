---
title: "GRAB"
subtitle: "A Game in under <1024 Bytes"
layout: project
technologies:
  - Javascript
  - Closure Compiler
  - GameDev
quickdesc: GRAB is my entry for the 2013 JS1k Contest, where all entries must be under 1024 Bytes (1KB). It's a game where you control a little glowing arrow, and have to pick up the glowing orbs of your color while avoiding the bad ones.
priority: 3
thumbnail: imgs/grabthumb.jpg
theatermode: true
game-include: grabgame.html
---
<div class="figure-caption text-center">
  <strong>W,A,D</strong> To Move Forward and Steer. Pick up the blue orbs, but <strong>avoid</strong> the red ones!
</div>
## Info

GRAB is my entry for the 2013 JS1K contest. It is a prototype for a complete game I'm currently working on that is built in under 1KB or 1024 Bytes.

You control a brave, little, glowing arrow and your mission is to gather up as many resources (glowing orbs) as possible. BUT every resource you pick up also spawns an enemy mine that drifts towards you at a speed inversely proportional to your distance from it. Weave your way in and out of the enemies that begin to clog the screen and rack up as many points as you can.

This was probably the most fun I've ever had writing several lines of code. After completion I feel like I almost know what it must have been like to program games when every single bit of code and memory counted. Imposing such strict limits on what you can do is actually a liberating experience; one that lets you work fully inside a defined space as opposed to an infinite one in which you bumble about.

<h2>Techniques<br><small class="text-muted">For keeping everything under 1KB</small></h2>

There were a few techniques I learned after working on this project that helped me to achieve the tiny file size.

#### Find a Good Compiler/Minifier

If you aren't using a compiler/minifier for JS1k the competition is a bit over before it even begins. Trying to write code and maintain it without good variable names and a nice visual hierarchy is going to be a nightmare. So for this project I used the Google Closure Compiler which got me like 60% of the way to 1KB from my original source code.

#### Turn your code into a string and eval!

<blockquote class="blockquote border-warning blockquote-tiny"><strong>Don't do this for normal code.</strong> This is for code golf / hacky purposes.</blockquote>

If you find yourself repeating a lot of the same function calls with the same parameters, say for example repeatedly calling `addEventListener('keyDown')` and `addEventListener('keyUp')`, you may be able to save some space with this method. Essentially you are turning your source code into a string and replacing those long function calls (or w/e else) with a single symbol. Then use regex on the string to replace those symbols with the original code, and eval the result. I was able to get a decent savings out of replacing the following:
  - `b.addEventListener("key`
  - `function `
  - `600*M.random()|0`

#### Sometimes less is more (literally)

The final trick or technique I utilized for this project was simply to rethink what I was trying accomplish. We don't often need all of the stuff we write. Throughout a project like this you should be thinking, *"What can I remove from this?"* far more often than *"What can I add?"*. 

In GRAB one of the easiest examples I can remember of this, had to do with how I was clearing the canvas and then repainting everything. In the original version, I had a white background and every frame i was clearing the canvas and drawing everything back to the screen. Then I realized I could get rid of the canvas clear and just use the canvas fill method that I was already using. Only now I made it black and gave it an alpha value. This meant every frame had a bit of a ghost from the previous frames. In the end I saved some bytes and gained a visual feature that I really liked!


## Source Code

Here's the final code for the JS1k 2013 Submissions. Unfortunately I don't have the original unobfuscated source code anymore.

{% highlight html %}

<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>JS1k, 1k - Coin Grab</title>
    <meta charset="utf-8">
  </head>
  <body>
    <canvas id="c"></canvas>
    <script>
      var b = document.body;
      var c = document.getElementsByTagName('canvas')[0];
      var a = c.getContext('2d');
      document.body.clientWidth; // fix bug in webkit: http://qfox.nl/weblog/218
    </script>
    <script>
      eval('c.width=c.height=600;a.fillStyle="rgba(0,0,0,.3)";var e,f,h,j,k,l,m,p,q,r,s,t;w="strokeStyle";M=Math;W="#0AF";_y(){l=!0;j=`;k=`;p=m=300;r=q=0;s=-1.57;t=[]}_z(d){a.lineWidth=6;a[w]=d;a.stroke();a.lineWidth=2;a[w]="#FFF";a.stroke();a.beginPath();}y();setInterval(_(){a.fillRect(0,0,600,600);if(l){e&&(q+=0.5*M.cos(s),r+=0.5*M.sin(s));f&&(s-=0.05);h&&(s+=0.05);20>M.abs(m-j)&&20>M.abs(p-k)&&(j=`,k=`,t.push(`,`));m+=q;p+=r;q*=0.9;r*=0.9;a.translate(m,p);a.rotate(s+1.57);a.beginPath();a.moveTo(-10,10);a.lineTo(0,-15);a.lineTo(10,10);z(W);a.setTransform(1,0,0,1,0,0);a.arc(j,k,10,0,2*M.PI);z(W);for(i=0;i<t.length;i+=2){d=m-t[i],v=p-t[i+1],x=M.sqrt(d*d+v*v);20>x&&y();d=M.atan2(v,d);t[i]+=50*M.cos(d)/x;t[i+1]+=50*M.sin(d)/x;a.arc(t[i],t[i+1],10,0,2*M.PI);z("#F00")}}},16)~down",_(d){o=d.keyCode;87==o&&(e=!0);68==o&&(h=!0);65==o&&(f=!0)})~up",_(d){o=d.keyCode;87==o&&(e=!1);68==o&&(h=!1);65==o&&(f=!1)});'.replace(/_/g,'function ').replace(/~/g,';b.addEventListener("key').replace(/`/g,'600*M.random()|0'));
    </script>
  </body>
</html>
{% endhighlight%}
