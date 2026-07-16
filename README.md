# STM32 EV Charger CC-CV Controller

A digital constant-current / constant-voltage (CC-CV) EV charger controller built on STM32, with CAN-based telemetry and EMI-aware PCB design. Developed during a research internship at **CART (Centre for Automotive Research & Tribology), IIT Delhi** (May–July 2026).

---

## Overview

The controller implements a cascaded dual-loop PI control scheme (outer voltage loop, inner current loop) to regulate charging current and voltage delivery, with telemetry sent over FDCAN for monitoring and diagnostics.

## Firmware highlights

- **STM32G474**: dual-loop PI control — outer voltage loop, inner current loop
- Anti-windup handling — resolved integrator order-of-operations bugs and windup asymmetry
- Input-voltage-dependent gain scaling for stable regulation across the operating range
- FDCAN telemetry, interrupt-driven reception between boards
- HRTIM/TIM1 PWM generation, injected ADC sampling with DMA
- OPAMP2 configured as a PGA for current sensing
- Soft-start ramp logic with clamped anti-windup for safe startup

**Debugging highlight:** a persistent PWM non-functionality issue was eventually traced to a floating PA6 pin triggering spurious BKIN break events, compounded by incorrect CCR4 register placement — a reminder that a single unconnected pin can look exactly like a firmware bug.

*(Earlier iteration: an STM32G491-based version of this same control scheme, including hardware button debounce and SWV/ITM debug output during bring-up.)*

## PCB design

- EMI-aware layout: ground plane partitioning, Kelvin sensing for accurate current measurement
- Decoupling capacitor hierarchy based on PDN impedance and ESR/ESL/SRF analysis
- CAN differential pair routing per CISPR 32 guidelines

## Standards referenced

- IEC 61851-1 (Control Pilot signal physics, relevant to overall charger behavior)

## Tools used

- STM32CubeIDE / STM32CubeMX
- KiCad / Altium *(update to whichever you used)*
- Nucleo-G491RE, custom STM32G474 boards

## License

MIT — see [LICENSE](./LICENSE).
