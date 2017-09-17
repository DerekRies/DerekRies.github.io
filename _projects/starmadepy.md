---
title: "Starmadepy"
subtitle: "Reading & Writing Starmade Files with Python"
layout: project
technologies:
    - Python
    - Binary/Hex
    - Reverse Engineering
quickdesc: Starmadepy is a simple python library that makes parsing and manipulating Starmade game data easy. As this project is fairly new, the only file type that is currently supported is the .smtpl, or Starmade Template file type.
github: https://github.com/DerekRies/starmadepy
priority: 3
thumbnail: imgs/starmadethumb.png
---

<div class="text-center big-figure">
    <figure class="figure">
        <img src="{{site.url}}/imgs/starmadepy-banner.jpg">
        <figcaption class="figure-caption text-center">The PC Game Starmade</figcaption>
    </figure>
    <a href="{{page.github}}" class="btn btn-lg btn-secondary"><i class="fa fa-github"></i> View On Github</a>
    <a href="http://starmadepy.readthedocs.io/en/latest/" class="btn btn-lg btn-secondary"><i class="fa fa-book"></i> Read the Docs</a>
</div>

## Overview

Starmadepy is a simple python library that makes parsing and manipulating Starmade game data easy. The only file type that is currently supported is the `.smtpl`, or Starmade Template file type. This library allows you to read and write starmade files, and make all sorts of programmatic modifications to them. Read on to see some examples of it's usage.

For this project I had to reverse engineer the file formats and then build out the Serialization/Deserialization in Python. 

## Explaining Starmade

Starmade is a block building game a lot like Minecraft, only it's in Space! Players often build Sci-Fi like Spaceships and Space Stations. In the process of building these creations, players may find themselves repeatedly building some of the same structures over and over. To solve this problem, Starmade allows for the creation and usage of **Templates**. Templates are just configurations of blocks that can be reused in many places; Starmade saves these templates as `.smtpl` files. (They also contain some information about Logic Circuitry that may be included but for the sake of this article I'll ignore it)

One of the drawbacks of those templates, was that they just stored configurations of blocks, and those blocks had a color associated with them. This meant if you wanted different color components you had to make a new template for each and every color you wanted. This was **extremely tedious** in game. That's where Starmadepy could come in!

## Using Starmadepy

With starmadepy you could write a python script that handled generating all of the desired color variations out of a single template file! Let's take a look at an example.

##### Changing a Template's Color with Starmadepy

In this example we're going to have a little gray compnent stored in a template file called `sometemplatefile.smtpl`, and we're going to try and generate an orange version of it and save it as `outtemplatefile.smtpl`

```python
from starmadepy import starmade

template = starmade.Template.fromSMTPL('sometemplatefile.smtpl')
template.replace({'color': 'grey'}, {'color': 'orange'})
template.save('outtemplatefile.smtpl')
```

This would give us the following result:

<div>
    <figure class="figure">
        <img src="https://github.com/DerekRies/starmadepy/raw/master/docs/img/tutorial1.png">
        <figcaption class="figure-caption">An orange version of the original template has been generated with starmadepy</figcaption>
    </figure>
</div>
