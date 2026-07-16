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

## PCB design

- EMI-aware layout: ground plane partitioning, Kelvin sensing for accurate current measurement
- Decoupling capacitor hierarchy based on PDN impedance and ESR/ESL/SRF analysis
- CAN differential pair routing per CISPR 32 guidelines

## Tools used

- STM32CubeIDE / STM32CubeMX
- Altium
- Nucleo-G491RE, custom STM32G474 boards
