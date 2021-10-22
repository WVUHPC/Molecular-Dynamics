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
useMath: true
---

# Molecular Dynamics, historical perspective.

The ability to model the movement of particles and get results for system of practical importance comes from the convergence of at least three fronts.
First the physical theories for the forces and potentials. Mathematical elements to perform the physical equations in a efficient Algorithm and finally the computational capabilities that we have today to model large systems to a level in size and time of simulation that could offer meaningful answers for problems of practical interests. As we can see molecular dynamics is at the crossroad between the science: Physics and Chemistry, the mathematical size including numerical methods and algorithms and Hardware and Software developments.

The dynamics of particles in the form of equations date back from Newton Laws for the movement of celestial bodies. However at Newton times only two body interactions could be solved in close form. It was later known that we can not expect a similar solution for 3 bodies or more, the equations still relevant must be left to be numerically computed and only during the last few decades we have enough computational resources to put those equations to work for thousands and even millions of particles.

## The need for Molecular Dynamics

Molecular dynamics is there to fill the gap between the too few particles and the limit of infinite particles at equilibrium.
From one side there is no closed form for the general problem of 3 bodies. An equation is said to be a closed-form solution if it solves a given problem in terms of mathematical functions. For 3 or more particles the solution to the Newton's equations could result in a dynamical system that is chaotic for most initial conditions. Only numerical simulation can tackle the problem to some extend.

From the other side, statistical mechanics is very precise in predicting the global state of a system usually needs systems large enough an in equilibrium. Beyond those limits, finite systems or systems out of equilibrium only simulation can provide answers.

We know that the theory at atomic scale is quantum in nature. However, for many practical purposes treating the atoms as classical particles produces results that are in agreement with experiments. The atomic forces however comes not only from the charge of the nucleus but more importantly from the electrons and those must be treated with quantum mechanics.

## Varieties of Molecular dynamics approaches.

There are many approaches to Molecular dynamics. The first and probably most important choice is how the forces will be calculated.

You can compute forces just from tabulated equations for the different this is the approach with force fields.
A force field (FF) is a mathematical expression describing the dependence of the energy of a system on
the coordinates of its particles. It consists of an analytical form of the interatomic potential energy,

<div class="math">
\begin{equation}
U(r_1, r_2, \cdots , r_N )
\end{equation}
</div>

and a set of parameters entering into this form. The parameters are typically obtained
either from ab-initio or semi-empirical quantum mechanical calculations or by fitting to experimental
data such as neutron, X-ray and electron diffraction, NMR, infrared, Raman and neutron spectroscopy,
etc. Molecules are simply defined as a set of atoms that is held together by simple elastic (harmonic)
forces and the FF replaces the true potential with a simplified model valid in the region being simulated.
Ideally it must be simple enough to be evaluated quickly, but sufficiently detailed to reproduce the
properties of interest of the system studied. There are many force fields available in the literature,
having different degrees of complexity, and oriented to treat different kinds of systems.

There are many codes for molecular dynamics that offer a reliable software landscape to perform this kind of calculation (e.g. Charmm, NAMD, Amber, Gromacs and many others) and to visualize and analyse their output (VMD,
gOpenMol, nMoldyn, ChimeraX, etc ), this area is what most people understand as Molecular Dynamics.

Ideally, forces should be computed from first principles, solving the electronic structure for a particular
configuration of the nuclei, and then calculating the resulting forces on each atom. Since the
pioneering work of Car and Parrinello the development of ab-initio MD (AIMD) simulations has
grown steadily and today the use of the density functional theory (DFT) allows to treat systems
of a reasonable size (several hundreds of atoms) and to achieve time scales of the order of hundreds
of ps, so this is the preferred solution to deal with many problems of interest. However quite often
the spatial and/or time-scales needed are prohibitively expensive for such ab-initio methods. In such
cases we are obliged to use a higher level of approximation and make recourse to empirical force field
(FF) based methods. Codes at the DFT level are for example ABINIT, VASP, Quantum Espresso, Octopus, ELK,
Gaussian and many others.

## Critical aspects in Molecular dynamics simulations

The results of any MD simulation are as good as the parameters chosen for describing the physical conditions of the system under simulation. There are many parameters that have a direct impact on the quality of the results as well as the computational cost of the simulation.

In the case of Force Fields, we can mention, the selection of appropriated force fields. The size and border conditions of the simulation box, if periodic boundary conditions are imposed and the box is not large enough replica effects could ruin the value of the results. In many cases, in particular in biological molecules, the presence of water and other solvents is critical for the proper behavior of the structures under study, selecting the right amount and density of those solvents is one of the first choices to make before starting the simulations. Spurious charges must be taken in also account.

Usually ab-initio approaches are only practical for small atomic structures. In this case there are several choices. Electrons are expressed with wavefunctions and those wavefunctions could be expanded in basis, the basis could be plane waves which is a suitable choice for periodic structures, localized basis are more used for finite systems. Another important choice is which electrons will be expressed explicitly and which electrons will be fixed and their effect accounted via a pseudopotential.
Codes like ELK use a all-electron approach most other codes use the pseudopotentials.

Each particular problem also impose a set of constrains on the methods available. The algorithms used for Geometry optimization are different from NVT simulations. In the first case, a accurate trajectory is of no importance, the fastest the system lowers the energy the better. In the case of chemical reactions the actual path is important.





{% include links.md %}
