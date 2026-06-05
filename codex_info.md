# Codex Handoff Notes

This repo is a portfolio workspace for Srikrishnaa Vadivel. It contains a
public master repo with nested GitHub submodules for theory notes, project
repos, resumes, and a static personal website.

## Current GitHub State

Master repo:

- `https://github.com/krishnaa423/industry`
- Public
- Latest local/pushed master commit before this handoff update: `73dfb3f`

GitHub Pages:

- Website repo: `https://github.com/krishnaa423/industry-personal-website`
- Live URL: `https://krishnaa423.github.io/industry-personal-website/`
- Pages was enabled from branch `main`, path `/`.
- The latest checked Pages build for commit `2942116` was `built`
  successfully. A later website update for Yale MS/MPhil was pushed at
  `9edfc18`; if future sessions need certainty, re-check Pages status with
  `gh api repos/krishnaa423/industry-personal-website/pages/builds/latest`.

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

## Education Facts Used

- Yale University, PhD in Electrical Engineering, 2021-present.
- Yale University, MS in Electrical Engineering, 2023, earned while in the PhD
  program.
- Yale University, MPhil in Electrical Engineering, 2023, earned while in the
  PhD program.
- Cornell University, MEng in Electrical and Computer Engineering, 2017-2018.
- Cornell University, BA in Electrical and Computer Engineering, 2013-2017.

## Important Implementation Notes

- User asked to save conversation state here so future Codex sessions can pick
  up in this repo. Keep this file current after meaningful changes.
- Current outstanding local state before this handoff update: `requirements.md`
  has an uncommitted local modification made outside the latest committed
  Codex changes. Do not overwrite it casually.
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

## Recent Conversation/Change Log

- Built the initial portfolio workspace from `requirements.md`: theory notes,
  project repos, resumes, and static website.
- Created local nested repos, pushed all submodules to public GitHub repos, and
  added `.gitmodules` in the master repo.
- Enabled GitHub Pages for `industry-personal-website`; live site is at
  `https://krishnaa423.github.io/industry-personal-website/`.
- Fixed hosted website links to point to public GitHub repos and hosted PDFs
  instead of local `../` paths.
- Replaced `minted` with `listings` in `cs/cs_theory/main.tex` so CS theory
  compiles with plain `pdflatex`.
- Added contact/socials to resumes and website:
  `srikrishnaacareers@gmail.com`, `516-853-5663`, GitHub `krishnaa423`,
  LeetCode `krishnaa42342`, Docker Hub `krishnaa42342`.
- Added Yale MS in ECE and Yale MPhil in ECE, both 2023, to all resumes,
  website copy, and these handoff notes.

Recent pushed commits before this handoff update:

- Master: `73dfb3f` (`Add Yale MS and MPhil education updates`)
- Resume submodule: `1b66b7d` (`Add Yale MS and MPhil to resumes`)
- Website submodule: `9edfc18` (`Add Yale MS and MPhil to website`)
- CS theory submodule: `15e0c67` (`Make CS theory compile with pdflatex`)

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
