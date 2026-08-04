# Match IQ — Sports Intelligence Engine

A sport-agnostic AI platform that predicts match outcomes, values in-game decisions, and trains
reinforcement-learning agents — built around one shared game-state schema so the same architecture
can serve both sports clubs (analysis) and gaming companies (in-game agents).

See `docs/Match_IQ_Project_Blueprint.docx` for the full architecture, resource list, and workplan,
and `docs/match_iq_ops_planner.html` for the interactive team tracker (open it in a browser).

## Repo layout

```
match-iq/
├── data/            # shared schema definitions, raw/processed data (gitignored)
│   ├── raw/
│   └── schema/
├── predict/         # xG model + win-probability model (Person A)
│   └── notebooks/
├── strategize/       # VAEP / socceraction pipeline (Person B)
│   └── notebooks/
├── train/            # Google Research Football + PPO agent (Person C)
│   └── scenarios/
├── deploy/           # dashboard + club/game-engine API endpoints (Person D)
│   └── dashboard/
└── docs/             # blueprint doc, ops planner, architecture notes
```

## Getting started

```bash
git clone <your-repo-url>
cd match-iq
python -m venv .venv && source .venv/bin/activate   # or .venv\Scripts\activate on Windows
pip install -r requirements.txt
```

## Module owners

| Module | Owner | Depends on |
|---|---|---|
| `data/` | Person A | — |
| `predict/` | Person A | `data/` |
| `strategize/` | Person B | `data/` |
| `train/` | Person C | — (independent, uses simulator) |
| `deploy/` | Person D | `predict/`, `strategize/`, `train/` outputs |

## Branching

One feature branch per module, merged into `main` via pull request:

```bash
git checkout -b predict/xg-baseline
# ... work ...
git push -u origin predict/xg-baseline
# open a PR into main on GitHub
```

Keep `main` always runnable — merge small, merge often, don't let branches live longer than a week.
