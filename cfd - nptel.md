# week 1 assignment

- The reformulation is often chosen for numerical convenience, not because it simplifies the order of the equations.
- The complexity in terms of differential order remains equivalent to the original Navier-Stokes equations.
---
- When dye is injected at a point in a flow, it traces the locations of all fluid particles that have passed through that point over time—this is called the streak line. At any later moment, the ends of these dye traces match the endpoints of the particles’ path lines through the injection point.
---

| Boundary Condition | Definition                                         | Example                         |
|--------------------|--------------------------------------------------|--------------------------------|
| Dirichlet          | Specifies the function value on the boundary     | $u(a) = A$                     |
| Neumann            | Specifies the derivative (flux) on the boundary  | $u'(a) = \alpha$               |
| Cauchy             | Specifies both function value and derivative     | $u(a) = A$, $u'(a) = \alpha$   |
| Robin              | Specifies a linear combination of value and derivative | $a u(a) + b u'(a) = g(a)$     |

---

| Operator   | Definition (CFD context)                                        | Example/Notes                                                                                                                                                                                                                 |
| ---------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Gradient   | Vector of spatial rate of change of a scalar field              | $\nabla \phi = \left(\frac{\partial \phi}{\partial x},\frac{\partial \phi}{\partial y},\frac{\partial \phi}{\partial z}\right)$                                                                                               |
| Divergence | Scalar measuring net outflow (source or sink) of a vector field | $\nabla \cdot \mathbf{u} = \frac{\partial u}{\partial x}+\frac{\partial v}{\partial y}+\frac{\partial w}{\partial z}$                                                                                                         |
| Curl       | Vector measuring local rotation or swirling of a vector field   | $\nabla \times \mathbf{u} = \left(\frac{\partial w}{\partial y}-\frac{\partial v}{\partial z},\frac{\partial u}{\partial z}-\frac{\partial w}{\partial x},\frac{\partial v}{\partial x}-\frac{\partial u}{\partial y}\right)$ |

---

| Operator   | Definition                                                                                      | Zero Case                              |
|------------|------------------------------------------------------------------------------------------------|--------------------------------------|
| Gradient   | $\nabla \phi = \left(\frac{\partial \phi}{\partial x},\frac{\partial \phi}{\partial y},\frac{\partial \phi}{\partial z}\right)$ | $\nabla \phi = \mathbf{0} \Rightarrow \phi$ constant |
| Divergence | $\nabla \cdot \mathbf{F} = \frac{\partial F_1}{\partial x} + \frac{\partial F_2}{\partial y} + \frac{\partial F_3}{\partial z}$ | $\nabla \cdot \mathbf{F} = 0$ incompressible/source-free |
| Curl       | $\nabla \times \mathbf{F} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ F_1 & F_2 & F_3 \end{vmatrix}$ | $\nabla \times \mathbf{F} = \mathbf{0}$ irrotational      |

---
## Stream Function and Velocity Components

For two-dimensional incompressible flow, the velocity components \(u\) and \(v\) can be expressed using the stream function \(\psi(x,y)\) as:

$$
u = \frac{\partial \psi}{\partial y}
$$

$$
v = -\frac{\partial \psi}{\partial x}
$$

- Here, \(u\) is the velocity component in the \(x\)-direction.
- \(v\) is the velocity component in the \(y\)-direction.
- The stream function \(\psi\) is a scalar function, constant along streamlines.
- This formulation automatically satisfies the continuity equation for incompressible flow.
---
- Eulerian approach: Observes and describes fluid properties at fixed points in space as time changes.
- Lagrangian approach: Follows and describes the motion of individual fluid particles as they move through space and time.
---

| Term        | Definition                                                                                                     |
|-------------|----------------------------------------------------------------------------------------------------------------|
| Streamline  | Curve tangent to velocity vector at an instant; shows flow direction at that moment                            |
| Streakline  | Locus of all particles that have passed through a fixed point over time; e.g., dye continuously injected      |
| Pathline    | Trajectory followed by a single fluid particle over time                                                     |
| Timeline    | Line formed by fluid particles marked simultaneously at an instant, tracked over time                         |

| Coincidence Cases                                                    |
|----------------------------------------------------------------------|
| Streamline = Streakline = Pathline = Timeline in steady flow         |
| Streamline and Timeline coincide since both are instant snapshots    |
| Streakline and Pathline coincide for continuous particle injection   |

---

