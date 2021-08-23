# RAMSES_Bi-Poission
My patched version of the N-body hydrodynamics code RAMSES to take into account two (coupled) Poisson equations
Extensive documentation for RAMSES can be found at [https://bitbucket.org/rteyssie/ramses/src/master/]. All changes to the main version are highlighted by a comment ```BiP``` (Bi-Poisson).

The main idea of this project is to customize RAMSES in order to take into account a second particle species.
Instead of the standard Poisson equation <img src="https://latex.codecogs.com/svg.latex?\Delta&space;\phi&space;=4&space;\pi&space;G&space;\rho" title="\Delta \phi =4 \pi G \rho" />, my patch version allows for a dynamics with two Poisson equations which can be customized in the form of <img src="https://latex.codecogs.com/svg.latex?\Delta(f(\phi_1,\phi_2))=4&space;\pi&space;G&space;g(\rho_1,\rho_2)" title="\Delta(f(\phi_1,\phi_2))=4 \pi G g(\rho_1,\rho_2)" />, with <img src="https://latex.codecogs.com/svg.latex?f" title="f" /> and <img src="https://latex.codecogs.com/svg.latex?g" title="g" /> two arbitrary functions of the two potentials <img src="https://latex.codecogs.com/svg.latex?\phi_1" title="\phi_1" />, <img src="https://latex.codecogs.com/svg.latex?\phi_2" title="\phi_2" /> and their corresponding densities <img src="https://latex.codecogs.com/svg.latex?\rho_1" title="\rho_1" />,<img src="https://latex.codecogs.com/svg.latex?\rho_2" title="\rho_2" />.

This can be achieved by changing line 69 of ``phi_fine_cg.f90`` and the rest of this file accordingly.

For the specific case of the "Dirac-Milne" universe, we studied the following equations:

<img src="https://latex.codecogs.com/svg.latex?\Delta&space;\phi_1=&space;4&space;\pi&space;G&space;(\rho_1-\rho_2)" title="\Delta \phi_1= 4 \pi G (\rho_1-\rho_2)" />

<img src="https://latex.codecogs.com/svg.latex?\Delta&space;\phi_2=&space;4&space;\pi&space;G&space;(-\rho_1-\rho_2)" title="\Delta \phi_2= 4 \pi G (-\rho_1-\rho_2)" />

More details can be found in [https://arxiv.org/abs/2102.08834]

In order to run the code, one needs to provide initial conditions for this specific dynamics, to do so, one needs to tell the code to which species each particles belong. This was achieved by using a "mask", that is provided by the user in addition to the usual initial conditions (generated for instance with [MUSIC](https://www-n.oca.eu/ohahn/MUSIC/). The mask is a fortran cube with has the same form as the other input. It however contains only 0 or 1 (first or second species). More details how RAMSES reads that mask can be seen around line 510 of ``init_part.f90``.
