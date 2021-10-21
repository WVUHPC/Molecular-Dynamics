---
title: "Introduction: History, basics and overview of major codes."
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

{% include links.md %}

## Introduction to Molecular Dynamcis 
There is not enough time to teach all or really any of the complex topics of molecular dynamics, and this tutorial is not focused on the theory of MD. Rather, this tutorial is aimed toward using HPC resources to run MD simulation. Molecular Dynamics is a classical dynamics approach to molecular simulation, which for systems of many atoms the assumption is valid. All MD simulations need a set of initial conditions, in most cases this is the starting positions of the atoms. This begin said if **The starting structure is garbage ,the simulation will continue using the bad stutruce giving poor results.**  It is important to become well versed in your system and take time to make sure everything looks good. 

### MD forcefeild's and Newtons second law 
From newtons second we know that:

<img src="https://cdn.kastatic.org/googleusercontent/2br46h98qSJTx_9H-OSeJkuSVFYw9zoP-YQq4jEskl9WqewpP7Ork5fI2hRYv5OeWPeI-sieTItqAQT3w1VgR2c">

The equation above is a rearranged portion of the second law. Take note that the force and the acceleration are both vectors of the coordinate system. The total force in MD is the sum of forces of all the atoms. Inorder to find the force the engines have a set equation called a force field. 

#### Charmm force feild 

The pontentail energy of the system is given 

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/1e5005f6ff57075c4a7eb71aed12de5bf5a30def">

<img src="https://www.researchgate.net/profile/Emal-Alekozai/publication/280664616/figure/fig16/AS:648243079831554@1531564602615/Schematic-illustration-of-the-bonded-terms-in-the-CHARMM-force-field-adapted-from.png">

This can be used with some fancy calacus to find the force on each atom’s interaction with all the atoms in the system. The sum of which is the total force/energy of the system.

## Dynamical constraint 

Simulations need a set of assumption inorder to dictate the atoms behavior 
- Microcanonical ensemble (NVE): constant number of atoms , constant volume and constant energy. Best for collecting data that is sensitive to temperature or pressure.
- Canonical ensemble (NVT):  constant number of atoms , constant volume and constant temperature. This type of simulation allows the system density to be uniform.
-  Isothermal–isobaric ensemble (NTP):  constant number of atoms , constant volume and constant temperature. These condition are the conditions that often relate the most to laboratory conditions 

# The history Of the Codes

## NAMD 
