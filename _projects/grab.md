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
thumbnail: http://via.placeholder.com/200/
theatermode: true
game-include: grabgame.html
---
## Game
**W,A,D** To Move Forward and Steer. Pick up the blue orbs, but **avoid** the red ones!

## Info

GRAB is my entry for the 2013 JS1K contest. It is a prototype for a complete game I'm currently working on that is built in under 1KB or 1024 Bytes.

You control a brave, little, glowing arrow and your mission is to gather up as many resources (glowing orbs) as possible. BUT every resource you pick up also spawns an enemy mine that drifts towards you at a speed inversely proportional to your distance from it. Weave your way in and out of the enemies that begin to clog the screen and rack up as many points as you can.

This was probably the most fun I've ever had writing several lines of code. After completion I feel like I almost know what it must have been like to program games when every single bit of code and memory counted. Imposing such strict limits on what you can do is actually a liberating experience; one that lets you work fully inside a defined space as opposed to an infinite one in which you bumble about.

## Source Code

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