# Verilog-A Library

This repository contains a collection of Verilog-A models for electronic components and systems. The models are intended for use with circuit simulators that support Verilog-A.

## Module Overview

| Cell | Description |
| --- | --- |
| [`adc_16bit_ideal`](adc_16bit_ideal.va) | Ideal 16-bit analog-to-digital converter that samples its input on a rising clock edge. |
| [`ctle`](ctle.va) | Continuous-time linear equalizer with one zero and two poles. |
| [`dac_16bit_ideal`](dac_16bit_ideal.va) | Ideal 16-bit digital-to-analog converter. |
| [`dff_sr`](dff_sr.va) | D-type flip-flop with asynchronous active-low reset and set. |
| [`pfd`](pfd.va) | Phase-frequency detector with up and down outputs. |
| [`vc_res`](vc_res.va) | Differential-voltage-controlled conductor with configurable conductance limits. |

## License

This project is licensed under the [MIT License](LICENSE).
