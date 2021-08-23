# RAMSES_Bi-Poission
My patched version of the N-body hydrodynamics code RAMSES to take into account two (coupled) Poisson equations
Extensive documentation for RAMSES can be found at [https://bitbucket.org/rteyssie/ramses/src/master/].

The main idea of this project is to customize RAMSES in order to take into account a second particle species.
Instead of the standard Poisson equation <img src="https://render.githubusercontent.com/render/math?math=\Delta \phi = 4 \pi G \rho">, my patch version allows for a dynamics with two Poisson equations which can be customized in the form of 
<img src="https://latex.codecogs.com/svg.latex?\Delta(f(\phi_1,\phi_2))=4&space;\pi&space;G&space;g(\rho_1,\rho_2)" title="\Delta(f(\phi_1,\phi_2))=4 \pi G g(\rho_1,\rho_2)" />
