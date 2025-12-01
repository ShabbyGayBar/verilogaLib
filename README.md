# Verilog-AMS Library

This repository contains a collection of Verilog-AMS models for various electronic components and systems. The models are designed for use in circuit simulation tools that support the Verilog-AMS language.

---

## Module Overview

### 1. `amp_dynamic`
- **Function:** Dynamic amplifier with clocked operation and reset. Amplifies the differential input on clock edge, then holds output.
- **Inputs:**
  - `clk`: Clock input (starts amplification on rising edge)
  - `rst`: Reset input (active high)
  - `inp`, `inm`: Differential analog inputs
- **Outputs:**
  - `done`: Indicates amplification complete
  - `outp`, `outm`: Differential analog outputs
- **Parameters:**
  - `tamp`: Amplification time (default: 10u)
  - `gain`: Amplifier gain (default: 8)
  - `vcm`: Common mode output voltage (default: 2.5)
  - `offset`: Input-referred offset voltage (default: 0)
  - `vlogic_high`: Logic high voltage (default: 5)
  - `vtrans`: Clock threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 2. `dff_rsn`
- **Function:** D flip-flop with asynchronous reset and set.
- **Inputs:**
  - `clk`: Clock input
  - `d`: Data input
  - `_rst`: Asynchronous reset (active low)
  - `_set`: Asynchronous set (active low)
- **Outputs:**
  - `q`: Output
  - `_q`: Complementary output
- **Parameters:**
  - `vlogic_high`: Logic high voltage (default: 5)
  - `vlogic_low`: Logic low voltage (default: 0)
  - `vtrans_clk`: Clock threshold voltage (default: 2.5)
  - `vtrans`: Data/reset/set threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 3. `comparator_dynamic`
- **Function:** Dynamic comparator. Compares differential input on clock edge, outputs logic high/low accordingly, and resets on clock fall.
- **Inputs:**
  - `clk`: Clock input (triggers comparison on rising edge, reset on falling edge)
  - `inp`, `inm`: Differential analog inputs
- **Outputs:**
  - `outp`, `outm`: Differential digital outputs
    - **Note:** Both outputs are logic high during reset (after clock falling edge).
- **Parameters:**
  - `offset`: Input-referred offset voltage (default: 0)
  - `vlogic_high`: Logic high voltage (default: 5)
  - `vlogic_low`: Logic low voltage (default: 0)
  - `vtrans_clk`: Clock threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 4. `tah_ideal`
- **Function:** Ideal track-and-hold circuit. Tracks input when clock is high, holds output when clock is low.
- **Inputs:**
  - `clk`: Clock input (track when high, hold when low)
  - `in`: Analog input
- **Inout:**
  - `out`: Analog output (bidirectional for charge sharing)
- **Parameters:**
  - `ron`: On-resistance during track mode (default: 25)
  - `vtrans_clk`: Clock threshold voltage (default: 2.5)

### 5. `adc_16bit_ideal`
- **Function:** Ideal 16-bit analog-to-digital converter. Converts analog input to 16-bit digital output on clock edge.
- **Inputs:**
  - `in`: Analog input
  - `clk`: Clock input (conversion on rising edge)
- **Outputs:**
  - `out[15:0]`: 16-bit digital output bus
- **Parameters:**
  - `vref`: Reference voltage for full-scale input (default: 1.0)
  - `vlogic_high`: Logic high voltage (default: 5)
  - `vlogic_low`: Logic low voltage (default: 0)
  - `vtrans_clk`: Clock threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 6. `dac_16bit_ideal`
- **Function:** Ideal 16-bit digital-to-analog converter. Converts 16-bit digital input to analog output.
- **Inputs:**
  - `in[15:0]`: 16-bit digital input bus
- **Outputs:**
  - `out`: Analog output
- **Parameters:**
  - `vref`: Reference voltage for full-scale output (default: 1)
  - `vtrans`: Input threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 7. `ohmmeter`
- **Function:** Measures resistance and conductance of a device under test (DUT). The DUT should be connected as follows:
  - Connect the DUT's positive terminal to `dutp`
  - Break the connection between the DUT's negative terminal and the rest of the circuit
  - Connect the DUT's negative terminal to `iprobe`
  - Connect the rest of the circuit to `dutm`
- **Inputs:**
  - `dutp`, `iprobe`: DUT voltage and current probe
- **Outputs:**
  - `dutm`: DUT negative terminal
  - `r`: Measured resistance output
  - `g`: Measured conductance output
- **Parameters:**
  - `max_resistance`: Maximum reported resistance (default: 1k)
  - `min_resistance`: Minimum reported resistance (default: -1)
  - `max_conductance`: Maximum reported conductance (default: 1)
  - `min_conductance`: Minimum reported conductance (default: -1)

### 8. `pfd`
- **Function:** Phase-frequency detector. Detects phase and frequency difference between two clock signals.
- **Inputs:**
  - `ref`: Reference clock input
  - `fb`: Feedback clock input
- **Outputs:**
  - `up`: Output pulse when `ref` leads `fb`
  - `down`: Output pulse when `fb` leads `ref`
- **Parameters:**
  - `vlogic_high`: Logic high voltage (default: 5)
  - `vtrans`: Input threshold voltage (default: 2.5)
  - `tdel`: Output delay (default: 3u)
  - `trise`, `tfall`: Output rise/fall times (default: 1u)

### 9. `ramp_gen`
- **Function:** Generates a linear voltage ramp from rising edge of `clk` with a slope defined by `slope`.
- **Inputs:**
  - `clk`: Clock signal (resets ramp)
- **Outputs:**
  - `ramp`: Ramp voltage output
- **Parameters:**
  - `vrst`: Starting voltage of the ramp (default: 0)
  - `vtrans_clk`: Clock threshold voltage (default: 2.5)
  - `slope`: Slope of the ramp in V/s (default: 5e6)

---

## License

This mod is under [MIT LICENSE](LICENSE).
