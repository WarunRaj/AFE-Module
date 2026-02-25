# AFE-Module
Analog Front-End (AFE) design for precision sensor interfacing. Features a 3-stage Op-Amp topology: active low-pass filtering, 11x non-inverting gain, and 0.9V DC biasing for 3.3V ADC compatibility. Optimized for low-power applications [1-10mV noisy signal] with verified signal integrity via real-time SPICE simulation.

# Industrial-Grade Analog Sensor Front-End & Logic System 🚀

## Project Overview
This project demonstrates the design and simulation of a dual-stage Analog Sensor Front-End (AFE) coupled with a Digital Decision Logic stage. 
The system bridges the gap between low-level physical sensors (µV–mV domain) and modern digital control systems such as Microcontrollers and ADCs.
A noisy, low-voltage sensor signal in the range of 1–10 mV is conditioned and converted into a clean, logic-compatible output (0–3.3 V).

## Key Objectives
- Safely interface low-voltage analog sensors with digital systems
- Achieve high gain without instability using staged amplification
- Suppress noise and EMI using analog filtering
- Provide real-time hardware-level decision logic
- Validate system behavior under fault and overvoltage conditions

## System Architecture
The system is divided into two primary functional phases:

### Phase 1: Analog Signal Conditioning
This stage conditions the raw sensor output so it can be interpreted reliably by the digital system. At the input, a 1 kΩ current-limiting resistor together with dual Schottky diode rail clamps to 0–5 V protects the analog front end from overvoltage spikes, accidental high-voltage connections, electrostatic discharge, and other transient faults. The signal is then amplified using a dual-stage architecture, where the total gain is split across two cascaded amplifier stages. Each stage provides a gain of 18.2×, resulting in an overall system gain of approximately 330× (about 50.4 dB). Using staged gain improves stability, preserves bandwidth by operating within the op-amp’s gain-bandwidth product, minimizes unnecessary noise amplification, and prevents early saturation of the amplifiers. Finally, noise is reduced using a passive RC low-pass filter with a cutoff frequency of approximately 159 Hz, which suppresses high-frequency electromagnetic interference, switching noise, and environmental disturbances before the signal is digitized.

### Phase 2: Digital Decision Logic
This stage provides hardware-level automation without introducing firmware latency. An op-amp is configured as a comparator with a 2.5 V reference, producing a digital HIGH whenever the input signal exceeds the defined threshold. The comparator output directly drives hardware automation elements such as an LED, alarm, or interrupt line, enabling immediate fault alerts, safety cutoffs, and autonomous decision-making independent of software execution.

## Technical Specifications

| Parameter | Specification |
|--------|-------------|
| Input Voltage Range | 1 mV – 10 mV |
| Output Voltage Range | 0.33 V – 3.3 V |
| Total Gain | ≈ 330× (50.4 dB) |
| Filter Cutoff Frequency | ~159 Hz |
| Supply Voltage | 5 V |

## Simulation & Verification
The system was designed and verified using the Falstad Circuit Simulator.

### Simulation Tests Performed

**! DC Sweep Analysis**

*Verified linear amplification:*

- 1 mV → 0.33 V

- 10 mV → 3.3 V

*Confirmed absence of saturation and clipping*


**! Fault Injection Test**

*Applied 10 V at the input*

*Protection diodes clamped voltage to ~5.7 V*

*Op-amp inputs remained within safe limits*


**! Comparator Validation**

*Verified LED triggers only when*

- Input > 7.5 mV

- Output > 2.5 V reference

## Hardware Implementation Recommendations

For real-world prototyping and testing:

**Op-Amps**

- LM358 (Dual, cost-effective)

- MCP6002 (Rail-to-rail, low power)

**Protection Diodes**

- BAT54S Schottky diodes

- Low forward voltage drop

- Fast transient response

**Passive Components**

- 1% tolerance metal film resistors

- Improves gain accuracy and repeatability

**Power Supply**

- Regulated 5 V single-rail

- Decoupling capacitors strongly recommended

## Applications

- Industrial sensor interfaces
- Embedded data acquisition systems
- Space science instrumentation education
- Safety-critical threshold detection
- Low-level analog signal processing

## 📜 License
This project is released for educational and research purposes.
You are free to study, modify, and extend it with proper attribution.

## 🤝 Contributions
Contributions, improvements, and discussions are welcome, especially in:

- Noise optimization
- Precision sensing
- Radiation-hardened design
- Space-grade electronics adaptations
