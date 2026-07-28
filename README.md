[🇨🇳 简体中文](./README.zh-CN.md)

# Intelligence Indeed

Intelligence Indeed (tars as short name in code) is a multi-agent computer-use system for desktop GUI automation. It is a hybrid agent framework that blends static and dynamic skills. Static skills provide system prompts and general references through progressive disclosure, while dynamic skills are generated in real time by a task feasibility probing module. Both jointly guide execution throughout the entire workflow, preserving information independence while unifying execution experience across the full pipeline.

This repository is a snapshot of [OSWorld](https://github.com/xlang-ai/OSWorld) with the Intelligence Indeed agent integrated for official evaluation.

## Method

### Motivation

In multi-agent computer-use settings, two issues often limit reliability. First, early environment probing and web research may uncover useful constraints, but those findings are not always shared systematically with later stages, so planning and execution still start largely from scratch. Second, agents are often given long, general-purpose prompts that mix rules from many domains; irrelevant guidance can dilute useful preferences and inflate context cost.

Intelligence Indeed addresses both with a hybrid skill system. **Static skills** provide reusable domain guidance; **dynamic skills** carry instance-specific findings from live probing and search. Together they guide the multi-agent workflow end to end, keeping information roles distinct while aligning execution preferences across stages.

### Overview

The system solves desktop tasks with a multi-agent pipeline. Given an instruction, the agent first selects and loads relevant domain skills from a static skill index, then forms a task-specific dynamic skill from environment probes and web research. Downstream agents plan and execute under this shared skill context.

<p align="center">
  <img src="assets/skill-system-overview.png" alt="Skill system overview" width="100%">
</p>

### Static skills

Static skills are general-purpose operating guides. Each skill stores discovery metadata (`name`, `description`) for the model, along with a body of domain rules and preferences.

The agent exposes static skills through progressive disclosure so irrelevant information stays out of context, reducing cross-domain interference and extra token cost. If probing later reveals a missed domain, skills can still be added.

### Dynamic skills

Dynamic skills are generated per task instance and are not written into the static library. The agent probes the live environment read-only (resources, app state, UI reachability, etc.) and, when needed, searches or fetches documentation to verify capabilities and GUI paths. These signals are summarized into a scene-specific dynamic skill that guides the rest of task execution.

## OSWorld Benchmark Performance

Intelligence Indeed was evaluated on the OSWorld benchmark using a subset of 361 tasks (excluding Google Drive tasks).

**Models Evaluated:**
- **Core execution model:** `claude-opus-4-7`

**Overall Performance:**
- **Total score:** 325.59 / 361
- **Average score:** 90.19%

**Score Breakdown by Domain:**

| Domain | Score | Total Tasks |
| :--- | :---: | :---: |
| Chrome | 35.93 | 46 |
| GIMP | 24.0 | 26 |
| LibreOffice Calc | 46.0 | 47 |
| LibreOffice Impress | 42.96 | 47 |
| LibreOffice Writer | 22.0 | 23 |
| Multi Apps | 78.81 | 93 |
| OS | 24.0 | 24 |
| Thunderbird | 13.0 | 15 |
| VLC | 16.89 | 17 |
| VS Code | 22.0 | 23 |

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
