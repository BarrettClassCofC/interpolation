Math 445/545 Project
Designing a Battery Percentage Indicator Using Interpolation
Overview

Portable electronic devices typically display an estimate of the remaining battery charge as a percentage between 
0
%
 and 
100
%
. The device cannot measure this percentage directly. Instead, it must infer the battery's state of charge from measurable quantities.

One simple approach is to estimate the state of charge from the battery voltage. The relationship between voltage and remaining charge is nonlinear, so a battery-management system can use experimentally measured calibration data together with interpolation to estimate the battery percentage at voltages that were not measured directly.

For this project, the battery state of charge is given by 
𝑆
(
𝑉
)
, where 
𝑉
 is the measured battery voltage.

A battery-percentage indicator should satisfy several basic physical requirements. The displayed percentage should satisfy

0
≤
𝑆
(
𝑉
)
≤
100.

Increasing voltage should not result in a lower predicted battery percentage, so we expect the indicator should be monotonically increasing:

𝑆
′
(
𝑉
)
≥
0.

We expect the percentage should be relatively stable in the measured voltage. That is, a very small change in measured voltage should not produce an unreasonable change in the displayed percentage.

Calibration Data

The following dataset consists of voltage--charge pairs collected during a battery experiment.

Voltage 
𝑉
 (V)	State of Charge 
𝑆
 (%)
3.30	0
3.38	4
3.45	9
3.52	15
3.58	22
3.63	31
3.68	42
3.73	54
3.78	65
3.83	74
3.89	82
3.96	89
4.04	95
4.12	100
Part I: Construct the Interpolants

Using the calibration data, construct each of the following interpolation models:

Piecewise linear interpolant
Global polynomial interpolant
Cubic spline interpolant

Create a single figure showing each interpolant along with the original calibration data. Evaluate the interpolants on a sufficiently fine voltage grid so that their behavior between calibration points can be clearly seen. Your figure must include appropriate axis labels, units, a legend, and a title.

Of the previous interpolants, determine the best fit considering the interpolant's range and monotonicity.

Part II: Predicting Battery Percentage

Suppose a device measures the following battery voltages:

3.41
,
3.55
,
3.70
,
3.76
,
3.92
,
4.08
 V
.

For each voltage, calculate the predicted battery percentage using all interpolation methods.

Present your results in a table. Answer the following questions:

At which test voltage do the interpolation methods disagree the most?
At which test voltage do they agree most closely?
Are the differences practically significant for a battery display?
Part III: Voltage Measurement Error

The voltage measurement is not exact. Assume the voltage sensor has an uncertainty of

±
0.010
 V
.

Therefore, when the device reports a voltage 
𝑉
𝑚
, the actual battery voltage may lie in

𝑉
𝑚
−
0.010
≤
𝑉
≤
𝑉
𝑚
+
0.010.

Use the interpolation method that you currently consider most appropriate for the battery gauge.

For each of the measured voltages

3.45
,
3.60
,
3.75
,
3.90
,
4.05
 V
,

determine the corresponding range of possible battery percentages.

Define

𝑆
min
⁡
=
min
⁡
𝑉
∈
[
𝑉
𝑚
−
0.010
,
𝑉
𝑚
+
0.010
]
𝑆
(
𝑉
)

and

𝑆
max
⁡
=
max
⁡
𝑉
∈
[
𝑉
𝑚
−
0.010
,
𝑉
𝑚
+
0.010
]
𝑆
(
𝑉
)
.

For each measured voltage, report

𝑆
min
⁡
,
𝑆
(
𝑉
𝑚
)
,
𝑆
max
⁡
.

Part IV: Sensitivity Analysis

Small voltage errors can produce different battery-percentage errors depending on the location of the discharge curve.

For sufficiently small 
Δ
𝑉
,

Δ
𝑆
≈
𝑆
′
(
𝑉
)
Δ
𝑉
.

Using your preferred interpolant, calculate and plot

