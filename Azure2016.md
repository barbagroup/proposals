## Azure Research Allocations

— [Microsoft Azure for Research Award Program](http://research.microsoft.com/en-us/projects/azure/default.aspx):
 Winning proposals are awarded large allocations of Azure storage and compute resources for one year.

* Deadline: *April 15, 2016*
* Proposal should not exceed 3 pages in length or 1000 words
* Proposal should include resource requirement estimates (number of cores, storage requirements)

*Hardware available for HPC*: Azure A9 nodes have 16 cores and 112GB RAM each, with MPI and Infinband, measured latency of < 3 µs
Future release: biggest nodes with 24 CPU cores and 2 x K80 cards (so 4 x GPUs)

####Proposal Title:
_"Assessing the potential of Azure resources for computational studies of aerodynamics of animal flight"_

####Proposal Abstract:

####Proposal Narrative:

_Background_

Our group published a study of the aerodynamics of flying snakes in 2014 [1], using two-dimensional simulations with a fluid solver called cuIBM.
The solver is a serial GPU-enabled code, and thus limited in the size of problems it can handle by the memory available on a single GPU card.
Even so, cuIBM allowed us to find evidence of a surprising aerodyanmic effect: enhancement of the lift forces at a particular angle of attack.
Lift-enhancement mechanisms are a major contributor to the flight forces created by animal flyers and gliders, and a source of bioinspiration for robotic air vehicles.
To further this research, our group developed a parallel three-dimensional solver called PetIBM.
It uses the PETSc scientific library to solve systems of algebraic equations in parallel CPU clusters.

