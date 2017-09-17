---
title: "Poker Client & Botfarm"
subtitle: "Farming Play Money Poker Chips"
layout: project
quickdesc: "For this project I targeted a popular play-money web application for No Limit Texas Hold Em, and developed a complete async network client for the game in python with asyncio. This includes an HTTP client for their REST(ish) internal API, as well as a fully functional websocket client for in game messages to automate collecting chips and playing tables."
technologies:
    - Python / AsyncIO
    - aiohttp
    - Websockets
    - Protocol Buffers
    - Angular
    - Redis
priority: 2
thumbnail: imgs/wsopthumb.png
---

<div class="text-center big-figure">
    <figure class="figure">
        <img src="{{site.url}}/imgs/pokerbanner.jpg">
        <figcaption class="figure-caption text-center">A Screenshot of the Play Money Poker WebApp Homepage with 23Billion chips</figcaption>
    </figure>
</div>

## Overview

{{page.quickdesc}}

In addition to the clients, the real fun part is in the scripts using those clients. I developed a taskrunner that continuously ran tasks that were scheduled every x minutes, which basically amounted to automatically collecting free chips on huge number of accounts in the botfarm. As well as a cli that provided me an administrative route to control all those bots.

<div class="alert alert-danger">Unfortunately I won't be sharing the source code for this project as it still contains sensitive information and could be used by others to further bot the website.</div>

This page will provide a general rundown of the project without any real concrete specifics, but if there's interest I may expand further on a few sections of the project in multiple blog posts.

