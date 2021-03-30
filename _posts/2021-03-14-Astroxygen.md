---
layout: post
categories: unity3d
comments: True
title: Unity3D - Astroxygen
published: True
description: My first Unity3D project.
---

<div align="center"><img src="../../../../assets/images/astroxygen_bg.png" alt="" width="700" />
</div>
<center>
  <p style="font-size:80%;">
Figure 1. Astroxygen.
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

# 0. Background

This blog finally has something related to video games. [Astroxygen](https://github.com/2ez4ai/Astroxygen) is my first Unity3D project after attending like three courses of Unity3D. This game is generally based on the *perfect match* map of **Fall Guys: Ultimate Knockout**, as I find the models of that are friendly given my poor modeling skills. Also, it innately allows me to personalize, to some extent, my game by using a different figure set rather than fruits. To complete the game flow, unlike *perfect match* that has fixed rounds, I set the goal for the player as collecting enough oxygen cylinder.

<div align="center"><img src="../../../../assets/images/fallguys_pm.png" alt="" width="450" />
</div>

<center>
  <p style="font-size:80%;">
Figure 2. The perfect match map of FullGuys.
  </p>
</center>

# 1. Components

The scene includes two main components: 
-	a screen to display the target figure and other information; 
-	a platform consisted of 16 tiles allowing players to stand on.

To make the falling reasonable, I use a picture of space as the background. For the choice of CSGO items, that was my very original idea since they are fascinating and highly distinguishable.

# 2. Mechanism

Actually, it occurred to me quite late that listing a time table for all scripts can relieve me a lot when doing such a turn-based game (at the start of the project, I dived into each logic independently, and very often got stuck with their inconsistent logic). In each round, the game proceeds as follows:
- -1.5s ~ 0.0s, ready for start;
- 0.0s ~ 5.0s, reveal some tiles randomly for memorisation;
- 5.0s ~ 10.0s, reveal some tiles randomly for memorisation; start counting down;
- 10.s ~ 15.0s, cover all tiles; generate oxygen tanks randomly;
- 15.0s ~ 17.5s, disable moving ability of all players; reveal all tiles to show the answer;
- 17.5s ~ 20.0s, disable tiles that have wrong figures;
- 20.0s ~ , reset timer, tiles state, player’s moving ability;

Now I would like to summarize the detailed mechanism of each object.

**FallGuys**: it is controlled by player via `CharacterController`. To avoid jumping over others’ head, which would stack fallguys,  I add an invisiable high cylinder for each of them.

**Computers**: to make it of great diversity, I created some materials for skins and outfits from which it choices randomly at the start of the game, and its action and memory are actually done by a lot of `Random.RandomRange()`. It does work. I mean, they look like smart and fun enough XD. The move is done by `move()` of `CharacterController`, where I set the horizontal/vertical input manually according to their position. I intended to implement the move by `NavMeshAgent`, but failed to make it due to the platform I implemented is not static.

<div align="center"><img src="../../../../assets/images/astroxygen_computers.png" alt="" width="1000" />
</div>

<center>
  <p style="font-size:80%;">
Figure 3. The computers can arrive right tiles, as well as the wrong ones (the green computer standing on the tile with a glove figure, which is different from the one in the screen).
  </p>
</center>
**Oxygen**: they are created randomly in the 10th seconds of each round. The main logic is done by in `OnTriggerEnter()`. I also add floating effect for them by changing the `transform.position.y`, which is also applied to the green indicator sign.

<div align="center"><img src="../../../../assets/images/astroxygen_oxygen.png" alt="" width="1000" />
</div>

<center>
  <p style="font-size:80%;">
Figure 4. The player is trying to get access to the oxygen cylinder. The screen shows that it still needs to collect 4 more oxygen cylinders.
  </p>
</center>
**Platform**: the removing of tiles makes the platform can not be static. The reveal and covering are all done by changing the corresponding material. It is quite easy.

**Screen**: like platform, its function mostly is done by changing materials.

**SphereBlock**: though they look gigantic, they are generally harmless, as they are floating quite high above players. The only reason I added this is that this project asks us to use `NavMeshAgent`. And yes, this is done with `NavMeshAgent`.

# 3. Conclusion

This project reminds me of the days when I enjoyed the scenario editors of *Age of Empires II* and *Warcraft 3*. But at that time I was like 15 years old, and actually did not make a thing. As for my first project and given such a short time, I think this project is of a high degree of completeness. The main drawback, for me, is the code construction is messy due to my lacking in the game logic in the early stage.