∣
𝑆
′
(
𝑉
)
∣

over the calibration interval. The units of this quantity are percentage points per volt.

Using the sensor uncertainty

∣
Δ
𝑉
∣
=
0.010
 V
,

construct the approximate percentage uncertainty

Δ
𝑆
=
∣
𝑆
′
(
𝑉
)
∣
Δ
𝑉
.

Plot 
Δ
𝑆
 and answer the following questions:

At what approximate voltage is the battery percentage most sensitive to voltage measurement error?
What state of charge corresponds approximately to this voltage?
Where is voltage-based state-of-charge estimation most reliable?
Where is it least reliable?
Explain physically what a large value of 
𝑆
′
(
𝑉
)
 means for the battery indicator.

Suppose the manufacturer would like the battery-percentage indicator to have no more than approximately 
±
2
 percentage points of uncertainty resulting from the voltage sensor.

Using the approximations

∣
Δ
𝑆
∣
≈
∣
𝑆
′
(
𝑉
)
∣
 
∣
Δ
𝑉
∣
,

∣
Δ
𝑉
∣
=
0.010
 V
,

determine the voltage intervals over which

0.010
∣
𝑆
′
(
𝑉
)
∣
≤
2

is satisfied.

Translate these voltage intervals into approximate state-of-charge intervals.

Based on this model and sensor accuracy, can voltage alone provide a uniformly accurate battery-percentage estimate over the entire discharge range? Explain your conclusion.

Part V: Low-Battery Warning Thresholds

Suppose the device displays two warnings:

Low Battery: 
20
%
Critical Battery: 
5
%

Using each interpolation method, numerically solve

𝑆
(
𝑉
)
=
20

and

𝑆
(
𝑉
)
=
5.

Report the predicted threshold voltages.

For each warning threshold, calculate the spread between the largest and smallest predicted voltage among the interpolation methods.

Answer the following questions:

Are the warning voltages sensitive to interpolation method?
Which warning threshold appears more sensitive?
Would a difference of 
10
--
20
 mV be important given the sensor uncertainty?
How should this uncertainty influence the design of a warning system?
Part VI: Simulated Battery Discharge

During operation, suppose the device records the following voltages.

Time (min)	Measured Voltage (V)
0	4.10
30	4.04
60	3.98
90	3.92
120	3.86
150	3.81
180	3.76
210	3.71
240	3.66
270	3.61
300	3.56
330	3.50
360	3.44
390	3.37

Using your recommended battery-percentage interpolation method:

Estimate the battery percentage at every recorded time.
Plot estimated battery percentage versus time.
Estimate the time at which the battery reaches 
50
%
.
Estimate when the 
20
%
 low-battery warning should occur.
Estimate when the 
5
%
 critical warning should occur.

The requested threshold times will generally lie between recorded measurements. Use interpolation and, where appropriate, root-finding rather than simply selecting the closest recorded time.

Final Deliverables

Produce a short write-up that describes your answers to the above questions. The answers should be accompanied by plots as necessary. Make sure the plots have axes labeled and units provided.

All code that produced the plots and was used to answer the questions should be included.

Your submission should include:

A typed/written report containing analysis, figures, tables, and conclusions.
All source code required to produce your results.
Any additional data files used by your programs.

The report should be understandable without requiring the reader to inspect your source code.

Use of Artificial Intelligence

You are permitted and encouraged to use any generative AI tools for this assignment, including for:

Programming assistance
Debugging
Syntax questions
Plotting
Explanations of numerical algorithms

However, you are responsible for ensuring correctness of the code. Make sure your plots and results pass basic sanity checks, such as requisite smoothness or interpolation conditions. You can test your code on simpler problems to ensure they provide correct results.

Your submitted analysis and conclusions must be supported by your computed results. Your report should demonstrate that you understand:

What your program computes
Why the numerical methods behave as they do
What conclusions can legitimately be drawn from the results

You may be asked to explain or modify portions of your code or analysis.
