---
layout: post
categories: unity3d
comments: True
title: Unity3D - GoldSeeker
published: False
description: My second Unity3D project.
---

<div align="center"><img src="../../../../assets/images/goldseeker_init.png" alt="" width="700" />
</div>
<center>
  <p style="font-size:80%;">
Figure 1. GoldSeeker.
  </p>
</center>

<div align="center">
<video width="700" controls="controls">
	<source src="../../../../assets/videos/astroxygen_recording.mp4"  type="video/mp4" />
</video>
</div>
<center>
  <p style="font-size:80%;">
Video 1. Demo video.
  </p>
</center>

# 0. Introduction

The flow of this game ([source](https://github.com/2ez4ai/GoldSeeker)) is to collect 10 gold items, *i.e.,* coins. Some coins can be obtained directly on the map. The others can only be obtained from the creatures.

Compared with my first game [Astroxygen](https://2ez4ai.github.io/2021/03/14/Astroxygen/) is my first game, this one is far less interesting. The story and flow is not completed. It seems like I just put all those new things I learnt together in a brute, straightfoward and no surprise way. But still, I gained lots of experience related to models, animations, *etc.* that the previous one failed to provide. 

# 1. Components

The scene includes four main components: 
-	a character controlled by a player;
-	four enemies;
-	two points for save & load;
-	quest components: coins and the light indicating the quest done;

Unlike the previous one, this time I used sophisticated models rather than simple cubes or spheres or capsules. The models I got mainly from [mixamo](http://mixamo.com/) and [sketchfab](https://sketchfab.com/3d-models). Actually, at the beginning I tried to make a Chinese style combat game. But when I skimmed the two fancy websites, I found there is little Chinese models. Those closest ones often turn out to be Japanese. That was the first time that I glimpsed the scale of the gap between the two industries. And I believe that one day, games adapted from our Chinese stories can be all the rage.

# 2. Mechanism

Though this game is far more naiver than the previous one, the logic parts are much more complicated.

**FallGuys**: it is controlled by player via `CharacterController`. To avoid jumping over others’ head, which would stack fallguys,  I add an invisiable high cylinder for each of them.

**Computers**: to make it of great diversity, I created some materials for skins and outfits from which it choices randomly at the start of the game, and its action and memory are actually done by a lot of `Random.RandomRange()`. It does work. I mean, they look like smart and fun enough XD. The move is done by `move()` of `CharacterController`, where I set the horizontal/vertical input manually according to their position. I intended to implement the move by `NavMeshAgent`, but failed to make it due to the platform I implemented is not static.

# 3. Conclusion

This project reminds me of the days when I enjoyed the scenario editors of *Age of Empires II* and *Warcraft 3*. But at that time I was like 15 years old, and actually did not make a thing. As for my first project and given such a short time, I think this project is of a high degree of completeness. The main drawback, for me, is the code construction is messy due to my lacking in the game logic in the early stage.
