<h2>Description</h2>
This project entails optimizing a trajectory for an interplanetary rendezvous mission to Comet 29P (Schwassmann-Wachmann 1). I designed this mission to explore the limits of high-efficiency Nuclear Electric Propulsion (NEP) and to demonstrate how a constant, low-thrust engine can navigate the vast distances of the outer solar system.

## 1. Project Overview & Motivation

Interplanetary missions typically rely on impulsive burns from chemical rockets. However, missions to targets like Comet 29P (at 5.79 AU) require enormous energy changes. I chose this project to investigate the Indirect Method of trajectory optimization, which allows for a high-precision solution by treating the flight path as a mathematical minimization problem.
<br />

* **The Mission:** Launch from Earth on December 4, 2032.
* **The Objective:** Maximize the final dry mass delivered to the comet.
* **The Constraint:** Match both the position and velocity of the comet at rendezvous.

## 2. Mathematical Methodology

I formulated the mission using Pontryagin’s Minimum Principle (PMP) to derive the necessary conditions for an optimal path.

### The Hamiltonian and Euler-Lagrange Equations
By defining a Hamiltonian ($H$), I linked the system's dynamics (position and velocity) with costates (Lagrange multipliers). The governing equation was derived as:

$$H = \lambda_r(u) + \lambda_{\theta}\left(\frac{v}{r}\right) + \lambda_u\left(\frac{v^2}{r} - \frac{\mu}{r^2} + \frac{T\sin\alpha}{m}\right) + \lambda_v\left(-\frac{uv}{r} + \frac{T\cos\alpha}{m}\right)$$

### The Optimal Control Law
The steering angle ($\alpha$) was optimized by finding the point where the partial derivative of the Hamiltonian with respect to the angle is zero. This mathematical proof shows that the thrust must always be directed along the Primer Vector (the velocity costate vector) to maximize efficiency.

## 3. MATLAB Implementation

The core of the project involved a Two-Point Boundary Value Problem (TPBVP) solved via a Shooting Method.
<br />

* **Canonical Units:** To ensure numerical stability, I transformed all distances and times into canonical units, preventing the large magnitudes of interplanetary space from causing solver failures.
* **Target Dynamics:** Because Comet 29P is in a moving orbit, the MATLAB script dynamically calculates the comet's position at the end of the guessed flight time to ensure a precise intercept.

## 4. Mission Results and Comparisons

I analyzed two distinct scenarios: an "Engines Only" baseline and a configuration incorporating Solar Radiation Pressure (SRP).

### Performance Metrics
The solver converged on an optimal trajectory with a 3.83-year flight time.
<br />

* **Dry Mass:** Delivered 1,990 kg to the comet (approx. 40% of initial mass).
* **Total $\Delta V$:** Executed a massive $37\text{ km/s}$ change in velocity.

### Key Insights
* **The Oberth Effect:** The optimized trajectory "dives" toward the Sun before spiraling outward. By thrusting deeper in the Sun's gravity well, the spacecraft maximizes mechanical energy gain per unit of propellant.
* **SRP Impact:** My analysis proved that at 1N of thrust, SRP forces are negligible (four orders of magnitude smaller than the engine), yielding virtually identical results to the baseline.

<p align="center">
  <img src="https://i.imgur.com/nqTby0X.png" height="80%" width="80%" alt="Mission Characteristics and Convergence Errors"/>
  <br />
  <i>Figure 4-1: Detailed Mission Characteristics and Convergence Errors</i>
</p>

<p align="center">
  <img src="https://i.imgur.com/DUUlzht.png" height="80%" width="80%" alt="Engines Only Heliocentric Trajectory"/>
  <br />
  <i>Figure 4-2: Option 1: Engines Only Heliocentric Trajectory</i>
</p>

<p align="center">
  <img src="https://i.imgur.com/cxQNFEG.png" height="80%" width="80%" alt="Engines and SRP Mission Characteristics"/>
  <br />
  <i>Figure 4-3: Option 2: Engines + SRP Mission Characteristics</i>
</p>

<p align="center">
  <img src="https://i.imgur.com/k9VagNo.png" height="80%" width="80%" alt="Engines and SRP Heliocentric Trajectory"/>
  <br />
  <i>Figure 4-4: Option 2: Engines + SRP Heliocentric Trajectory</i>
</p>

## 5. Conceptual Sample Return Architecture

I additionally developed a conceptual architecture for a Sample Return Mission. This expands the problem into a multi-phase optimization:
<br />

* **Outbound Leg:** Earth to Comet rendezvous.
* **Waiting Phase:** Accounting for the comet's motion during a 2-year science stay.
* **Inbound Leg:** Return to Earth with mass continuity (accounting for collected samples).

This would require a Multiple Shooting Method to link mass and fuel usage across the entire round trip simultaneously.
