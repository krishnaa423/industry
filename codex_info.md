# Codex Handoff Notes

This repo is a portfolio workspace for Srikrishnaa Vadivel. It contains a
public master repo with nested GitHub submodules for theory notes, project
repos, resumes, and a static personal website.

## Current GitHub State

Master repo:

- `https://github.com/krishnaa423/industry`
- Public
- Latest local/pushed master commit at time of this note: `908db69`

Submodules are registered in `.gitmodules` and pushed to public repos:

- `cs/cs_theory` -> `https://github.com/krishnaa423/industry-cs-theory.git`
- `cs/egnn_qm9` -> `https://github.com/krishnaa423/industry-egnn-qm9.git`
- `cs/ros2_turtlebot_sim` -> `https://github.com/krishnaa423/industry-ros2-turtlebot-sim.git`
- `ee/ee_theory` -> `https://github.com/krishnaa423/industry-ee-theory.git`
- `ee/mips_processor` -> `https://github.com/krishnaa423/industry-mips-processor.git`
- `ee/ai_accelerator` -> `https://github.com/krishnaa423/industry-ai-accelerator.git`
- `math/math_theory` -> `https://github.com/krishnaa423/industry-math-theory.git`
- `physics/physics_theory` -> `https://github.com/krishnaa423/industry-physics-theory.git`
- `physics/dolfinx` -> `https://github.com/krishnaa423/industry-dolfinx.git`
- `physics/meep_ring_resonator` -> `https://github.com/krishnaa423/industry-meep-ring-resonator.git`
- `physics/first_principles_lif` -> `https://github.com/krishnaa423/industry-first-principles-lif.git`
- `resume` -> `https://github.com/krishnaa423/industry-resume.git`
- `personal-website` -> `https://github.com/krishnaa423/industry-personal-website.git`

## Contact/Socials Used

These came from `requirements.md` and were added to resumes and the website:

- Phone: `516-853-5663`
- Email: `srikrishnaacareers@gmail.com`
- GitHub: `https://github.com/krishnaa423`
- LeetCode: `https://leetcode.com/u/krishnaa42342/`
- Docker Hub: `https://hub.docker.com/u/krishnaa42342`

## Important Implementation Notes

- `cs/cs_theory/main.tex` originally used `minted`, but local `latexminted`
  failed with the Homebrew Python 3.14 argparse API. It now uses `listings`, so
  plain `pdflatex main.tex` works without shell escape or Pygments.
- `cs/cs_theory/main.pdf` is committed and was generated successfully with
  plain `pdflatex`.
- Resume PDFs are committed in the `resume` submodule.
- Static site files live in `personal-website/`; open `index.html` directly or
  serve the folder with Python.
- The Browser plugin's required Node REPL tool was not exposed in the earlier
  session, so visual browser verification was not performed through the in-app
  browser.

## Verification Commands

From repo root:

```bash
git status --short
git submodule status
```

Compile CS theory:

```bash
cd cs/cs_theory
pdflatex -interaction=nonstopmode -halt-on-error main.tex
pdflatex -interaction=nonstopmode -halt-on-error main.tex
```

Compile resumes:

```bash
for d in resume/software resume/ml resume/embedded resume/comp_physics resume/ee; do
  (cd "$d" && pdflatex -interaction=nonstopmode -halt-on-error main.tex)
done
```

Run lightweight Python artifacts:

```bash
python3 physics/first_principles_lif/src/lif_bands.py
python3 cs/ros2_turtlebot_sim/src/trajectory_demo.py
python3 cs/egnn_qm9/src/train.py
```

Run Verilog checks:

```bash
cd ee/mips_processor
mkdir -p build
iverilog -g2012 -o build/mips_tb src/mips_cpu.v tb/mips_tb.v
vvp build/mips_tb
```

```bash
cd ee/ai_accelerator
mkdir -p build
iverilog -g2012 -o build/matmul_tb src/matmul_accel.v tb/matmul_tb.v
vvp build/matmul_tb
```

Serve the website:

```bash
cd personal-website
python3 -m http.server 8000
```

## Workflow for Future Changes

When editing a submodule:

1. Commit and push inside the submodule.
2. Return to repo root.
3. `git add <submodule-path>`
4. Commit and push the master repo so the gitlink points to the new submodule
   commit.

Example:

```bash
cd resume
git add .
git commit -m "Update resumes"
git push
cd ..
git add resume
git commit -m "Update resume submodule"
git push origin main
```