##### Contents
 - [Goals](#goals)
 - [Components of this Project](#components-of-this-project)
    - [Client](#client)
        - [HTTP-Client](#http-client)
        - [Websocket-Client](#websocket-client)
    - [CLI](#cli)
    - [TaskRunner](#continuous-botfarm-taskrunner)
 - [Challenges](#challenges)
 - [Future Additions](#future-additions)
 - [Things They Could do to Catch Botting](#things-they-could-do-to-catch-botting)

<hr>

## Goals

##### Writing a Bot to Play Poker

As a huge fan of watching and playing poker, I initially wanted to try my hand at developing a poker bot. But before I could write a bot that could play poker well, I was going to have to write a bot that could play poker at all. By that I mean, I needed to find a platform to play on, a way to get info about the game state, and a way to send actions to the game. So for this project I decided I would build out an entire network client, rather than do something primitive and limited like screen scraping and sending click commands to the OS. 

##### Collecting a Whole Lot of Chips

Let's face it, having a ton of chips never hurt. The site that I played on offered free chips every few hours to accounts, as well as a few ways to get some additional free chips. So I figured why not have a bunch of accounts collect a bunch of chips, a botfarm.

<hr>

## Components of this Project

Because this project is so large in scope I'll provide a quick description of each component and then go into more detail for each one individually later:
 - **Client**
    - **HTTP Client**, used to interact with the primary functionality of the website.
    - **Websocket Client**, used at tables to actually player poker. (Receiving Game State and Sending Actions)
 - **CLI**, used to run specific commands on the website for individual accounts and botfarm administration
 - **Continuous Botfarm TaskRunner**

### Client

The reason why I chose to implement a complete Network Client, with all of it's added complexity was simply because a screen scraping and clicking method would be far too limited. Limited in the sense that I could only run a few bots at any one time with a method like that because I'm limited by what fits on the screen. It would also be really brittle as it would either rely on computer vision and be fairly slow for multiple clients, or hardcoded pixel offsets to find information.

Let's take a look at the Web Client in the browser before we look at my client.

<!-- ![Alt Text]({{site.url}}/imgs/poker-site-network-graph.png) -->

<div class="text-center">
    <figure class="figure">
        <img src="{{site.url}}/imgs/poker-site-network-graph.png">
        <figcaption class="figure-caption text-center">A Clients Web Browser sends HTTP Requests to the site, which hands to a game server for a websocket connection.</figcaption>
    </figure>
</div>

In the above diagram, a client (in this case, a web browser) sends HTTP Requests to the site and site lets the client establish a websocket connection with one of the game servers. In this case the Poker Site handles most stuff like querying data through a REST(ish) interface and the Game Servers handle all the game-related processing like assigning tables and managing hands being played at any one given table.

##### HTTP Client

The HTTP Client handles a large portion of the functionality that the website provides, namely:
 - Authentication
 - Establishing a Game Server (Casino ID)
 - Sending / Accepting Friend Requests
 - Sending / Collecting Chip Gifts Between Friends
 - Looking up stats for a given player id
 - Redeeming Promo Codes
 - Collecting Hourly Chip Bonuses
 - Spinning the Mega Bonus Wheel
 - Spinning the Slot Machines
 - Joining a Friend's Casino

 Basically everything that isn't directly related to a hand of actual poker being played.

##### Websocket Client

Once an HTTP client logs in to the site and establishes which Game Server (Casino) it's going to be using, then the websocket connection is opened with that game server and the websocket client sends an authentication message with the token that the HTTP client was given. In order for me to develop this websocket client i had to first discover how the websocket messages were structured, and what kind of encryption or encoding they might be using. 

<div class="text-center">
    <figure class="figure">
        <img src="{{site.url}}/imgs/poker-site-ws-log.png">
        <figcaption class="figure-caption text-center">The websocket messages being sent and received through Chrome Dev Tools Network Tab</figcaption>
    </figure>
</div>

After looking at a few of the messages being sent ending with the = sign I figured the messages were probably being Base64 Encoded. After decoding them with Base 64 they still looked like gibberish, so I went into the obfuscated code in the web app and after some looking around I found a protocol buffers definition. I cleaned up the .json file inside the obfuscated code with the protocol buffers definitions in them and compiled my own python library from those definitons with the Protobuf Compiler.

With the Base 64 decoded string I then tried to use the protobuf generated python to `parseFromString` and it worked! **Success!** Now I was able to send and receive valid messages to the poker app. As an example a ping message in the application would look like this in `.proto` form and its websocket message form.

```proto3
# proto3 file
message Ping {
    int32 pingId = 1;
}
```
```
# Websocket Message
oAYJSgMI40g=
```

### CLI

Using the Click python library I built out a CLI that utilized the Clients to automate some tasks with the parameters that I provided. This allowed me to easily handle any administrative duties I had to do on the botfarm, like:

 - Redeeming Promo Codes for a specific account or the whole botfarm
 - Sending / Accepting Friend Requests
 - Spinning the Slot Machine
 - Collecting Hourly Bonuses and Spinning the MegaBonus Wheel

<!-- 
<h5>Redeeming Promo Codes <small class="text-muted">for a specific account or the whole botfarm</small></h5>

##### Sending / Accepting Friend Requests

##### Spinning the Slot Machine

<h5>Collecting Hourly Bonuses <small class="text-muted">(And Spinning the Wheel)</small></h5> -->


### Continuous Botfarm TaskRunner

Finally, I wrote a simple python script that continuously runs, and executes a scheduled task every n minutes that it was scheduled to run for. Basically, I've got a a few main tasks:
 - **Send Chip Gifts** from every account to every other account (once a day)
 - **Collect Chip Gifts** on every account (once a day)
 - **Collect Hourly Bonuses** if any accounts are eligible to collect. (every 5 minutes)
 - **Sample Active Users:** Checks the current number of online users and adds it to the database (every 5 minutes)
 - **Update Stats** for the botfarm (every 30 minutes)

<hr>

## Future Additions

Here are some of my ideas for future additions to the project:

##### Colluding Bots (No Limit Hold Em or Pot Limit Omaha)

In Pot Limit Omaha each player gets 4 hole cards. That means with 3 bots at the table I could know up to 18 cards in the deck, which makes the probability calculations alone much more certain. (4*3 = 12 hole cards + 5 Community Cards). Would be cool to develop a strategy for colluding bots that could work together to extract maximal value out of opponents.

##### Actual Poker AI Bot

Now that I've got all the infrastructure built out, I'd like to go back to that original goal of developing a bot that can play poker well.

##### Angular Dashboard

Having a way of viewing the status of the bots, scheduling tasks, and running commands all from a web browser would be ideal so I could manage the botfarm without having to go to the cli.

<hr>


## Things They Could do to Catch Botting

Assuming they even care to catch botters, there's a few things they could do to stop botting/cheating.

##### The Super Easy Basic Stuff
 - Prevent multiple accounts with the same I.P. from joining the same table.
 - Monitor the number of hands played per minute at a table. Tables with really high hands per minute (like above 2) probably have some shady stuff happening at them, like collusion or botting.

##### Slightly More Work
 - Pattern Detection
 - Network Analysis, for finding out which accounts play with each other and send chips to each other frequently.
 - Additional Network Analysis, could use a directed graph to see how many chips are flowing between accounts to identify chip dumpers and chip collectors.