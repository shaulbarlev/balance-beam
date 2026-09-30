# Balance beam

Two weights on a rigid rod, pinned in the middle. Drag either weight to any
angle, let go, and watch what happens.

**It stays where you put it.** With equal masses on equal arms the two gravity
torques cancel at *every* angle, so the net torque is identically zero — there
is nothing pulling the beam back to horizontal. That is neutral equilibrium,
and it is what the simulator was built to check.

Nothing here is animated by hand: it integrates the rigid body's equation of
motion (`I·θ̈ = τ`) at 480 Hz with a semi-implicit Euler step, which conserves
energy properly, so "it holds the angle" is a result rather than a decision.

## Things to try

| | |
|---|---|
| **neutral** | the experiment itself — drop it anywhere, it holds |
| **heavy rod** | a 300 g rod instead of 20 g. Still holds every angle: a uniform rod is symmetric about the pin, so its weight makes no torque. Press **nudge** and you feel what it *did* change — the same push now reaches half the spin, because inertia went up |
| **scale** | raise the pin above the rod and it becomes a real balance: level is now the one stable angle, and a 2 g difference between the weights tilts it to a steady 6° — the reading of a weighing scale |
| **top-heavy** | drop the pin below the rod and level turns into a pencil balanced on its point |

**nudge** applies the same angular impulse every time, so it is an inertia
meter you can feel: spin = impulse / I.

## The physics

Body frame: rod along *x*, origin at the rod's centre, pin at `(0, d)`.

- centre of mass along the rod: `s = ARM·(mA − mB) / M`
- about the pin: `I = mA·ARM² + mB·ARM² + m_rod·L²/12 + M·d²`
- gravity torque: `τ = −M·g·(s·cos θ + d·sin θ) = −M·g·R·sin(θ + φ)`,
  with `R = √(s² + d²)` and `φ = atan2(s, d)`

So the beam rests at `θ = −φ` and swings with period `2π√(I / M g R)` — and
when `R = 0`, meaning the centre of mass sits exactly on the pin, there is no
resting angle at all. Every angle is a resting angle.

## Running it

One file, no build, no dependencies: open `public/index.html`. Built for iOS Safari —
pointer events, `touch-action: none`, safe-area insets, dynamic viewport
height.
