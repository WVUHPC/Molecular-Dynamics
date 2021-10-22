---
title: "Using Gromacs on WVU HPC resources"
questions:
- "What is GROMACS?"
- "How do I run GROMACS on the cluster?"
- "How do I check on my job and the simulation status?"
objectives:
- "Learn about the HPC GROMACS Modules"
- "Learn how to do some quick analysis on a simulation"
---
"GROMACS"

GROMCS is a free molecular dynamics software package that was originally designed for simulations of biomolecules but, due to it's high performace and force field options, has also been used in research of non-biological systms such as polymers. It is also user friendly with it's files and command inputs being easy to understand and use and comes with a full suite of analysis tools.

"GROMACS commands"

All Gromacs commands in current versions start with the binary "gmx" followed by the specific command and inputs such as:
~~~
gmx solvate -cp 1AKI_newbox.gro -cs spc216.gro -o 1AKI_solv.gro -p topol.top
~~~
This command solvate adds the specified solvent "spc216.gro" into the system provided "1AKI_newbox.gro" and outputs the solvate system as "1AKI_solv.gro" the flags used are uniform across all GROMACS commands to prevent confusion. A full list of all commands and thire use is availble by use of the gmx help option or the online gromacs manuel https://manual.gromacs.org/current/user-guide/cmdline.html

"Lysozyme tutorial"
 
There are multiple tutorials for gromacs at the website http://www.mdtutorials.com/gmx/index.html the first and simplest is the lysozyme in water that provides a good first time experience with GROMACS with good explanations of each step in introductions to the commonly used files, while the others provide experience in other methods and systems setups of md simulations. The first parts of this tutorial, which consist of the setup and minimization, can be completed in a rather short time frame and it is recommended that you experiment with them to learn more at a later time.