| Number           | Symbol | Formula/Definition                                            |
| ---------------- | ------ | ------------------------------------------------------------- |
| Reynolds number  | Re     | Inertial force / Viscous force                                |
| Capillary number | Ca     | Viscous force / Surface tension                               |
| Froude number    | Fr     | Inertial force / Gravity force                                |
| Weber number     | We     | Inertial force / Surface tension                              |
| Nusselt number   | Nu     | Convective HT / Conductive HT                                 |
| Prandtl number   | Pr     | Momentum diffusivity / Thermal diffusivity                    |
| Stanton number   | St     | Heat Transferred / Thermal capacity = $\frac{Nu}{Re\cdot Pr}$ |

---
## General Form of 2nd order PDE
$$
A \phi_{xx} + B \phi_{xy} + C \phi_{yy} + D \phi_x + E \phi_y + F \phi + G = 0
$$

### Classification Criterion
Discriminant:  
$$
\Delta = B^2 - 4AC
$$
- If $\Delta < 0$: Elliptic PDE  
- If $\Delta = 0$: Parabolic PDE  
- If $\Delta > 0$: Hyperbolic PDE  

### PDE Types and Examples

| Type      | Properties                                | Examples                              |
|-----------|------------------------------------------|-------------------------------------|
| Elliptic  | No real characteristics, steady behavior | Laplace Eq: $\phi_{xx} + \phi_{yy} = 0$ |
| Parabolic | One repeated characteristic, diffusion type | Heat Eq: $\phi_t - k(\phi_{xx} + \phi_{yy}) = 0$ |
| Hyperbolic| Two distinct real characteristics, wave type | Wave Eq: $\phi_{tt} - c^2(\phi_{xx} + \phi_{yy}) = 0$ |
| Mixed     | Changes type in domain                     | Tricomi Eq (Elliptic-Hyperbolic mixed) |

---
## Laplacian Operator
- Mathematical form: $\nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} + \frac{\partial^2}{\partial z^2}$
- Explanation: Measures how a quantity diffuses or spreads out from a point in space.

## Conservation of Momentum Equation (General form)
$$
\rho \frac{D \mathbf{u}}{D t} = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{a}
$$
- $\rho$: fluid density  
- $\frac{D}{D t}$: material derivative (rate of change following a fluid particle)  
- $\mathbf{u}$: velocity vector  
- $p$: pressure  
- $\boldsymbol{\tau}$: deviatoric (viscous) stress tensor  
- $\mathbf{a}$: body acceleration (e.g., gravity)

## Navier-Stokes Equation

### For Incompressible Newtonian Fluid
$$
\rho \left(\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right) = - \nabla p + \mu \nabla^2 \mathbf{u} + \rho \mathbf{a}
$$
- $\mu$: dynamic viscosity  
- Left side: fluid inertia (acceleration)  
- Right side: pressure force, viscous force, and external body forces

### For Compressible Newtonian Fluid
$$
\rho \left(\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u}\right) = - \nabla p + \mu \nabla^2 \mathbf{u} + \left(\mu + \lambda \right) \nabla (\nabla \cdot \mathbf{u}) + \rho \mathbf{a}
$$
- $\lambda$: second coefficient of viscosity (bulk viscosity)  
- Additional term $\left(\mu + \lambda \right) \nabla (\nabla \cdot \mathbf{u})$ accounts for compressibility effects.

## Continuity Equation

### Incompressible Flow
$$
\nabla \cdot \mathbf{u} = 0
$$
- Constant density, no volume change in fluid particles.

### Compressible Flow
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
- Allows density to change with time and space.
---
## Types of Grids

### Structured Grids
- Regular arrangement of grid points in a curvilinear coordinate system.
- Grid points and cells have a structured, ordered indexing (i, j, k).
- Advantages: Efficient storage, simple neighbor relationships, easier numerical methods.
- Disadvantages: Difficult to fit complex geometries.

### Unstructured Grids
- Irregular arrangement of points and cells, no fixed connectivity pattern.
- Requires explicit connectivity data to define neighbors.
- Can use various cell shapes (triangles, tetrahedrons).
- Advantages: Easily adapts to complex geometries and local refinements.
- Disadvantages: More complex data structure and higher computational cost.

### O-C Type Grids
- Combination of O-type and C-type grid topologies.
- O-type: Grid lines form closed loops around objects (good for around bodies).
- C-type: Grid lines wrap around the body and extend downstream (better wake resolution).
- O-C hybrid combines strengths for complex shapes and flow features.

### Body-Fitted Grids
- Grids that conform closely to the geometry of the physical body.
- Created by mapping flow domain to a computational domain that matches shape.
- Facilitates accurate boundary condition application on complex shapes.
- Can be structured or block-structured with orthogonal or non-orthogonal curvilinear coordinates.
- Common in simulations requiring precise geometric fidelity.
---
## Forward Difference Second Derivative Scheme

