---
layout: post
categories: unity3d
comments: True
title: Unity3D - GoldSeeker
published: True
description: My second Unity3D project.
---

<div align="center"><img src="../../../../assets/images/goldseeker_init.png" alt="" width="700" />
</div>
<center>
  <p style="font-size:80%;">
Figure 1. GoldSeeker.
  </p>
</center>

{% include youtubePlayer.html id="TNMTLX0pcEY" %}
<center>
  <p style="font-size:80%;">
Video 1. Demo video.
  </p>
</center>

# 0. Introduction

The flow of this game ([source](https://github.com/2ez4ai/GoldSeeker)) is to collect 10 gold items, *i.e.,* coins. Some coins can be obtained directly on the map. The others can only be obtained from the creatures.

Compared with my first game [Astroxygen](https://2ez4ai.github.io/2021/03/14/Astroxygen/) is my first game, this one is far less interesting. The story and flow is not completed. It seems like I just put all those new things I learnt together in a brute, straightforward and no surprise way. But still, I gained lots of experience related to models, animations, *etc.* that the previous one failed to provide. 

# 1. Components

The scene includes four main components: 
-	a character controlled by a player;
-	four enemies;
-	two points for save & load;
-	quest components: coins and the light indicating the quest done;

Unlike the previous one, this time I used sophisticated models rather than simple cubes or spheres or capsules. The models I got mainly from [mixamo](http://mixamo.com/) and [sketchfab](https://sketchfab.com/3d-models). By the way, the audio is from [Dota2]([https://dota2.fandom.com/wiki/Category:Audio]).

Actually, at the beginning I tried to make a Chinese style combat game. But when I skimmed the two fancy websites, I found there is little Chinese models. Those closest ones often turn out to be Japanese. That was the first time that I glimpsed the scale of the gap between the two industries. And I believe that one day, games adapted from our Chinese stories can be all the rage.

# 2. Mechanism

Though this game is far more naiver than the previous one, the logic parts are much more complicated. The following content may be confusing if I use wrong gaming parlance.

**Main Character**: it is controlled by a player via `CharacterController`. The new feature here is that the control now supports both **keyboard** and **controller**, and we have animations for our character, which is supported with **blend tree**. Besides, we now have HP and furor (mana), which makes it formal.

**Third Person Camera**: the control for the main character would also affect the **camera** since they are grouped. More over, it also supports an independently way to control the camera, by using the right click of a mouse (the right joystick of a controller) as the input of the camera's rotation. I also implemented a naive **lock-on** mechanic. I made it by adding the move input of the player as a factor to the rotation input of the camera, because I want a smooth lock-on rather than in a brutal way.

**Enemies**: they now three status: idle, patrol, and attack. All the move related logic is done with `NavMeshAgent`. I also added an **aggro** mechanic for the enemies. Actually, I think the only tricky part lies in the synchronization between the logic and the animation. Maybe I should use `rayCast` to detect the timing.

**Skills** (attack): in fact, the normal attack for the main character is like shooting. It generates a prefab with `rigidBody` then we adds a velocity to it and make damage when the `OnTriggerEnter` happens. The special attack, sequentially generating nine swords circle the target and then converge, is quite similar but different in prefabs: more lights, more awesome, I assume.

**Save & Load**: this is a fancy function. I used `GameManager` for this. However, given those remarkable skills, like the *Recall* of *Tracer* in OverWatch and *Time Lapse* of *Weaver* in Dota2, I think there is more can be done with this function.

# 3. Conclusion

So this is my second project. I spent a lot of time in selecting models and setting animations. Sometimes I felt like I am a director, with all the materials for a movie. However, I was too stick to models and animations to focus on the gameplay. What makes it worse is that the effect is not attracting at all. But still, I learnt much from this project. I now have the basic ability to make a complete and standard game. Next time I will try harder on gameplay and visual effects to improve the player experience.
