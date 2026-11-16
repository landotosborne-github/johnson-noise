# Measuring Boltzmann's Constant with Johnson–Nyquist Noise

**UC Santa Barbara · Physics 128AL (Advanced Lab) · Fall 2022**
Landon Osborne, with lab partner Brian Ly

Every resistor generates thermal noise. Nyquist's theorem ties the noise power directly to temperature:

$$\langle V^2 \rangle = 4 k_B T R \, G$$

where $G$ is the band gain of the measurement chain. This experiment measured that noise in a set of resistors at room temperature and in liquid nitrogen (77 K), then used it to estimate the Boltzmann constant $k_B$ and the temperature of absolute zero.

The same physics sets the noise floor of every RF receiver ($kTB$), which is why this lab is the foundation for receiver sensitivity and link-budget work.

## Method

1. **Signal chain:** resistor → low-noise preamplifier → 3–10 kHz band-pass filter → spectrum analyzer, with linear averaging.
2. **Characterize the system:** measured the amplifier/filter gain $g(f)$ by comparing a white-noise source with and without the chain, then fit it to a Gaussian. Measured the total capacitance of the input (resistor, cable, preamp), since it forms a low-pass filter with $R$.
3. **Band gain:** numerically integrated $G = \int |g(f)|^2 / (1 + (2\pi f C R)^2)\, df$ with error propagated through the fit parameters.
4. **Noise measurements:** recorded noise across several resistances at room temperature and at 77 K, subtracted the system background, and fit $\langle V^2 \rangle$ against $R$ to extract $k_B$ and absolute zero.

## Results

| Condition | Absolute zero | $k_B$ (J/K) |
| --- | --- | --- |
| Room temperature | −226.7 ± 10.5 °C | (1.153 ± 0.049) × 10⁻²³ |
| Liquid nitrogen (77 K) | −259.0 ± 2.7 °C | (1.129 ± 0.048) × 10⁻²³ |
| Accepted value | −273.15 °C | 1.381 × 10⁻²³ |

The results land on the right order of magnitude but fall about 16–18% low on $k_B$, outside the stated uncertainty. The 77 K run came much closer on absolute zero, likely because of the lower background noise. The report traces the gap to unexpected noise sources, under-measured system capacitance, and above all the Gaussian fit to the gain function, which feeds into every result through the band gain. A repeat would average more gain data sets and push to lower temperatures.

## Files

| File | What it is |
| --- | --- |
| `Johnson_Noise_report.pdf` | Full lab report (theory, method, results, error analysis) |
| `Johnson_Noise_notebook.pdf` | Lab notebook |
| `AMPplots.py` | Analysis: gain fit (SciPy `curve_fit`), band-gain integration, noise fits |
| `AMP*.TXT`, `BG*.TXT` | Spectrum analyzer captures: amplified white noise and background |
| `jonsonnoise - *.csv` | Noise vs. resistance at room temperature and 77 K |
| `Plots/` | Gain fit, background and noise-fit figures |

**Tools:** Python (NumPy, Pandas, SciPy, Matplotlib), spectrum analyzer, low-noise preamp, band-pass filter, DMM, LN₂ dewar.