[GROMACS_TUTORIAL.zip](https://github.com/AlexanderBWr/Molecular-Dynamics/files/7397124/GROMACS_TUTORIAL.zip)


The later half of the tutorial is the actual MD simulations and can take a quite a few hours to complete depending on the computer, and this issue just gets worse as the sysems size and complexity increases. This situation is where the HPC's are extremely useful, allowing the completetion of simulations far faster than what you be possible otherwise. As such these steps will be done on the HPC following the transfer of the files.

~~~
cd /scratch/yourdirectory/GROMACS_tutorial
~~~

To use the HPC, a pbs script is required, this script contains the modules the HPC has to load, the queue the job is to run on, how long to run the job, the commands to be executed and where they are to be run, amount of nodes requested, the job name, and your email. As long as the pbs script is prepared properly the HPC will queue up the job and run the simulations.

"HPC GROMACS MODULES"

There are multiple GROMACS modules availble on the HPC at WVU allowing for different versions of the software to be used, allowing use of old versions, or use of versions specilized for different software or hardware specifications. The full list of all modules is avalible with the module avail command with the avalible GROMACS versions being in the tier2 modules and all begining with atomistic/gromacs/ and can be loaded with the module load command.
~~~
$ module avail
~~~
~~~
$ module load
~~~

"Loading other modules"
The GROMACS software can not run by itself and requires other sofware package to be loaded to run and while it is possible to try and run a command with out them the only result would be a line of text informing you the name of the missing module it is far quicker to check before hand the the module show command. This command outputs info about the module specified inculing the modules it depends on.
~~~
module show atomistic/gromacs/XXX
~~~
"gmx or gmx_mpi"

One of the more common types of avalible GROMACS versions are the MPI versions of GROMACS that are set up to take full advantage of avalible GPUs. These MPI versions of GROMACS do not have the default binary command of gmx but a binary on gmx_mpi, thus it is important to identify which binary is to be used in the command.
 
The module show command is usefull for identifing these MPI versions as these version require certain other types of module to be loaded such as gcc libaries or openmpi software to be loaded.

"PBSexample"

An example of a pbs script is below just create a file and copy and paste the text into it.

~~~
#!/bin/bash

#PBS -q comm_gpu_week
###comm_gpu_week ###standby ###debug
##select which queue to submit to

#PBS -m abe
###send email at (a)bort, (b)egin, (e)nd

#PBS -M YOUR@email.here
###select email to send messages to

#PBS -N jobname
###select jobname

#PBS -l walltime=168:00:00
###walltime in hh:mm:ss

#PBS -l nodes=1:ppn=8:gpus=1
###set number of nodes and processors per node

module load general_intel18
module load lang/gcc/11.1.0
module load libs/fftw/3.3.9_gcc111
module load atomistic/gromacs/5.1.5_intel18
###tell the cluster to load gromacs
###COMMANDS BELOW

### cd /job directory

cd $PBS_O_WORKDIR
###Your gromacs command here

gmx_mpi grompp -f nvt.mdp -c em.gro -r em.gro -p topol.top -o nvt.tpr

gmx_mpi mdrun -deffnm nvt -nb gpu

gmx_mpi grompp -f npt.mdp -c nvt.gro -r nvt.gro -t nvt.cpt -p topol.top -o npt.tpr

gmx_mpi mdrun -deffnm npt -nb gpu

gmx_mpi grompp -f md.mdp -c npt.gro -t npt.cpt -p topol.top -o md_0_1.tpr

gmx_mpi mdrun -deffnm md_0_1 -nb gpu
~~~

"Running the job and job status"

While there are interactive jobs for running this simulation we only need one command to have the HPC run the job:
~~~
qsub PBSexample
~~~
The status of jobs can be checked with the "qstat" command which will give a list of all jobs currently on the HPC, and jobs for specific users can be isolated with the -u flag.
~~~
qstat -u username
~~~

"Job output and errors"

The HPC will output infomation about the jobs to files based on the job name and job number "jobname.e5282" these files will contain infomation about the job and commands run and any errors that occured.

"Simulation output"

GROMACS will output multiple files that each record different iinformation about the simulation run such as the energy over time and the particle trajectories, however the .log file contains the record of the simulation's progress and is important to read to understand GROMACS pefromance, as it gives information about the time spent on each type of calculation and overall simulation speed.
~~~
     R E A L   C Y C L E   A N D   T I M E   A C C O U N T I N G

On 4 MPI ranks

 Computing:          Num   Num      Call    Wall time         Giga-Cycles
                     Ranks Threads  Count      (s)         total sum    %
-----------------------------------------------------------------------------
 Domain decomp.         4    1       1001       5.961         38.147   0.5
 DD comm. load          4    1        951       0.076          0.489   0.0
 DD comm. bounds        4    1        901       0.127          0.810   0.0
 Neighbor search        4    1       1001      19.563        125.195   1.7
 Comm. coord.           4    1      49000       9.006         57.634   0.8
 Force                  4    1      50001     739.282       4731.188  62.8
 Wait + Comm. F         4    1      50001       7.435         47.581   0.6
 PME mesh               4    1      50001     362.410       2319.321  30.8
 NB X/F buffer ops.     4    1     148001       8.608         55.086   0.7
 Write traj.            4    1        101       0.852          5.455   0.1
 Update                 4    1      50001       7.702         49.290   0.7
 Constraints            4    1      50003       9.691         62.017   0.8
 Comm. energies         4    1       5001       3.759         24.059   0.3
 Rest                                           1.840         11.779   0.2
-----------------------------------------------------------------------------
 Total                                       1176.312       7528.051 100.0
-----------------------------------------------------------------------------
 Breakdown of PME mesh computation
-----------------------------------------------------------------------------
 PME redist. X/F        4    1     100002     172.900       1106.508  14.7
 PME spread             4    1      50001      73.034        467.395   6.2
 PME gather             4    1      50001      50.968        326.180   4.3
 PME 3D-FFT             4    1     100002      39.695        254.034   3.4
 PME 3D-FFT Comm.       4    1     100002      21.577        138.087   1.8
 PME solve Elec         4    1      50001       4.100         26.237   0.3
-----------------------------------------------------------------------------

               Core t (s)   Wall t (s)        (%)
       Time:     4705.206     1176.312      400.0
                 (ns/day)    (hour/ns)
Performance:        7.345        3.267
~~~

"Analysis"

There is not much point in doing simulations if you do not collect infomation at the end, through analysis of the system and how it evolved over the course of the simulation. One type of analysis that should always be done is a visual analysis of the system, as it gives you a perspective on the system that graphs and other anaylsis types will not give. Using VMD load the .gro file and the .trr file and then select the atom types you which to view in the represntations window, in this case to examine the protein you can use use the selction "not resname SOL and not resname ION".

As memtnioned before GROMACS has a full suite of anaylsis tools inculded all of which could be used to perfore analysis on the system being studied, the examples in the lysozyme tutorial are some of the more basic ones that can be used for most simulations but there are specizied analysis command that can be used for specific puropses such as lipid order and polymer properties. One command thet is important to learn how to use is the gmx select command this command selects user specified particles and outputs them into a .ndx file that is used by other commands. For example, createing an .ndx file for the protien. These groups can be specified in the command line with the - select command otherwise the command brings up coomonly used groups for selection.
~~~
gmx select -f npt.gro  -s npt.tpr -on PRO.ndx -select 'atomnr 1 to 1960'
~~~
~~~
gmx select -f npt.gro  -s npt.tpr -on PRO.ndx

Available static index groups:
 Group  0 "System" (33876 atoms)
 Group  1 "Protein" (1960 atoms)
 Group  2 "Protein-H" (1001 atoms)
 Group  3 "C-alpha" (129 atoms)
 Group  4 "Backbone" (387 atoms)
 Group  5 "MainChain" (517 atoms)
 Group  6 "MainChain+Cb" (634 atoms)
 Group  7 "MainChain+H" (646 atoms)
 Group  8 "SideChain" (1314 atoms)
 Group  9 "SideChain-H" (484 atoms)
 Group 10 "Prot-Masses" (1960 atoms)
 Group 11 "non-Protein" (31916 atoms)
 Group 12 "Water" (31908 atoms)
 Group 13 "SOL" (31908 atoms)
 Group 14 "non-Water" (1968 atoms)
 Group 15 "Ion" (8 atoms)
 Group 16 "CL" (8 atoms)
 Group 17 "Water_and_ions" (31916 atoms)
Specify any number of selections for option 'select'
(Selections to analyze):
(one per line, <enter> for status/groups, 'help' for help, Ctrl-D to end)
~~~

{% include links.md %}
