## Azure Research Allocations

— [Microsoft Azure for Research Award Program](http://research.microsoft.com/en-us/projects/azure/default.aspx):
 Winning proposals are awarded large allocations of Azure storage and compute resources for one year.

* Deadline: *April 15, 2016*
* Proposal should not exceed 3 pages in length or 1000 words
* Proposal should include resource requirement estimates (number of cores, storage requirements)

*Hardware available for HPC*: Azure A9 nodes have 16 cores and 112GB RAM each, with MPI and Infinband, measured latency of < 3 µs
Future release: biggest nodes with 24 CPU cores and 2 x K80 cards (so 4 x GPUs)

#### Proposal Title:
_"Assessing the potential of Azure resources for computational studies of the aerodynamics of animal flight"_

#### Proposal Abstract:

#### Proposal Narrative:

_Introduction_

Our group published a study of the aerodynamics of flying snakes in 2014 [1], using two-dimensional simulations with a fluid solver called cuIBM.
The solver is a serial GPU-enabled code, and thus limited in the size of problems it can handle by the memory available on a single GPU card.
Even so, cuIBM allowed us to find evidence of a surprising aerodynamic effect: enhancement of the lift forces at a particular angle of attack.
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

#### Resource requirements estimate

Prior two-dimensional simulations of the snake cross-section used a Cartesian stretched grid containing about 2.9 million cells.
We centered the bluff-body in the domain $30cx30c$ (where $c$ is the chord-length).
We uniformly discretized the grid with spacing $0.004c$ in both directions, in the region covering the immersed boundary and its immediate vicinity; then stretched the grid to the external boundaries with a constant ratio of 1.01.

If we use the same resolution for the three-dimensional configuration, expand the mesh in the spanwise direction over a length of $\pi c$, and choose a spanwise cell-width that is one order of magnitude larger ($0.04c$), we end up with a mesh-size of roughly 225 millions cells.

A preliminary run of the three-dimensional problem on a smaller mesh of 4 millions cells performed on 4 cores required 8.8GB of RAM.
We estimate that the memory requirements of a PetIBM simulation with a mesh of 225 million cells will need 6 nodes on Azure.

While we estimate this mesh to be DNS-compatible, we are curious to run a strong scaling analysis on a coarser mesh (about 45 million cells when we double the grid-spacing in the streamwise and crosswise directions while maintaining the same stretching ratio).
A mesh of this size will fit on 2 Azure nodes.
This will provide useful data related to the scalability of PetIBM and allow us to compare the DNS flow solution (finer mesh) with an implicit LES solution (coarser mesh).

In order to perform a strong scaling study, we propose to run the coarser mesh over a time-integration period of 100 time-steps with time-increment $8\times10{-3}s$ to maintain a CFL number (based on the freestream speed) lower than 1.0.
As a test, we ran 2800 time-steps on a mesh of 10.3 million cells in about 36 hours using 1 node (16 cores); we estimate the cost per time-step and per mesh-point to be $4.5\times10^{-6}$ seconds.
Therefore, 100 time-steps of the solution on a mesh of 45 million cells will require about 5.6 core hours, or approximately 11 minutes-per-run using 2 nodes.
We would like to perform a strong scaling study of PetIBM using this coarser mesh requesting 2, 4, 8, and 16 nodes.  Each run will be repeated five times and the results taken as the average across the runs.
We estimate that this first stage, studying strong scaling on the coarse grid, will require approximately 112 core hours (FYI: 5*4*5.6).

Second, we would like to evaluate the scalability of PetIBM on a DNS-ready mesh-size of 225 million cells using 6, 8, 12, and 24 nodes.
Running 100 time-steps on this finer mesh will require about 28.1 core hours.
This second stage, on the finer mesh, will total approximately 562 core hours (FYI: 5*4*28.1).

Based on our two-dimensional results at Reynolds number 2000, the flow leaves the transient phase to reach a periodic regime after about 30 non-dimensional time-units.
We propose to use the periodic solution of the flow after 30 time-units as an initial condition for our strong scaling analysis.
Thus, on the coarser mesh, we need to compute 3750 time-steps with time-increment 8\times10^{-3}, requiring 211 core hours (FYI: 4.6E-06*45E+06*3750).
On the finer grid, we need to compute 37500 time-steps with time-increment 4\times10^{-3}, requiring 10500 core hours (FYI: 4.6E-06*225E+06*37500).


(FYI: right now, we end-up with: 112+562+211+10500=11217 core hours.)


We also developed an AmgX-wrapper, compatible with PetIBM, to solve the linear systems on multiple GPUs.
It will be interesting to compare the performances obtained on CPUs and GPUs.

_References_

[1] A. Krishnan, J. Socha, P. Vlachos and L. Barba, "Lift and wakes of flying snakes", Physics of Fluids, vol. 26, no. 3, p. 031901, 2014

