## Designing a Battery Percentage Indicator Using Interpolation

---

## Overview

Portable electronic devices typically display an estimate of the remaining battery charge as a percentage between $0\%$ and $100\%$.

The device cannot measure this percentage directly. Instead, it must infer the battery's *state of charge* from measurable quantities.

One simple approach is to estimate the state of charge from the battery voltage. The relationship between voltage and remaining charge is nonlinear, so a battery-management system can use experimentally measured calibration data together with interpolation to estimate the battery percentage at voltages that were not measured directly.

For this project, the battery state of charge is given by $S(V)$ where $V$ is the measured battery voltage.

A battery-percentage indicator should satisfy several basic physical requirements. The displayed percentage should satisfy

$$0 \leq S(V) \leq 100.$$ 

Increasing voltage should not result in a lower predicted battery percentage, so we expect the indicator should be monotonically increasing.

$$S'(V) \geq 0.$$

We expect the percentage should be relatively stable in the measured voltage. That is, a very small change in measured voltage should not produce an unreasonable change in the displayed percentage.

## Calibration Data

| Voltage V (V) | State of Charge S (%) |
|---:|---:|
|3.30|0|
|3.38|4|
|3.45|9|
|3.52|15|
|3.58|22|
|3.63|31|
|3.68|42|
|3.73|54|
|3.78|65|
|3.83|74|
|3.89|82|
|3.96|89|
|4.04|95|
|4.12|100|

## Part I: Construct the Interpolants

Using the calibration data, construct each of the following interpolation models.

- Piecewise linear interpolant
- Global polynomial interpolant
- Cubic spline interpolant

Create a single figure showing each interpolant along with the original calibration data. Evaluate the interpolants on a sufficiently fine voltage grid so that their behavior between calibration points can be clearly seen. Your figure must include appropriate axis labels, units, a legend, and a title.

Of the previous interpolants, determine the best fit considering the interpolant's range and monotonicity.

## Part II: Predicting Battery Percentage

Suppose a device measures the following battery voltages:

$$3.41,\qquad3.55,\qquad3.70,\qquad3.76,\qquad3.92,\qquad4.08\text{ V}. $$

For each voltage, calculate the predicted battery percentage using all interpolation methods. Present your results in a table. Answer the following questions:

1. At which test voltage do the interpolation methods disagree the most?
2. At which test voltage do they agree most closely?
3. Are the differences practically significant for a battery display?

## Part III: Voltage Measurement Error

The voltage measurement is not exact. Assume the voltage sensor has an uncertainty of $\pm 0.010$ V.

Use the interpolation method that you currently consider most appropriate for the battery gauge. For each measured voltage 3.45, 3.60, 3.75, 3.90, and 4.05 V, determine the corresponding range of possible battery percentages.

Report $S_{min}$, $S(V_m)$, and $S_{max}$.

## Part IV: Sensitivity Analysis

For sufficiently small $\Delta V$,

$$\Delta S \approx S'(V)\Delta V.$$

Using your preferred interpolant, calculate and plot $|S'(V)|$ over the calibration interval.

Construct the approximate percentage uncertainty

$$\Delta S = |S'(V)|\Delta V.$$

Answer:

1. At what approximate voltage is the battery percentage most sensitive to voltage measurement error?
2. What state of charge corresponds approximately to this voltage?
3. Where is voltage-based state-of-charge estimation most reliable?
4. Where is it least reliable?
5. Explain physically what a large value of $S'(V)$ means for the battery indicator.

Suppose the manufacturer would like the battery-percentage indicator to have no more than approximately ±2 percentage points of uncertainty resulting from the voltage sensor. Determine the voltage intervals over which the requirement is satisfied and translate these intervals into approximate state-of-charge intervals.

## Part V: Low-Battery Warning Thresholds

Suppose the device displays two warnings:

- **Low Battery:** 20%
- **Critical Battery:** 5%

Using each interpolation method, numerically solve $S(V)=20$ and $S(V)=5$.

Report the predicted threshold voltages. For each warning threshold, calculate the spread between the largest and smallest predicted voltage among the interpolation methods.

Answer:

1. Are the warning voltages sensitive to interpolation method?
2. Which warning threshold appears more sensitive?
3. Would a difference of 10–20 mV be important given the sensor uncertainty?
4. How should this uncertainty influence the design of a warning system?

## Part VI: Simulated Battery Discharge

| Time (min) | Measured Voltage (V) |
|---:|---:|
|0|4.10|
|30|4.04|
|60|3.98|
|90|3.92|
|120|3.86|
|150|3.81|
|180|3.76|
|210|3.71|
|240|3.66|
|270|3.61|
|300|3.56|
|330|3.50|
|360|3.44|
|390|3.37|

Using your recommended battery-percentage interpolation method:

1. Estimate the battery percentage at every recorded time.
2. Plot estimated battery percentage versus time.
3. Estimate the time at which the battery reaches 50%.
4. Estimate when the 20% low-battery warning should occur.
5. Estimate when the 5% critical warning should occur.

Use interpolation and, where appropriate, root-finding rather than simply selecting the closest recorded time.

## Final Deliverables

Produce a short write-up that describes your answers to the above questions. The answers should be accompanied by plots as necessary. Make sure the plots have axes labeled and units provided. All code that produced the plots and was used to answer the questions should be included.

Your submission should include:

1. A typed/written report containing analysis, figures, tables, and conclusions.
2. All source code required to produce your results.
3. Any additional data files used by your programs.

The report should be understandable without requiring me to inspect your source code.

## Use of Artificial Intelligence

You are permitted and encouraged to use any generative AI tools for this assignment, including for programming assistance, debugging, syntax questions, plotting, and explanations of numerical algorithms.

However, you are responsible for ensuring correctness of the code.
'''
path='/mnt/data/README_exact.md'
open(path,'w').write(md)
print(path)
