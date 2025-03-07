============
Introduction 
============

The FLOSIC code is based on the UTEP version of NRLMOL, the Naval Research 
Laboratory Molecular Orbital Library.[1-4]

NRLMOL is a massively parallel code for electronic structure calculations on molecules and clusters. 
It is based on the Kohn-Sham (KS) formulation of density functional theory (DFT) and solves KS equations by expressing 
the KS orbitals as a linear combination of Gaussian orbitals. NRLMOL was developed by Mark Pederson and collaborators.

NRLMOL contains an implementation of the Fermi-Löwdin orbital self-interaction correction (FLO-SIC) method[5-8] 
that corrects the self-interaction error for common exchange-correlation functionals.
In FLO-SIC, the Kohn-Sham canonical orbitals are transformed into Fermi orbitals, which are orthogonalized to become Fermi-Löwdin orbitals (FLOs).
These FLOs are used to evaluate the orbital-dependent self-interaction corrected total energy. The transformation requires
a set of parameters that are points in three dimensional space, the so-called
Fermi-orbital descriptors (FODs). These FODs form what can be thought of as the electronic geometry. 
The FOD positions are optimized to obtain the FLOs that minimize the total energy.  
Thus, there are two geometries to consider in a FLOSIC calculation: The molecular geometry (given by the atoms) and the electronic geometry (given by the FODs).

The optimization of the FODs is a crucial part of any FLO-SIC calculation. 
FOD optimization is analagous to a molecular geometry optimization. From a given FOD starting point, 
FOD forces (energy gradients with respect to FOD positions)
are calculated and fed into a gradient-based optimization scheme,
along with the FOD positions and the total energy, to update FOD positions.
The optimization continues until the total energy and the FOD forces are converged.

The following is a list of some SIC-related properties that are calculated using the FLOSIC code:

	- Total energy
	- SIC contribution to the energy
	- Orbital energies
	- Orbital contributions to self-interaction correction; orbital moments, self-Coulomb, self-exchange, and self-correlation energy.
	- Analytical FOD forces (for FOD optimization using conjugate gradient or LBFGS optimizers)
	- Orbitals in .cube format

Physically interesting properties that have been evaluated recently with the FLOSIC code include:[9-14] 

	- Atomization energies
	- Ionization potentials from the highest occupied orbitals
	- SIC optimized molecular geometries
	- Polarizabilities
	- Dipole moments
	- Magnetic exchange couplings
        - Chemical reaction barriers

The following are references to the NRLMOL code:

        [1] `M.R. Pederson and K.A. Jackson, Phys. Rev. B 41, 7453 (1990). <https://journals.aps.org/prb/abstract/10.1103/PhysRevB.41.7453>`_ 

        [2] `K.A. Jackson and M.R. Pederson, Phys. Rev. B 42, 3276,(1990). <https://journals.aps.org/prb/abstract/10.1103/PhysRevB.42.3276>`_  

        [3] `D. Porezag and M.R. Pederson,  Phys. Rev. A 60, 2840, (1999). <https://journals.aps.org/pra/abstract/10.1103/PhysRevA.60.2840>`_

        [4] `M.R. Pederson et al., phys. stat. sol. b, 217, 197, (2000). 
        <https://onlinelibrary.wiley.com/doi/abs/10.1002/%28SICI%291521-3951%28200001%29217%3A1%3C197%3A%3AAID-PSSB197%3E3.0.CO%3B2-B>`_

Further information about the FLO-SIC method can be found in the following references:

        [5] `M.R. Pederson, A. Ruszsinszky, J.P. Perdew., J. Chem. Phys. 140, 121103, (2014). <https://aip.scitation.org/doi/10.1063/1.4869581>`_

        [6] `M.R. Pederson, J. Chem. Phys. 142, 064112, (2015). <https://aip.scitation.org/doi/10.1063/1.4907592>`_

        [7] `Z.-h. Yang, M.R. Pederson, J.P. Perdew, Phys. Rev. A 95, 052505, (2017). <https://journals.aps.org/pra/abstract/10.1103/PhysRevA.95.052505>`_

        [8] `M.R. Pederson, T. Baruah, Advances In Atomic, Molecular, and Optical Physics, Chapter 8, (2015). 
        <https://www.sciencedirect.com/science/article/pii/S1049250X15000087?casa_token=yjEnP6mZkNIAAAAA:JnqLVhS0FyoQT6ZbQM-4ZtNXRkkRFHFnYvM_UQO1ItyCsR8LSWHuo4MgN3RuDA44OFl8n1Ao_Q>`_

Applications of FLO-SIC are described in these references:

        [9] `K. Sharkas et al., J. Phys. Chem. A 122, 9307-9315, (2018). <https://pubs.acs.org/doi/10.1021/acs.jpca.8b09940>`_

        [10] `R.P. Joshi et al., J. Chem. Phys. 149, 164101, (2018). <https://pubs.aip.org/aip/jcp/article/149/16/164101/199258/Fermi-Lowdin-orbital-self-interaction-correction>`_

        [11] `D.-y. Kao, K. Withanage, T. Hahn, J. Batool, J. Kortus, K. Jackson, J. Chem. Phys 147, 164107, (2017).
        <https://pubs.aip.org/aip/jcp/article/147/16/164107/76817/Self-consistent-self-interaction-corrected-density>`_

        [12] `S. Schwalbe, T. Hahn, S. Liebing, K. Trepte, J. Kortus, J. Comput. Chem. 39, 2463-2471, (2018). <https://onlinelibrary.wiley.com/doi/10.1002/jcc.25586>`_

        [13] `K. Withanage, K. Trepte, J.E. Peralta, T. Baruah, R. Zope, K.A. Jackson, J. Chem. Theory Comput. 14, 4122-4128, (2018). <https://pubs.acs.org/doi/10.1021/acs.jctc.8b00344>`_

        [14] `K. Trepte, S. Schwalbe, T. Hahn, J. Kortus, D.-y. Kao, et al., J. Comput. Chem. 40, 820-825, (2019). <https://onlinelibrary.wiley.com/doi/10.1002/jcc.25767>`_