**Scheme:**  
$$
\frac{\partial^2 f}{\partial x^2} \approx \frac{f_{i+2} - 2f_{i+1} + f_i}{\Delta x^2}
$$

- This uses points $i, i+1, i+2$, making it a forward difference.
- Taylor expansion shows the local truncation error is $O(\Delta x)$.
- Thus, **order of accuracy is 1 (first-order accurate)**.
---
## Central Difference Second Derivative Steps

Compute $\frac{d^2f}{dx^2}$ for $f(x) = \sin\left(\frac{\pi x}{4}\right)$ at $x = 1.5$
Step size: $h = 0.01$

### Steps

1. Find $f(x+h)$, $f(x)$, and $f(x-h)$:
   - $f(1.51) = \sin\left(\frac{\pi \times 1.51}{4}\right)$
   - $f(1.5) = \sin\left(\frac{\pi \times 1.5}{4}\right)$
   - $f(1.49) = \sin\left(\frac{\pi \times 1.49}{4}\right)$

1. Apply central difference formula:
$$
\frac{d^2f}{dx^2} \approx \frac{f(x+h) - 2f(x) + f(x-h)}{h^2}
$$

2. Substitute values and calculate:
   - Plug computed $f$ values and $h = 0.01$ into the formula.

1. The answer is $-0.56$
---
## types of differences table for 1st and 2nd order derivatives

| Derivative Order | Method                   | Formula                                       | Accuracy Order            |
| ---------------- | ------------------------ | --------------------------------------------- | ------------------------- |
| 1st Derivative   | Forward Difference (FD)  | $\frac{f_{i+1} - f_i}{\Delta x}$              | 1st order                 |
|                  | Backward Difference (BD) | $\frac{f_i - f_{i-1}}{\Delta x}$              | 1st order                 |
|                  | Central Difference (CD)  | $\frac{f_{i+1} - f_{i-1}}{2 \Delta x}$        | 2nd order                 |
| 2nd Derivative   | Forward Difference (FD)  | $\frac{f_i - 2f_{i+1} + f_{i+2}}{\Delta x^2}$ | 2nd order (sometimes 1st) |
|                  | Backward Difference (BD) | $\frac{f_{i-2} - 2f_{i-1} + f_i}{\Delta x^2}$ | 2nd order (sometimes 1st) |
|                  | Central Difference (CD)  | $\frac{f_{i+1} - 2f_i + f_{i-1}}{\Delta x^2}$ | 2nd order                 |

---
## Taylor Series Expansion

### Expansion at $f(x)$
$$
f(x) = \sum_{k=0}^\infty \frac{f^{(k)}(x)}{k!} (x - a)^k
$$

### Expansion at $f(x + n \Delta x)$
$$
f(x + n \Delta x) = \sum_{k=0}^\infty \frac{f^{(k)}(x)}{k!} (n \Delta x)^k
$$

Where:  
- $f^{(k)}(x)$ is the $k$-th derivative of $f$ at $x$.
- $n$ is an integer multiple of the step size $\Delta x$.
- $a$ is the point about which the function $f$ is expanded.
---

# CFD Numerical Methods MCQ Tips & Tricks for week 3 assignment

## 1. Stability Analysis Tips

### How to Identify Stability Types
**Conditionally Stable:**
- Requires CFL condition: $\Delta t < \text{some limit}$
- Examples: FTCS (Forward Time Central Space), explicit schemes
- **Trick:** Explicit schemes are usually conditionally stable

**Unconditionally Stable:**
- No restrictions on time step $\Delta t$ or CFL number
- Examples: Implicit schemes (Backward Euler), DuFort-Frankel
- **Trick:** Look for "implicit" or "backward" in scheme names
---
### implicit and explicit scheme

| Feature            | Explicit Scheme                                        | Implicit Scheme                                       |
| ------------------ | ------------------------------------------------------ | ----------------------------------------------------- |
| Definition         | Computes future values using known past/current values | Involves solving equations with unknown future values |
| Stability          | Conditionally stable, limited by CFL condition         | Usually unconditionally stable                        |
| Computational Cost | Lower, direct update                                   | Higher due to solving systems                         |
| Example            | Forward Euler, FTCS, Explicit RK                       | Backward Euler, Crank-Nicolson, DuFort-Frankel        |

