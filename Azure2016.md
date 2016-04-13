## Azure Research Allocations

— [Microsoft Azure for Research Award Program](http://research.microsoft.com/en-us/projects/azure/default.aspx):
 Winning proposals are awarded large allocations of Azure storage and compute resources for one year.

* Deadline: *April 15, 2016*
* Proposal should not exceed 3 pages in length or 1000 words
* Proposal should include resource requirement estimates (number of cores, storage requirements)

*Hardware available for HPC*: Azure A9 nodes have 16 cores and 112GB RAM each, with MPI and Infinband, measured latency of < 3 µs
Future release: biggest nodes with 24 CPU cores and 2 x K80 cards (so 4 x GPUs)

####Proposal Title:
_"Assessing the potential of Azure resources for computational studies of the aerodynamics of animal flight"_

####Proposal Abstract:

####Proposal Narrative:

_Introduction_

Our group published a study of the aerodynamics of flying snakes in 2014 [1], using two-dimensional simulations with a fluid solver called cuIBM.
The solver is a serial GPU-enabled code, and thus limited in the size of problems it can handle by the memory available on a single GPU card.
Even so, cuIBM allowed us to find evidence of a surprising aerodyanmic effect: enhancement of the lift forces at a particular angle of attack.
Lift-enhancement mechanisms are a major contributor to the flight forces created by animal flyers and gliders, and a source of bioinspiration for robotic air vehicles.
To further this research, our group developed a parallel three-dimensional solver called PetIBM.
It uses the PETSc scientific library to solve systems of algebraic equations in parallel CPU clusters.
Recently, we also coupled PetIBM with the AmgX library for solving systems of equations on multi-GPUs.
This work was presented at the GPU Technology Conference, held April 4-7 2016 in San Jose, CA.
We also made available a technical report as supplementary material to the conference presentation, in the form of a Jupyter notebook:
["Using AmgX to Accelerate PETSc-Based CFD Codes"](http://nbviewer.jupyter.org/github/barbagroup/conferences/blob/2f51957e03585d980a471c52595f46551948b771/GTC2016/GTC2016_S6355.ipynb)
As reported therein, we looked at the cost difference in running simulations with PetIBM on GPU nodes (using AmgX) versus CPU nodes (using PETSc), using AWS EC2 cloud resources.
This was the first time that we studied the suitability of cloud resources for our research, and we are encouraged by the results.
The goal of this Microsoft Azure Research allocation award is to establish the suitability of Azure resources for our research on the aerodynamics of animal flight, using our PetIBM code.
We estimated that with 200k CPU-core hours, we will be able to complete a small-scale study of the parallel performance of PetIBM on Azure CPU nodes.
We would also like to run PetIBM on the new Azure GPU nodes, and compare the time-to-solution and cost of both architectures for our application.
The results of this study will allow us to estimate the resources that would be needed to complete a full study of the three-dimensional lift-enhancement mechanism in anatomically correct sections of a flying snake's body.

_References_

[1] A. Krishnan, J. Socha, P. Vlachos and L. Barba, "Lift and wakes of flying snakes", Physics of Fluids, vol. 26, no. 3, p. 031901, 2014

