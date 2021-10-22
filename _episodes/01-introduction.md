---
title: "Introduction: Basic introduction to MD"
teaching: 15
exercises: 0
questions:
- "What is Molecular-Dynamics ?"
objectives:
- "Gain a basic understanding of Molcualr dyanmics "
keypoints:
- "bad systems into the engeine give bad data out"
- "For every step of the system the total ponteial energy is found that is the sum of the forces on each atom"
---

{% include links.md %}

## Introduction to Molecular Dynamcis 
There is not enough time to teach all or really any of the complex topics of molecular dynamics, and this tutorial is not focused on the theory of MD. Rather, this tutorial is aimed toward using HPC resources to run MD simulation. Molecular Dynamics is a classical dynamics approach to molecular simulation, which for systems of many atoms it is fair to say the system would behave classically. All MD simulations need a set of initial conditions, in most cases this is the starting positions of the atoms. This begin said if **The starting structure is garbage ,the simulation will continue using the bad stutruce. This will produce bad results for the system you aaare studying.**  It is important to become well versed in your system and take time to make sure everything looks good. 

### MD forcefeild's and Newtons second law 

<img src="https://cdn.kastatic.org/googleusercontent/2br46h98qSJTx_9H-OSeJkuSVFYw9zoP-YQq4jEskl9WqewpP7Ork5fI2hRYv5OeWPeI-sieTItqAQT3w1VgR2c">

The equation above is a rearranged portion of the second law. Take note that the force and the acceleration are both vectors of the coordinate system. The total force in MD is the sum of forces of all the atoms. Inorder to find the force the engines have a set equation called a force field. 

we are using the CHARMM force feild as an example 

The pontentail energy of the system is given 

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/1e5005f6ff57075c4a7eb71aed12de5bf5a30def">

<img src="https://www.researchgate.net/profile/Emal-Alekozai/publication/280664616/figure/fig16/AS:648243079831554@1531564602615/Schematic-illustration-of-the-bonded-terms-in-the-CHARMM-force-field-adapted-from.png">

The total force which relates to the total energy of the system is just the change in the potential energy in each one of the components of the system

## Dynamical constraints 

Simulations need a set of assumption inorder to dictate the atoms behavior 
- Microcanonical ensemble (NVE): constant number of atoms , constant volume and constant energy. Best for collecting data that is sensitive to temperature or pressure.
- Canonical ensemble (NVT):  constant number of atoms , constant volume and constant temperature. This type of simulation allows the system density to be uniform.
-  Isothermal–isobaric ensemble (NTP):  constant number of atoms , constant volume and constant temperature. These condition are the conditions that often relate the most to laboratory conditions 

