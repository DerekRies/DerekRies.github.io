---
title: Talks
subtitle: and Presentations
layout: project
---

{% for talk in site.data.talks %}
<div class="post media">
    <img src="{{talk.thumbnail}}" alt="" class="d-flex rounded-circle">
    <div class="media-body">
        <h3 class="card-title">{{talk.title}} <small class="text-muted">{{talk.subtitle}}</small></h3>
        <p class="text-muted"><em>{{talk.date | date: '%B %d, %Y' }}</em></p>
        <p class="card-text">{{talk.summary}}</p>
        <a href="{{talk.video}}" class="btn btn-lg btn-primary"><i class="fa fa-tv"></i> Watch Talk</a>
        <a href="{{talk.slides}}" class="btn btn-lg btn-secondary">View Slides</a>
    </div>
</div>
{% endfor%}