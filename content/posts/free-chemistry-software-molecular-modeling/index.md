---
title: "Free Chemistry Software - Molecular Modeling"
date: 2011-10-29T08:35:48+02:00
categories: [chemistry]
tags: [computational chemistry, chemistry, free software, IGF-1, IYC, molecular modeling, gromacs]
draft: false
---

## Free Chemistry Software - Molecular Modeling

Molecular modeling is a very large and important field of chemistry. As computers have increased in raw computing power, the usage of computers to calculate molecular properties is not a specialized fields for the few. Today, every chemist can perform calculation for even large molecules.


Roughly speaking, you can divide the calculations in two separate groups: molecular mechanics and quantum chemistry. The first is based on classical mechanics, while the second group uses quantum mechanics as a underlying model and equations. The software list at http://en.wikipedia.org/wiki/Molecular_modeling shows a wide range of offerings. Many of them are commercial and closed-source solutions.

Molecular mechanics calculations are used when no chemistry is going to. By definition, chemistry is the rearrangement of atoms - and that involves electrons. But molecular mechanics can be used to investigate how a molecule is solvent that is, how its structure changing when it is surrounded by a solvent like water.

[Gromacs](http://www.gromacs.org/) is one of the oldest and most successful molecular mechanics software suites. It is covered by the GNU General Public License (version 2), and most distributions like Debian GNU/Linux have a package of it. It does not come with a fancy user interface, and the user primarily interacts with Gromacs at the command line. It is a big advantage as some of the operations can take a long time. Seldomly, you sit by your computer and work with Gromacs. The typical usage is to write small shell scripts and run them as batch jobs.

Today, most supercomputers in the chemical industry and academia are Linux clusters which are build from commodity hardware. That means that a supercomputer is a distributed system where the individual processors are loosely coupled using Ethernet (or maybe InfiniBand). The [MPI](http://www.mpi.org/) framework is used by Gromacs to utilize such a supercomputer (if you have a SMP system, MPI can still be used for parallelization). Queuing systems (SUN Grid Engine, OpenPBS/Torque, etc.) schedule which batch job to execute, and the command-line nature of Gromacs comes to its rights on such systems.

Explaining all details of Gromacs is not the scope here. But let us a quick tour on how to use some of the many utilities and programs of Gromacs. The assignment is to take the experimentally determined structure a small biological active molecule and create a solvated version of the molecule. The structure found at the Protein DataBank is for a crystal, and IGF-1 (as most other molecules in your body) is in a solution where water is the solvent (remember, 60 % of you body is water). For the tour, the [Insulin-like growth factor 1](http://en.wikipedia.org/wiki/IGF-1) (IGF-1) is chosen. IGF-1 is a small protein (or peptide) which is involved of the growth and regeneration of your body. You can download a file with the experimental structure from [Protein DataBank](http://www.pdb.org/pdb/home/home.do).

First, you must pre-process the downloaded file into files used by Gromacs. In that process you decided the force field. The force field is the parametrization of the interaction between the atoms, and all calculations in Gromacs (and any other molecular mechanical program) are based on [Newton's second law](http://en.wikipedia.org/wiki/Newton's_second_law#Newton.27s_second_law). In the command-line below, two files are generated (`2GF1.gro` and `2GF1.top`).

```sh
pdb2gmx -f 2GF1.pdb -o 2GF1.gro -p 2GF1.top -ignh -ff G53a6
```

Now you have to edit the output file (`2GF1.gro`) in order to change box size. You can do an energy minimization and generate a solvation box using the commands (some steps might take some time):

```sh
mdrun -v -deffnm 2GF1-EM-vacuum -c 2GF1-EM-vacuum.gro
editconf -f 2GF1-EM-vacuum.gro -o 2GF1-PBC.gro -bt dodecahedron -d 1.2
genbox -cp 2GF1-PBC.gro -cs spc216.gro -p 2GF1.top -o 2GF1-water.gro
```

The final file is `2GF1-water.gro` which is the biological molecule solvated in water. It might not sound as a great deal, but the file can be used in further simulation involving the solvated molecule.

Other molecular modeling packages exists. [NAMD](http://www.ks.uiuc.edu/Research/namd/) is a highly scalable molecular dynamics program. It is aimed at large molecules (proteins) and can utilize very large parallel computers. But NAMD is not free software as defined by [Free Software Foundation](http://www.fsf.org/). You can download it and use it for any non-commercial purpose.
