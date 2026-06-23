# Zynq Theremin

A no-compromise, studio-grade **digital theremin** built on a Xilinx Zynq-7000 SoC —
a modern, fully SMD reincarnation of the open FPGA theremin tradition.

> **Inspired by the ideas of Eric Wallin (dewster)** and his open d-lev project.
> This is an independent design that builds on his concepts — full credit and lineage below.

> **Core principle — Zero Latency:** all real-time signal processing runs in the FPGA
> fabric. The ARM cores are strictly control plane — never in the audio path.

## Status

🌱 **Early stage — staking the project.** The architecture and the detailed design
decisions are defined and held privately for now; they will be published incrementally
as the hardware is brought up and validated.

- **SoC:** Xilinx Zynq **XC7Z020** (Cortex-A9 PS + Artix-7 PL)
- **Prototype board:** EBAZ4206 mining board (reworked from XC7Z010 to XC7Z020)
- **Phase:** schematic & BOM → FPGA prototype

## Vision

The goal is a digital theremin that treats the FPGA — not a CPU or DSP chip — as the
core instrument: deterministic, sample-accurate, and latency-free by construction.
Around that core sit a precision analog front end, expressive player feedback, and a
modern connectivity layer — engineered to the standard of a finished studio instrument
rather than a hobby board.

Detailed feature specifications, the analog front-end topology, and the synthesis
architecture are intentionally **not published yet**. They will appear here as each
subsystem is proven on hardware.

## Credits & lineage

This project is a tribute to and builds on the ideas of **d-lev** by **Eric Wallin
(dewster)** — the open FPGA theremin (HDL and software released under the MIT License):

- d-lev HDL & software: https://github.com/d-lec
- Theremin World design thread: http://www.thereminworld.com/Forums/T/28554/lets-design-and-build-a-mostly-digital-theremin

## License

See [LICENSE](LICENSE).
