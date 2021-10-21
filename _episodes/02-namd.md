---
title: "Using Nanoscale Molecular Dynamics (NAMD) on WVU HPC resources"
teaching: 0
exercises: 0
questions:
- "How do I transfer my files to the HPC?"
- "How do I run NAMD on the cluster?"
- "How do I check if my job has failed?
objectives:
- "Learn how to tranfer files"
- "Learn which queues to use"
- "Learn how to submit a job"
- "Learn how to do some quick analysis on a simulation"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Visualizing the system

In the NAMD tutorial, you are instructed on creating a system of ubiquitin in water to simulate. For brevity, we will use the pregenerated files in the `1-1-build/example-output/` directory. Copy `ubq_wb.psf` and `ubq_wb.pdb` to the `common` directory. 

Open VMD and load `ubq_wb.psf` and `ubq_wb.pdb` by going to File>New Molecule. You should see something similar to the image below:

![A figure showing the initial coordinates of ubiqitin in a water box.](../fig/starting_namd.png)

I changed the representation for the protein to New Cartoon so that it is more visible.

In the `1-3-box` directory, there is a NAMD configuration file, `ubq_wb_eq.conf`, that is set to run an equilibration of ubiquitin in water. This is the .conf that we will be running on Thorny Flat.

## Transferring files to the HPC





## Connecting to the cluster

## Moving around with the command line

## Making a pbs script and submitting a job

## Checking jobs, benchmarking, and output files

## Visualizing and quick analysis of the trajectory


{% include links.md %}
