# Suresh et al. 2026 - Minimal observables for discriminating laser cavity solitons in a microresonator-filtered fibre laser
Optical Materials Express, Vol. 16, Issue 6, pp 1782-1795

## Sections read:
Read: Abstract, Section 2, Section 1 skimmed

## Summary
Key concepts:
- laser cavity solitons are defined by the control parameters of the system
- discrimination of soliton states were determined based on these parameters - updated: incorrect, states were discriminated by metrics calculated at each pump x delay cell


### CONTINUED READING ON 25-10-2026
## System Overview
- laser cavity solitons (LCS) consists of a microcavity nested within an amplifying fibre loop
- a 976nm laser diode pumps an erbium fibre amplifier. Microresonator is pumped directly by the amplifier, no external coherent pump laser needed
- 4-port, 50GHz silicon-oxynitride microresontor with anomalous dispersion and Kerr nonlinearity (see 'pasquazi2019_microcomb_review.md'), supporting bright temporal solitons 
- laser cavity is closed through the drop port, output is taken from through port
- gain path is decoupled from the Kerr microresonator, comb bandwidth is not limited by the gain bandwidth 

## Control Parameters
- states depend on amplifier pump power and total cavity delay length
- parameters are scanned systematically to build heatmap dataset
- diagnostics used are optical spectrum analyser (OSA) and photodetector + oscilloscope (OSC)
- metrics are extracted to optical bandwidth and RF bandwidth 

## Discriminator 
- optical and RF information is processed and assigned to each data index
- classified as solitons, continuous-wave (CW) or unstable 
- uses predefined thresholds derived from statistical distribution of data

## Physics Points
- solitons are stabilised via dissipative coupling between Kerr ring and gain cavity
- access to solitons is affected by slow nonlinearities: erbium gain saturation and thermal effects in the fibre and ring
 