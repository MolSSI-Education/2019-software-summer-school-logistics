---
title: MM Project
layout: default
---

# Molecular Mechanics
## Object Oriented Programming

### One Potential Solution

There are many ways you could sove this problem. The following is what the MolSSI team decided.

1. The Box class.
    The Box class is initialized with a box length. A set of particle coordinates as a numpy array is an optional input. The default argument for `particles` is `None`. Meaning that you can have a box without particles. 

    The Box class has the following attributes.
    -  box dimensions (ie the `box_length`)
    - particles - `None` or a numpy array of particle coordinates

    The Box class has the following methods.
    - wrap  
        - Place particles which are outside of box into box based on periodic boundaries.
    - minimum_image_distance
        - arguments are two points. Calculate the distance between these two points based on periodic boundaries.
    - volume
        * The box volume. Uses the `@property` decorator.
    - number_particles
        * Uses the `@property` decorator. Returns 0 if there are no particles (ie `self.particles` is `None`) or the length of the numpy array if there are particles.


1. The MCState class.
    Holds the state of the system (box with particles and thermodynamic quantities like reduced temperature).

    The MCState class is initialized with a box object, cutoff distance, maximum displacement, and reduced temperature.

    The MCState class has the following attributes.
    - box - a Box object
    - cutoff - the simulation cut off
    - max_displacement - the maximum displacement for a Monte Carlo move.
    - beta (1 / reduced_temperature)
    - total_pair_energy
    - tail_correction
    - total_energy
    
    The MCState class has the following methods.
    - calculate_total_pair_energy
        - **returns** the total pair energy 
    - calculate_tail_correction
        - **returns** the tail correction
    - calculate_total_energy
        - **returns** the total energy based on calculation using `calculate_total_pair_energy` and `calculate_tail_correction`.
    - get_particle_energy
        - takes a particle index as an argument. Optional arugment of particle_movement (this is a vector describing out to move the specified particle).
        - **returns** the pairwise interaction energy of a with all other particles.

1. The following functions are not associated with classes.
    - lennard_jones_potential
    - accept_or_reject
    - adjust_displacement
    - generate_initial_cooridinates

1. A Factory Design pattern is used with `generate_initial_coordinates` to specify method. This function now returns a tuple, `coordinates, box_length`. 


1. Add error handling to your functions.

    For example, in the function generate_initial_state, your function should check that input parameters are compatible for each method.
    if the method is "random", expected inputs are num_particles and box_size. Having additional or missing arguments should cause a TypeError.
    if the method is "file", expected inputs are fname. Having additional or missing arguments should cause a TypeError.
    You should check that the method is either "random" or "file". If not either of these, raise a ValueError.
    use a try except clause to open the file for method=file