# Thomson Problem Simulation (MATLAB)

![Simulation Demo](https://github.com/user-attachments/assets/603aa053-155e-4ade-a7de-0492e69cdc17)

A MATLAB-based N-Body simulation that solves the **Thomson Problem**: determining the distribution of N electrons constrained to the surface of a unit sphere.

Using `ode45` for numerical integration, this script calculates the interaction of charged particles under Coulomb's Law while enforcing spherical constraints. It creates a 3D visualization of the particles' trajectories as they evolve over time.

## Features

* **N-Body Solver:** Vectorized calculation of pairwise Coulomb forces for an adjustable number of electrons.
* **Dual Simulation Modes:**
  * **Equilibrium Finding (Relaxation):** Using drag (Mu > 0), particles lose energy and settle into a minimum potential energy configuration (e.g., the vertices of a Platonic solid).
  * **Chaotic Motion:** With zero drag (Mu = 0), particles exhibit continuous, conservation-of-energy orbital motion on the spherical surface.
* **Dynamic Visualization:** Includes a built-in animation loop with rotating camera angles, particle trails, and specific coloring for up to 7 unique spheres.
* **Vectorized Physics:** Utilizes MATLAB's `cellfun` and 3D matrix operations for efficient force calculation without nested loops for pair interactions.

## How It Works

### The Physics

The simulation uses **arbitrary dimensionless units** (k=1, m=1, q=1). The motion is governed by three primary vector components:

1. **Coulomb Repulsion:** The electrostatic force between every pair of electrons.
   $$F_{c} = k \frac{q_i q_j}{|r|^3} r$$

2. **Spherical Constraint:** To keep particles on the sphere, the code calculates:
   * **Projection Force:** Removes the radial component of the Coulomb force.
   * **Centrifugal Correction:** Compensates for velocity to maintain the radius.

3. **Drag Force:** A damping term proportional to velocity.
   $$F_{drag} = -\mu v$$

### The Code Structure

* **Initialization:** Electrons are spawned at random positions on the sphere using spherical coordinates (theta, phi).
* **Solver:** The standard `ode45` (Runge-Kutta) solver integrates the state vector (Position and Velocity).
* **Visualization:** A custom loop draws the sphere and updates particle positions with a trail effect.

## Requirements

* **MATLAB** (Base installation is sufficient; no additional toolboxes required).

## Usage

1. Clone the repository or download the script.
2. Open the script in MATLAB.
3. Adjust the **Configuration Variables** (optional, see below).
4. Run the script. A figure window will appear showing the animation.

### Configuration Variables

You can modify the following variables at the top of the script or inside the `electron_derivatives` function to change the simulation behavior:

| Variable | Location | Description |
| :--- | :--- | :--- |
| `electron_num` | Top of Script | Number of particles to simulate (Default: 5). |
| `Mu` | Top of Script | Drag coefficient. Set **>0** for relaxation (finding shapes), or **0** for chaotic motion. |
| `tspan` | Top of Script | Duration and time-step of the solver. |

## Author

**Fisayo Ogunsulire**

## License

No license provided. All rights reserved.
