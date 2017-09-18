---
title: About Me
subtitle: Commander of the Armies of the North...
layout: project
logo_color: "#1863e6"
languages:
    - python
    - javascript
    - typescript
    - c#
    - c++
    - go
    - sass
---

I'm Derek and I do Software Development. I primarily work with web technologies, building Single Page Applications with Angular on the frontend and Python or node on the backend. I love programming of all kinds, but I'm usually most interested in Web Development, Game Development, Artificial Intelligence, and Reverse Engineering binary stuff!

### How I Got Into Programming

I first got interested in coding when I was 12 thanks to an online game called **Neopets** that let you customize your pet's pages with HTML & CSS. Then I started getting into programming maybe a year or two later due to another game, **RuneScape**. This time around my friends and I would program little macro GUIs so we could spam our messages in chat

<blockquote class="blockquote">
    Selling Rune Scimmy! 30k
    <footer class="blockquote-footer">
        <cite title="">1mju574n00b</cite>
    </footer>
</blockquote>

### Hobbies

 - Video Games (Halo for consoles, and PC for everything else)
 - Skateboarding
 - Snowboarding
 - Poker (No Limit Texas Hold Em & Pot Limit Omaha)
 - Weightlifting & Powerlifting

### Favorite Programming Languages

<ul>
{% for lang in page.languages %}
<li>{{lang}}</li>
{% endfor%}
</ul>