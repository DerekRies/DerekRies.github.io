---
title: "Kanbanzilla"
subtitle: "A Bugzilla-Integrated Trello Clone for Mozilla"
layout: project
quickdesc: "My Internship project at Mozilla"
technologies:
    - Python / Flask
    - Angular
    - Bugzilla
priority: 2
thumbnail: imgs/kanbanzilladarkthumb.png
github: https://github.com/mozilla/kanbanzilla
extra-link: https://air.mozilla.org/intern-presentations-reis
extra-link-text: View Talk
---

<div class="text-center big-figure">
<figure class="figure">
    <!-- <a href="{{page.extra-link}}"> -->
        <img src="{{site.url}}/imgs/kanbanzilla-presentation.jpg" class="figure-img img-fluid">
    <!-- </a> -->
    <figcaption class="figure-caption text-center">My intern presentation at Mozilla viewable on <a href="{{page.extra-link}}">AirMozilla</a></figcaption>
</figure>
<a href="{{page.github}}" class="btn btn-lg btn-secondary"><i class="fa fa-github"></i> View Project on Github</a>
<a href="{{page.extra-link}}" class="btn btn-lg btn-secondary"><i class="fa fa-tv"></i> Watch Presentation (20mins)</a>
</div>

## What's Kanbanzilla?

During the Summer of 2013, I interned at Mozilla on the Web Dev (later split to Web Engineering) team. For my internship I worked on Kanbanzilla, an internal web app that provided a Kanban Interface on top of the old Bugzilla API. Essentially this meant a Trello Clone that would sync with Bugzilla. When someone moved a card on the kanban board, it would be updated with Bugzilla. At the time, Trello didn't have support for integrating with anything. Since 2013, Github Issues and Bitbucket (Jira) have added a Kanban Cards and Columns style view, very much like what Kanbanzilla did.

<div class="text-center big-figure">
    <figure class="figure">
        <img src="http://via.placeholder.com/650x400" alt="">
        <figcaption class="figure-caption text-center">A Screenshot of Kanbanzilla</figcaption>
    </figure>
</div>

## What's Bugzilla?

<blockquote class="blockquote border-primary">
Bugzilla is a "Defect Tracking System" or "Bug-Tracking System". Defect Tracking Systems allow individual or groups of developers to keep track of outstanding bugs in their products effectively.
<footer class="blockquote-footer"> from <a href="https://bugzilla.org/about"><cite title="About Bugzilla">Bugzilla.org</cite></a></footer>
</blockquote>

## Bugzilla as a Backend

Any user of Kanbanzilla would login using their Bugzilla credentials, and their boards would be loaded into the app according
to which projects they belonged to.

Kanbanzilla used the old Bugzilla API, before BzAPI (which is now deprecated as well), which meant a lot of functionality didn't exist. Boards in Kanbanzilla mapped to Projects in Bugzilla. Each of those projects could have many different statuses and bugs/issues could find themselves belonging to one, or more, or none of those statuses. Ideally we would map a Kanban Board to a project, the columns in the board to a Status in Bugzilla, and the cards in the columns to the bugs in the Bugzilla project. However, there were a few issues that complicated the matter a bit. 

Columns in Kanbanzilla would instead need to map to "virtual statuses". Virtual statuses were either statuses, or a composition of multiple statuses that bugs would often belong to. They could also be backed by *whiteboard data*. Whiteboard data was essentially just a big field for user data in the Bugzilla platform that ended up being used differently by every team.
