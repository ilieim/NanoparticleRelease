# Physical mechanisms of nanoparticle intracellular release through membrane pore nucleation and expansion

This repository contains the LAMMPS input files associated with the manuscript **"Physical mechanisms of nanoparticle intracellular release through membrane pore nucleation and expansion"** by Massimiliano Paesani and Ioana M. Ilie.

The simulations follow the release of a coarse-grained nanocarrier from an enclosing lipid vesicle. Two icosahedral metaparticles are considered: MP60, with 60 interconnected beads and radius approximately `4.5 sigma`, and MP180, with 180 beads and radius approximately `7 sigma`. The membrane is represented with the three-bead Cooke-Deserno lipid model.

## Overview

Starting from a fully endocytosed configuration, the study compares three release mechanisms:

| Label | Release mechanism | Driving used in the input files |
| --- | --- | --- |
| `P` | Passive | No active force; release is controlled by the metaparticle-lipid interaction. |
| `IO` | Inside-out active | One type-4 cargo bead is created at the metaparticle center and propelled along its instantaneous velocity with force `5 epsilon/sigma`. |
| `FA` | Fully active | Every metaparticle bead is propelled in the `+x` direction with force `0.1 epsilon/sigma`. |


## Repository contents

```text
.
|-- I_Pot/
|   `-- muLJ_*.table
|-- MP60/
|   |-- P_rep_7_MP60/
|   |-- IO_rep_7_MP60/
|   `-- FA_rep_7_MP60/
|-- MP180/
|   |-- P_rep_7_MP180/
|   |-- IO_rep_7_MP180/
|   `-- FA_rep_7_MP180/
`-- README.md
```

Each simulation directory contains:

| File | Purpose |
| --- | --- |
| `run_bilayer.in` | Main LAMMPS input, dynamics, active forcing, random seed and output settings. |
| `system.in.init` | Units, atom style, interaction styles and neighbor-list settings. |
| `system.in.settings` | Pair, bond and angle coefficients. |
| `*.data` | Starting coordinates and molecular topology for the vesicle-metaparticle system. |
| `tabulated_potential.dat` | Tabulated interactions for the Cooke-Deserno lipid model. |

| Atom type | Component |
| --- | --- |
| `1` | Lipid head bead |
| `2` | Lipid tail bead |
| `3` | Metaparticle bead |
| `4` | Active internal cargo, created only by the `IO` inputs |

## Requirements

- [LAMMPS](https://www.lammps.org/) with the `MOLECULE` and `BROWNIAN` packages enabled.
- The `FA` simulations additionally require the `DIPOLE` package because they use `fix propel/self dipole`.
- Enough storage for a trajectory containing 20,000 saved configurations per production run.

See the official documentation for [`fix propel/self`](https://docs.lammps.org/fix_propel_self.html) and [`pair_style table`](https://docs.lammps.org/pair_table.html). Run `lmp -h` and confirm that `propel/self`, `fene`, `harmonic` and `table` are available in your build before starting production calculations.
