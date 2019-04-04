% Felt integration in FreeCAD

As my first contribution to a large open-source project with any users, I am attempting to integrate FElt solver in FreeCAD.
So my upcoming blogs are going to be about this whole process.
As an introductory blog, here I would like to discuss the background info so that we are all caught up and are on the same page.
So lets start!!!

## FreeCAD

"FreeCAD is an open-source parametric 3D modeler made primarily to design real-life objects of any size. Parametric modeling allows you to easily modify your design by going back into your model history and changing its parameters.
FreeCAD equips you with all the right tools for your needs. You get modern **Finite Element Analysis (FEA) tools**, experimental CFD, BIM, Geodata workbenches, Path workbench, a robot simulation module that allows you to study robot movements and many more features. FreeCAD really is a Swiss Army knife of general-purpose engineering toolkits."
The above content was taken from FreeCAD's [official website](https://www.freecadweb.org/).

Our main concern will be the Finite Element Analysis tools that FreeCAD provides through its Finite Element Methods (FEM) workbench.

## FElt

[FElt](http://felt.sourceforge.net/) is an open source system for finite element analysis. 

Its a quite old software. The original developers (Jason Gobat and Darren Atkinson) left the Felt project after releasing from 3.02 to 3.05 (as per the [Changelog](https://github.com/Sudhanshu-Dubey14/felt/blob/experiment/CHANGELOG)), and they had the copyright till 2005 (as per the [User Guide](https://github.com/Sudhanshu-Dubey14/Burlap/blob/master/doc/felt.pdf)).
A developer [pvossos](https://github.com/pvossos) picked up the Felt code in 2000 and started working on it. He has releases till 3.07 (same as on [sourceforge](https://sourceforge.net/projects/felt/files/FElt/)) and his last commit was from 2011. He also had a branch in which he was preparing for the 3.08 release but had to stop his work due to personal reasons.

What I worked on (along with my friend [Alok](https://github.com/AkMecha) was a fork of pvossos repo by [inderpreetsingh](https://github.com/inderpreetsingh). When I picked up felt, it had errors in it because of the changes in C++ that had happened over time. I removed all the errors (took me a considerable time) and had to remove [Burlap](https://github.com/Sudhanshu-Dubey14/Burlap) (an octave-like mathematical environment for felt) and Velvet (a GUI for felt) so that [felt](https://github.com/Sudhanshu-Dubey14/felt) could compile on the latest linux system with latest c++.

## FEM

- The finite element method (FEM), is a numerical method for solving problems of engineering and mathematical physics. 
- Typical problem areas of interest include structural analysis, heat transfer, fluid flow, mass transport, and electromagnetic potential. 
- The analytical solution of these problems generally require the solution to boundary value problems for partial differential equations.
- To solve the problem, it subdivides a large system into smaller, simpler parts that are called finite elements. 
- The simple equations that model these finite elements are then assembled into a larger system of equations that models the entire problem.
- FEM then uses variational methods from the calculus of variations to approximate a solution by minimizing an associated error function.
- Studying or analyzing a phenomenon with FEM is often referred to as finite element analysis (FEA).

## FEA using FreeCAD

The steps to carry out a FE analysis are:

1. **Preprocessing**: setting up the analysis problem.
   - *Modeling the geometry*: creating the geometry with FreeCAD, or importing it from a different application.
   - *Creating an Analysis*.
            * Creating a finite element Mesh for the geometrical model.
            + Adding Constraints such as loads and fixed supports to the model.
            * Adding a Material to the analysis model.
1. **Solving**: solving a system of equations using an external solver from within FreeCAD.
1. **Postprocessing**: visualizing the analysis Results from within FreeCAD.
