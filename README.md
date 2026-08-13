# Druhinh Roy

Electrical & Computer Engineering at UT Austin (BSECE, May 2028). I work on digital design — RTL, microarchitecture, and the flow that turns Verilog into a physical chip.

Right now I'm taking a floating-point datapath from an empty file to fabricated silicon.

---

## Currently building

**[BF16 Multiply-Accumulate Unit](https://github.com/druhinhroy/bf16-mac)** — a pipelined Brain Float 16 multiply / FP32 accumulate unit, taped out on the SkyWater 130nm open PDK.

BF16 multiply with FP32 accumulation is what actually runs inside modern AI accelerators — you keep FP32's dynamic range, trade away mantissa bits, and spend the savings on gate count and power. The interesting part isn't the multiply. It's everything around it:

- **Special cases.** NaN propagation, ±Inf saturation, signed zeros, round-to-nearest-even. Subnormals are flushed to zero — a deliberate area/timing trade-off, documented rather than hidden.
- **Verification.** cocotb driving directed edge cases and constrained-random stimulus against a Python `bfloat16` golden model, regressed on every commit.
- **I/O budget.** The target fabric gives me 8 input and 8 output pins. Two 16-bit operands don't fit, so they're serialized over a byte-wide load interface — the design latches a weight once and streams activations against it, structurally a systolic-array PE.
- **Physical design.** Full RTL-to-GDSII through OpenLane, with automated DRC, LVS, and gate-level simulation. Optimized for power, timing closure, and cell area, not just functional correctness.

Progress is committed as it happens, including the parts that don't work yet.

## Other work

**Multi-Mode Programmable Processor** — a programmable processor in Verilog on a Basys3 FPGA, partitioned into a custom datapath and controller FSM specified via High-Level State Machine formalism. Four operating modes at 10 ms resolution, verified in simulation before synthesis and hardware bring-up.

## Toolchain

Verilog · SystemVerilog · cocotb · Icarus Verilog · GTKWave · AMD Vivado · OpenLane (Yosys, OpenROAD, Magic) · SkyWater 130nm PDK · Tcl · Python · C/C++ · KiCad · Altium

## Away from the keyboard

President of [Texas Guadaloop](https://www.txguadaloop.org/), UT Austin's hyperloop team — 100+ members across engineering, business, and research. We took first place in both Design Only Engineering and Design Only Hyperloop Week at European Hyperloop Week 2026 in Groningen. Before that I led the power electronics team, designing 60–600 V high-voltage systems for the pod.

I also founded [Hyperloop Open](https://hyperloopopen.org), a Texas nonprofit building an inaugural collegiate hyperloop competition in Austin for May 2027.

Off-hours: a Proxmox homelab I keep breaking on purpose, and a home theater build that has gotten out of hand.

---

📫 druhinhroy@gmail.com · [LinkedIn](https://linkedin.com/in/druhinhroy)
