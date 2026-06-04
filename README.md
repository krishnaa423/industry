# Industry Portfolio Workspace

Portfolio, resumes, and technical notes for Srikrishnaa Vadivel.

## Structure

- `personal-website/`: static portfolio site tying together resumes, notes, and projects.
- `resume/`: targeted LaTeX resumes for software, ML, embedded, computational physics, and EE roles.
- `cs/`: CS theory notes, EGNN/QM9 force-model scaffold, and ROS 2 TurtleBot simulation plan.
- `math/`: math theory notes for algebra, analysis, geometry, and probability.
- `physics/`: physics theory notes plus DOLFINx, Meep, and first-principles LiF projects.
- `ee/`: EE theory notes, Verilog MIPS CPU, and tiny matrix-multiply accelerator.

## Local Verification

```bash
python3 physics/first_principles_lif/src/lif_bands.py
python3 cs/ros2_turtlebot_sim/src/trajectory_demo.py
python3 cs/egnn_qm9/src/train.py
```

```bash
cd ee/mips_processor && mkdir -p build
iverilog -g2012 -o build/mips_tb src/mips_cpu.v tb/mips_tb.v
vvp build/mips_tb
```

```bash
cd ee/ai_accelerator && mkdir -p build
iverilog -g2012 -o build/matmul_tb src/matmul_accel.v tb/matmul_tb.v
vvp build/matmul_tb
```

Open `personal-website/index.html` directly, or serve it with:

```bash
cd personal-website
python3 -m http.server 8000
```
