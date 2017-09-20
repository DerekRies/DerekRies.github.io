---
title: "Arkpy"
subtitle: "A Python Library for Reading & Writing Ark Files"
layout: project
quickdesc: "ARKpy is a library for reading and writing the file formats of ARK: Survival Evolved with Python. ARKpy does not simply look for the offsets of particular strings to find the data (like other existing libraries/scripts), but implements the complete file protocol that reads the entire data structure of the file into memory."
technologies:
    - Python
    - Binary / Hex
    - Reverse Engineering
github: https://github.com/DerekRies/arkpy
priority: 2
thumbnail: 'imgs/arkthumb.png'
---

<div class="text-center big-figure">
    <figure class="figure">
        <img src="https://cloud.githubusercontent.com/assets/1471991/17155479/1b5b27a6-533a-11e6-84bd-439626d98a67.jpg">
        <figcaption class="figure-caption text-center">The PlayerCharacter's skin has been edited beyond what is capable in-game, by changing the .arkprofile file</figcaption>
        <!-- <img src="https://i.ytimg.com/vi/5fIAPcVdZO8/maxresdefault.jpg"> -->
        <!-- <figcaption class="figure-caption text-center">Players ride their Dinosaurs into combat! Ark: Survival Evolved is an action-adventure survival video game developed by Studio Wildcard.</figcaption> -->
    </figure>
    <a href="{{page.github}}" class="btn btn-lg btn-primary"><i class="fa fa-github"></i> View on Github</a>
    <a href="http://arkpy.readthedocs.io/en/latest/" class="btn btn-lg btn-secondary"><i class="fa fa-book"></i> Read the Docs</a>
</div>
<!-- 
<div class="row">
    <div class="col-md-6 text-center big-figure">
        <figure class="figure">
            <img src="https://cloud.githubusercontent.com/assets/1471991/17155479/1b5b27a6-533a-11e6-84bd-439626d98a67.jpg">
            <figcaption class="figure-caption text-center">The PlayerCharacter's skin has been edited beyond what is capable in-game, by changing the .arkprofile file</figcaption>
        </figure>
    </div>
    <div class="col-md-6 text-center big-figure">
        <figure class="figure">
            <img src="https://cloud.githubusercontent.com/assets/1471991/17155479/1b5b27a6-533a-11e6-84bd-439626d98a67.jpg">
            <figcaption class="figure-caption text-center">The PlayerCharacter's skin has been edited beyond what is capable in-game, by changing the .arkprofile file</figcaption>
        </figure>
    </div>
</div> -->

## Overview

ARKpy is a library for reading and writing the file formats of ARK: Survival Evolved with Python. ARKpy does not simply look for the offsets of particular strings to find the data (like other existing libraries/scripts), but implements the complete file protocol that reads the entire data structure of the file into memory.

For those interested in the reverse engineering of the file types, the complete specifications can be found among the library docs [here](http://arkpy.readthedocs.io/en/latest/formats/). I also plan on writing a Blog post detailing my process of reverse engineering the formats, which I will include a link to in this page once it's finished.

<div class="text-center">
    <a href="http://arkpy.readthedocs.io/en/latest/formats/" class="btn btn-lg btn-secondary"><i class="fa fa-external-link"></i> File Format Specifications</a>
</div>


#### What's Ark: Survival Evolved?

Ark: Survival Evolved is a open-world, survival pvp game. Basically that means, you play as a character starting from scratch and will have to fight, build, and tame your way to primacy against (or in cooperation with) many other players. In Ark, players tame Dinosaurs, Form Tribes and Alliances, Build Strongholds, and Wage War all in a persistent world.

#### Where Does Arkpy Fit In?

Ark has a few file formats that are used to serialize game state, configurations, and other data. These include:
 - **`.arkcharactersetting`:** These files describe the templates, or saved presets, that you can choose to quickly create a character off of on the character creation screen. They are relatively simple and contain no compressed data.
 - **`.arkprofile`:** These files contain all the data relevant to the player character, apart from things handled at the world level like Inventory and Position.
 - **`.arktribe`:** These files contain data about a Tribe, which includes things like the Creator/Owner of the Tribe, it's members, and what alliances it may belong to. Also includes a limited chat log of in game messages sent to the Tribe Chat.
 - **`.ark`:** These files describe the state of the world (the server in question), and includes all of the existing entities and their positions. Things like player bodies, structures, tamed and untamed dinosaurs.

Arkpy provides support for reading all of these filetypes except the world `.ark` file.

<h4>Library Features <small class="text-muted">Beyond Reading/Writing</small></h4>
 - Create new characters or tribes dynamically
 - Friendly API Wrapper around the data
 - Maps to enumerate through and identify the proper indices for:
   - BoneModifierSlots (Head Size, Chest, etc..)
   - Body Colors (Skin, Hair, Eyes)
   - Stats (Health, Oxygen, Stamina, etc...)
   - Item Blueprint Paths/IDs

## Usage

##### Installation

```
pip install arkgamepy
```

##### Example

For the following example I'm going to try and read in my SinglePlayer Ark characters .arkprofile, and display some information about the character

```python
from arkpy.ark import ArkProfile
from arkpy.ark import BoneMap, StatMap, BodyColorMap

file_path = 'data/SavedArksLocal/LocalPlayer.arkprofile'
profile = ArkProfile(file_path)

print 'Character Name: %s' % profile.character.name
print 'Level: %s ' % 1 + profile.character.level_ups
print 'XP: %s' % profile.character.experience
print 'Engram Points: %s' % profile.character.engram_points

# Get all the allocated Stat points and print them
stats = profile.character.stat_points
for stat in StatMap:
    print '%s: %s' % (stat.name, stats[stat])

# Print all the bone modifier values, which are basically what the character looks like
bones = profile.character.body_modifiers
for bone in BoneMap:
    print '%s: %s' % (bone.name, bones[bone])

```