---
### Quick Stability Check Method
1. **Von Neumann Analysis:** Look for amplification factor $G$
   - Stable if $|G| \leq 1$
   - CFL condition typically: $\Delta t / \Delta x^2 \leq 1/2$ for diffusion
2. **For diffusion equation:** CFL = $\alpha \Delta t / \Delta x^2 \leq 0.5$
3. **For wave equation:** CFL = $c \Delta t / \Delta x \leq 1$

## 2. Order of Accuracy Tips

### How to Determine Order
**From Taylor Series Expansion:**
1. Expand all terms using Taylor series about base point
2. Substitute into finite difference formula
3. **Leading error term** determines order
   - If error $\propto (\Delta x)^n$, then scheme is $n$-th order accurate

**Quick Recognition:**
- **Central differences:** Usually 2nd order
- **Forward/Backward differences:** Usually 1st order
- **Higher-order schemes:** Use more grid points

### Example Pattern Recognition
- $\frac{f_{i+1} - f_{i-1}}{2\Delta x}$ → 2nd order (central)
- $\frac{f_{i+1} - f_i}{\Delta x}$ → 1st order (forward)
- $\frac{f_{i+2} - 2f_{i+1} + f_i}{(\Delta x)^2}$ → Usually 1st or 2nd order

## 3. Taylor Series Term Identification

### Standard Numbering Convention
- **Term 1:** $f(x)$ (constant term)
- **Term 2:** $f'(x) \cdot s$ (first derivative term)
- **Term 3:** $\frac{f''(x)}{2!} s^2$ (second derivative term)
- **Term 4:** $\frac{f'''(x)}{3!} s^3$ (third derivative term)

### Key Formula for MCQs
For $f(x + s)$ where $s = n\Delta x$:
$$f(x + n\Delta x) = \sum_{k=0}^\infty \frac{f^{(k)}(x)}{k!} (n\Delta x)^k$$

**Trick:** The "$k$-th derivative term" has coefficient $\frac{f^{(k)}(x)}{k!}$

## 4. Error Type Recognition

### Dissipative vs Dispersive Errors
**Dissipative Error:**
- Caused by **even-order** truncation terms
- Effect: Smooths solutions (numerical diffusion)
- Look for: $\frac{\partial^2}{\partial x^2}$, $\frac{\partial^4}{\partial x^4}$ terms

**Dispersive Error:**
- Caused by **odd-order** truncation terms  
- Effect: Creates oscillations/wiggles
- Look for: $\frac{\partial^3}{\partial x^3}$, $\frac{\partial^5}{\partial x^5}$ terms

## 5. Scheme Recognition Shortcuts

### Common Scheme Properties
**FTCS (Forward Time, Central Space):**
- Time: Forward difference → 1st order in time
- Space: Central difference → 2nd order in space
- Stability: Conditionally stable

**DuFort-Frankel:**
- 2nd order accurate in both time and space
- Unconditionally stable
- **Trick:** If you see "DuFort-Frankel," mark stable + 2nd order

**ADI (Alternating Direction Implicit):**
- For 2D: 2 fractional steps per time step
- For 3D: 3 fractional steps per time step
- Generally more stable than explicit

## 6. Mesh and Discretization Tips

### Finite Volume Method Recognition
- **Cell-centered:** Solutions defined at cell centers
- **Node-based:** Solutions defined at vertices
- **Conservative:** Fluxes balanced across faces

### Influence Patterns
- **Upstream/Downstream influence:** Equally weighted in central schemes
- **Stencil size:** More points → potentially higher order

## 7. Quick MCQ Strategy

### Step-by-Step Approach
1. **Identify scheme type** (explicit/implicit, forward/central/backward)
2. **Check stability** (look for conditions on $\Delta t$)
3. **Determine accuracy** (count derivatives, check Taylor expansion)
4. **Recognize error types** (even terms = dissipative, odd = dispersive)

### Common MCQ Patterns
- "Which is unconditionally stable?" → Look for implicit schemes
- "Order of accuracy?" → Do Taylor expansion or recognize pattern
- "Third term in series?" → Count carefully from constant term
- "Conservative scheme?" → Finite volume with flux balance

### Red Flags to Avoid
- Don't confuse "third derivative term" with "third term"
- Explicit schemes are rarely unconditionally stable
- Higher order doesn't always mean more stable
- CFL conditions are necessary for stability, not sufficient

## 8. Memory Aids

**STABLE acronym:**
- **S**cheme type (explicit/implicit)
- **T**aylor expansion for accuracy
- **A**mplification factor check
- **B**oundary conditions matter
- **L**eading error term
- **E**ven/odd terms for error type
---

hi hello 123
