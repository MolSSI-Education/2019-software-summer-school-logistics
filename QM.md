---
title: QM Project
layout: default
---

# Quantum Mechanics
## Object Oriented Programming

### One Potential Solution

This is the solution the MolSSI team decided. Your team may decided to implement something different.

1. The `Noble_Gas_Model` class.
    The Noble Gas model is a data class. It has data associated with the noble gas model, and utility functions for indexing. 

    The Noble Gas model class is initialized with a gas type. 

    The `Noble_Gas_Model` class has the following attributes.
    -  model_parameters
        A dictionary of the parameters for a specific noble gas. You already have the parameters for Argon.

        You can also add paramters for Neon.
        ```
        {
                'coulomb_p': -0.010255409806855187,
                'coulomb_s': 0.4536486561938202,
                'dipole': 1.6692376991516769,
                'energy_p': -3.1186533988406335,
                'energy_s': 11.334912902362603,
                'r_hop': 2.739689713337267,
                'r_pseudo': 1.1800779720963734,
                't_pp1': -0.029546671673199854,
                't_pp2': -0.0041958662271044875,
                't_sp': 0.000450562836426027,
                't_ss': 0.0289251941290921,
                'v_pseudo': -0.015945813280635074
        }
        ```
    The rest of the attributes are general for every noble gas.
    - ionic_charge
    - orbital_types
    - p_orbitals
    - orbitals_per_atom
    - vec
    - orbital_occupations

    The `Noble_Gas_Model` class has the following methods (indexing functions)

    - atom
    - ao_index
    - orb

This class is an example of the [builder pattern](https://en.wikipedia.org/wiki/Builder_pattern).

2. The `Hartree_Fock` class
    The Hartree Fock class performs the Hartree Fock calculation. It is initialized with atomic_cooridnates, and a `Gas_Model` object.
    
    The `Hartree_Fock` class has the following attributes.

    - atomic coordinates
    - gas modle
    - ndof (number of degrees of freedom)
    - interaction matrix
    - density matrix
    - chi tensor
    - hamiltonian matrix
    - fock matrix

    The `Hartree_Fock` class has the following methods.

    - calculate_interaction_matrix
    - coulomb_energy
    - calculate_potential_vector 
    - calculate_chi_tensor
    - chi_on_atom
    - hopping_energy
    - calculate_hamiltonian_matrix
    - pseudopotential_energy
    - calculate_atomic_density_matrix
    - calculate_fock_matrix
    - calculate_density_matrix
    - scf_cycle
    - calculate_energy_ion
    - calculate_energy_scf
    - solve 
        Performs scf cycle.

3. The `MP2` class
    The MP2 class inherits from `Hartree_Fock`.

    The MP2 class is intialized with atomic coordinates and a gas model object.

    The MP2 class has the following additional attributes.

    - hf_energy
    - occupied_energy
    - interaction_tensor

    The MP2 class has the following additional methods.
    - partition_orbitals
    - transform_interaction_tensor
    - calcualte_energy_mp2
    
    The MP2 also has a solve method. It must first run Harteee Fock, then do some additional work to solve MP2. Since the MP2 class inherits from `Hartree_Fock`, you can use `super()` to inherit everything from the `Hartree_Fock` solve. Then you can add code for doing MP2.

**challenge** - The way the MP2 method is currently implemented, an MP2 object will always have to first run Hartree Fock. Can you figure out a way to initialize the MP2 class with a Hartree Fock object? (we haven't taught you this)

