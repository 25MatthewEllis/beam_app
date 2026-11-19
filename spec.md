# Beam Designer

## Purpose
Analyze simply supported, cantilever, and overhanging beams under upward or
downward point and uniform loads. Show shear, moment, and deflection diagrams,
and check bending stress and deflection against specified limits. This is a
preliminary calculator, not a code-compliant design tool.

## Inputs
- Unit system: prominent US customary/metric toggle at the top of the app; US customary is the default. Users may switch at any time. Switching converts entered values and displayed results/diagram labels without changing the physical beam. Use ft, kip, and kip/ft for US customary, or m, kN, and kN/m for metric.
- Support: simply supported, cantilever, or overhanging beam with two simple supports; default to simply supported. Use a selector.
- Span: numeric field with a unit label; greater than zero, with the maximum TBD. The opening example uses 20 ft. For an overhanging beam, this is the support-to-support span; enter left and right overhangs separately.
- Overhangs: for an overhanging beam, choose left, right, or both sides with a selector, then enter the active overhang length(s) as nonnegative values. Default to a 5 ft (1.524 m) right overhang; numerical maximum TBD. Show both support positions on the total beam, inset from the ends by the selected lengths.
- Loads: use repeatable rows with add/remove controls; maximum number of rows TBD.
  - Point load: positive magnitude in kip or kN, position from the left beam end in ft or m (0 to total beam length), and an up/down direction selector. Default direction is downward and default position is midspan. Magnitude range/default TBD. No point load is present in the opening example.
  - Uniform load: positive intensity in kip/ft or kN/m, a loaded interval in ft or m (within 0 to total beam length), and an up/down direction selector. The opening example uses a downward 1 kip/ft load over the full span; other magnitude limits are TBD.
- Beam section: choose a steel W-shape or lumber size from a catalog, or enter a custom section. The starter catalog includes W12x26 steel grade A992 and Douglas Fir-Larch No. 2 nominal 2x4 through 2x12 lumber sizes. Expand the catalog later. Show a cross-section preview in the left input column.
  - Catalog and custom sections must provide strong-axis section modulus Sx for bending stress, moment of inertia Ix for deflection, elastic modulus E, allowable bending stress Fb, material identity/grade, and weight per length. Lumber entries must identify species and grade.
  - Source steel shape geometry and weight from the AISC Shapes Database v16.0. Source lumber design properties from the AWC 2024 NDS Supplement, including its 2026-09-17 addendum.
  - Populate Douglas Fir-Larch No. 2 catalog sections with reference E = 1,600 ksi and Fb = 0.90 ksi from NDS Supplement Table 4A. Compute Sx and Ix from the assumed dressed dimensions. Estimate weight per length from Table 1 specific gravity 0.50 using an oven-dry density assumption, and clearly disclose that actual weight varies with moisture.
  - Record the exact source, edition, and table for each catalog value. Store a supplied/curated Fb per entry; do not calculate code-specific allowables. The source and assumptions for the steel Fb value remain TBD.
  - Custom sections require numeric fields for Sx, Ix, E, and Fb. Use in^3, in^4, ksi, and kip/ft for US customary; use mm^3, mm^4, MPa, and kN/m for metric. A section label/material identity is also required.
- Beam self-weight: user toggle, on by default. Catalog entries and any custom section used while this toggle is on must provide weight per length; include it in analysis and report it separately from applied loads. Do not draw self-weight as an applied load in the beam sketch.
- All numeric inputs must be finite. Span must be greater than zero; point-load positions and uniform-load intervals must remain within the beam. Numerical ceilings and load magnitude limits are TBD.

## Calculations
- Use upward force as positive, downward force as negative, positive internal shear as upward on the left face, and positive bending moment as sagging.
- Calculate reactions, shear, and moment from statics. Sum entered loads and enabled self-weight linearly; do not apply load factors.
- Calculate deflection with a linear-elastic, small-deflection Euler-Bernoulli beam model; ignore shear deformation.
- For an overhanging beam, use two simple supports at the entered overhang offsets, calculate reactions by statics, and enforce zero deflection at both supports. Use the support-to-support span as L for the L/360 reference.
- Calculate bending stress fb = M/Sx along the beam and compare the maximum absolute stress to the supplied/curated Fb. A pass requires the maximum not to exceed Fb.
- Compare maximum absolute deflection under total applied load to L/360. For a simply supported beam, L is the support-to-support span; for a cantilever, L is the fixed-end-to-free-end length.
- When enabled, include beam self-weight in the total applied load.

## Outputs
- The beam with its loads, and shear, moment, and deflection diagrams with labeled units.
- An exaggerated deflected beam shape directly below the beam/load sketch, updated whenever inputs change and labeled as not to scale.
- Support reactions, maximum shear and moment, maximum deflection, calculated bending stress, applicable reference limits, and ratios to those limits. Do not label the beam safe or show an overall pass/fail verdict.
- Use kip, ft, kip-ft, in, and ksi for US customary results; use kN, m, kN-m, mm, and MPa for metric results.
- Interactive diagrams show the position and value at the cursor.
- Use a distinct color for each response diagram, fill between each curve and
  its zero axis, and label its maximum and minimum values on the plot.
- Provide a print view that users can save as PDF, including inputs, diagrams, and results.
- Prominently state that the results are educational/preliminary and are not for approving a real beam design. The app does not check shear capacity, buckling, connections, or code load combinations.

## Look and feel
Clean and professional, with a prominent unit toggle at the top and an
example beam loaded when it opens. The example uses the default self-weight
setting, which is on.
- Use a subtle warehouse-inspired background while keeping the controls and
  results panels high-contrast and easy to read.
- Keep the cross-section preview in the left input column. Show reactions,
  calculated information, and comparisons in the left input column below the
  applied-load controls; put the loaded-beam sketch on the right, with shear,
  moment, and deflection diagrams stacked directly below it. On narrow screens,
  stack these areas vertically.

## Validation
20 ft simply supported W12x26 with 1 kip/ft and self-weight off:
M = 50.0 kip-ft,
deflection 0.609 in.
Add independently checked cases for self-weight on, point loads, a
cantilever, a lumber section, custom section properties, and metric inputs;
expected values are TBD.

## Out of scope
Continuous beams, buckling, and shear-strength checks. The shear diagram is
reported, but shear capacity is not checked.