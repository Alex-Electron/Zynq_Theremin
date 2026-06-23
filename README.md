# Zynq Theremin

A no-compromise, studio-grade **digital theremin** built on a Xilinx Zynq-7000 SoC.
A modern, SMD-based reincarnation of the open FPGA theremin **d-lev** by Eric Wallin (dewster),
with a current-sensing analog front end, hardware DSP synthesis, and zero-latency response.

> **Inspired by the ideas of Eric Wallin (dewster)** and his open d-lev project.
> This is an independent design that builds on his concepts — full credit and lineage below.

> **Core principle — Zero Latency:** all phase tracking (DPLL) and audio synthesis run
> exclusively in the FPGA fabric (PL). The ARM cores (PS) are strictly control plane —
> GUI, connectivity, MIDI mapping, OTA — never in the realtime audio path.

## Status

🌱 **Early stage — staking the project.** Architecture and design decisions are fixed;
hardware bring-up is next.

- **Phase:** Phase 1 (BOM + schematic) → Phase 3a (FPGA prototype on EBAZ4206)
- **FPGA:** Xilinx Zynq **XC7Z020**
- **Prototype board:** EBAZ4206 mining board (reworked from XC7Z010 to XC7Z020)

## Hardware platform

| Block | Choice |
|---|---|
| SoC | Xilinx Zynq **XC7Z020** (Cortex-A9 PS + Artix-7 PL) |
| Prototype board | EBAZ4206 (reworked 7010 → 7020) → custom PCB later |
| AFE topology | Wallin current-sensing, air-core coils (no ferrite drift) |
| Comparator | ADCMP600 (precision, ultra-fast — replaces CMOS inverters) |
| Power | LT3045 ultra-low-noise LDO |
| Isolation | ADuM1250 digital isolators, latching relays for calibration |
| Audio DAC | PCM5102A over I²S |
| Display coprocessor | ESP32-S3 (USB OTG host for MIDI 2.0 UMP, BLE, Wi-Fi OTA) |
| Display | 480×320 touch TFT, EMI-isolated (Faraday cage + ferrite filters) |

## Feature roadmap

What we want to implement. Nothing here is shipped yet — this is the target spec.

### Core engine (FPGA / PL)
- [ ] DPLL phase tracking entirely in PL — deterministic, zero-latency
- [ ] 48-bit fixed-point DSP for oscillator stability and linearity
- [ ] High-speed ISERDES capture for direct RF sensing
- [ ] Hardware DSP synthesis: additive, formant choirs, physical modeling
- [ ] Wavetable + subtractive synthesis (Korg Radias / Waldorf Blofeld inspired)
- [ ] Theremin-appropriate effects chain in PL
- [ ] I²S audio output to PCM5102A

### Pitch & field control
- [ ] Mathematical field linearization (extend d-lev's linearity)
- [ ] Adjustable pitch correction / autotune with variable depth
- [ ] Deep customization of the volume "knee"
- [ ] Instant (~1 s) antenna autocalibration at power-on

### Analog front end
- [ ] Current-sensing AFE with emitter-degeneration resistors
- [ ] Air-core coils for thermal stability
- [ ] ADCMP600 precision comparator path
- [ ] "Isolated islands" power/signal architecture (LT3045 + ADuM1250)
- [ ] Latching relays for physical antenna disconnect during calibration/silence

### Player feedback
- [ ] Classic ring LED tuner, PL-driven, zero-lag — with full dim/off for ear training
- [ ] Touch TFT: visual pitch preview (Randy George / Merlin Tuner style)
- [ ] On-instrument oscilloscope, preset and field-setting visualization
- [ ] Dedicated **Tuner Out** — independent, constant-level, pre-volume/pre-effects clean tone

### Control plane (PS + ESP32-S3)
- [ ] MIDI mapping + MIDI 2.0 UMP (USB OTG host on ESP32-S3)
- [ ] BLE mobile app (iOS/Android) for live parameter tuning without touching audio
- [ ] Wi-Fi OTA FPGA bitstream (`.jic`) updates from the app
- [ ] Wavetable / IR loading into DDR3, streamed to PL over AXI HP

## Architecture (one line)

```
AFE (current sensing, ADCMP600, LT3045, ADuM1250)
  → Zynq PL (DPLL + hardware DSP synth + effects + LED ring + I²S)
  → PCM5102A I²S DAC → Audio out + Tuner out

Zynq PS (control)  ←UART/SPI→  ESP32-S3 (TFT GUI + BLE + Wi-Fi OTA + MIDI 2.0 host)
```

## Credits & lineage

This project is a derivative of and tribute to **d-lev** by **Eric Wallin (dewster)** —
the open FPGA theremin (HDL and software released under the MIT License). Original work:

- d-lev HDL & software: https://github.com/d-lec
- Theremin World design thread: http://www.thereminworld.com/Forums/T/28554/lets-design-and-build-a-mostly-digital-theremin

## License

See [LICENSE](LICENSE).
