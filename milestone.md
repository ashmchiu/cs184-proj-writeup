---
layout: page
title: 'Milestone'
has_right_toc: true
usemathjax: true
nav_order : 1
---
<h2><strong>Honey, I Upped the Viscosity! 🍯</strong></h2>
<i>Team Members: Ashley Chiu, Emmanuel Duarte, Dana Feng, Raymond Tan</i> | [Slides](https://docs.google.com/presentation/d/1XChTjyzATtKneU5rBeOULRzXM5DbCcm-AcWQce74FTo/edit#slide=id.p) | [Video](https://youtu.be/3IcuNlEuynY)

## What We've Accomplished
<img src="../assets/milestone/adhesion.png" width="25%" align="right" />

Building a **particle model** based on Homework 4's `PointMass` class, we constructed a scene with a sphere of `PointMass`es hovering over a `Sphere` `CollisionObject`. Then, simulating fluid dynamics referencing [Modeling and Rendering Viscous Liquids](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=bdbe45284686a54f3284fdf98759f099e3a95e84), we implemented 
- **liquid-solid interactions** so honey sticks to the sphere
- **liquid-liquid interactions** for viscous honey particles 

At first, our simulations were effectively unrunnable (buffering at every frame). We utilized spatial hashing for neighbor particle searching and incorporated **OpenMP parallelization** to fix this. Parallelizing neighbor search and particle-sphere collision at every timestep had the most impact.

## Preliminary Results
<div align="center">
    <img src="../assets/milestone/milestone_update.gif" width="30%"/>
</div>

90 frames/second, 30 steps/frame, 20,000 particles. A higher resolution version is on [YouTube](https://youtu.be/XzGDkuJSUBg).

## Reflections
In our current simulations, we like that the particles are attracted to the sphere, wrapping around rather than falling straight down. However, we'd like to fix a few things in **particle movements**:
- **volume preservation**: preserve density across honey particles. The particles are treated discretely so there's a 2D-ification as it pools flatly on the plane, when the honey should coil.
- **snail trail**: particles should mushroom out before colliding with the sphere ([reference](/assets/proposal/honey_on_sphere.png)), but they immediately hit the sphere unnaturely with a few sparse particles trickling down.

We want to focus more time on making more realistic viscosity models than originally intended so we'll only drip honey on the sphere since it demonstrates honey-solid adhesion well. Our main remaining goals are
- tune particle movements and volume preservation 
- Create meshes **using [marching cubes](https://www.cs.toronto.edu/~jacobson/seminar/lorenson-and-cline-1987.pdf)** and port meshes out of `Clothsim` into Blender
- Replicate visual experience of honey (lighting, shadows, environment refraction)

## Updated Work Plan
- **Week 2 (4/14-4/20)**: Tweak adhesion and viscosity values to be more realistic, implement volume preservation. Complete marching cubes and capture meshes at different timesteps. 
- **Week 3 (4/21-4/28)**: Parse produced `.obj` files from marching cubes through [Stop-motion-OBJ](https://github.com/neverhood311/Stop-motion-OBJ). Import mesh sequence into Blender, add BSDF for honey.
- **Week 4 (4/28 - 5/4)**: Ray trace shadows. Refract environment through honey (stretch goal). 