# Intelligence Indeed

Intelligence Indeed (tars as short name in code) is a multi-agent computer-use system for desktop GUI automation. It separates feasibility probing, planning, and execution across a Gate, a Planner, and an Executor, and combines dynamic and static skills to improve cross-agent coordination on open-ended desktop tasks.

This repository is a snapshot of [OSWorld](https://github.com/xlang-ai/OSWorld) with the Intelligence Indeed agent integrated for official evaluation.

## Technical report

A technical report with method details, ablations, and analysis is **coming soon**.

## Agent & evaluation entrypoints

- Agent package: [`mm_agents/intelligence_indeed/`](mm_agents/intelligence_indeed/)
- Agent README / setup: [`mm_agents/intelligence_indeed/README.md`](mm_agents/intelligence_indeed/README.md)
- Desktop env adapter: [`desktop_env/desktop_env_tars.py`](desktop_env/desktop_env_tars.py)
- Multi-env runner: [`scripts/python/run_multienv_tars.py`](scripts/python/run_multienv_tars.py)

## Quick start (OSWorld nogdrive)

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# configure repo-root .env (AWS_* + Anthropic / Parallel keys)
# see mm_agents/intelligence_indeed/README.md

python scripts/python/run_multienv_tars.py \
  --provider_name aws --region us-east-1 --headless \
  --test_all_meta_path evaluation_examples/test_nogdrive.json \
  --result_dir ./results/tars-nogdrive-full \
  --num_envs 6 --max_steps 100
```

## About OSWorld

This tree includes the full OSWorld codebase used for evaluation. For the upstream benchmark, docs, and license, see [xlang-ai/OSWorld](https://github.com/xlang-ai/OSWorld) (Apache-2.0). The original upstream README is kept as [`OSWORLD_README.md`](OSWORLD_README.md).

## Acknowledgements

We thank the Pointer, Agent-S, and VLAA teams, as well as the broader OSWorld agent community, for open research and tooling that informed the development of Intelligence Indeed.
