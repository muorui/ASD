# AGENTS.md

## Project overview

**ASD** is an early-stage Python-oriented repository for multimodal autism spectrum disorder (ASD) screening research. The only checked-in artifact today is `dataset/autism_dataset_index.csv`, which indexes 100 subjects across image, voice, motion, and physio modalities. Application code, tests, lint config, and media assets are not present yet.

## Local development

| Step | Command |
|------|---------|
| Create venv | `python3 -m venv .venv` |
| Install deps | `.venv/bin/pip install -r requirements.txt` |
| Activate (optional) | `source .venv/bin/activate` |

## Lint / test / build / run

| Task | Status | Notes |
|------|--------|-------|
| Lint | N/A | No Python source or linter config in repo |
| Test | N/A | No `tests/` directory; validate the dataset index manually (see below) |
| Build | N/A | No build target |
| Run app | N/A | No server or CLI entrypoint |

### Dataset validation (current “hello world”)

From repo root with the venv active:

```bash
.venv/bin/python -c "
import pandas as pd
df = pd.read_csv('dataset/autism_dataset_index.csv')
assert len(df) == 100
print(df['label'].value_counts())
"
```

## Cursor Cloud specific instructions

- **System package:** Ubuntu images may not include `python3-venv` by default. If `python3 -m venv .venv` fails with `ensurepip is not available`, run `sudo apt-get install -y python3.12-venv` once per VM (not in the update script).
- **Update script:** Runs `pip install -r requirements.txt` inside `.venv` after creating the venv if missing. No services to start.
- **No long-running services:** There is no API, UI, or Docker stack. End-to-end product testing is not applicable until application code lands.
- **Dataset media:** CSV paths point to `images/`, `voice/`, `motion/`, and `physio/` under the dataset tree; those files are not committed. Work against the index only unless assets are added locally.
