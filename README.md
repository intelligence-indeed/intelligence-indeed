# Intelligence Indeed

Intelligence Indeed (tars as short name in code) is a multi-agent computer-use system for desktop GUI automation. It separates feasibility probing, planning, and execution across a Gate, a Planner, and an Executor, and combines dynamic and static skills to improve cross-agent coordination on open-ended desktop tasks.

This repository hosts the Intelligence Indeed agent implementation used for [OSWorld](https://github.com/xlang-ai/OSWorld) evaluation ([PR #542](https://github.com/xlang-ai/OSWorld/pull/542)).

## Technical report

A technical report with method details, ablations, and analysis is **coming soon**.

## Contents

- `mm_agents/intelligence_indeed/` — agent package (roles, skill system, toolkit, runtime)
- `desktop_env/desktop_env_tars.py` — OSWorld desktop environment adapter
- `scripts/python/run_multienv_tars.py` — multi-env evaluation runner

## Setup & evaluation

See [`mm_agents/intelligence_indeed/README.md`](mm_agents/intelligence_indeed/README.md) for environment variables and the full `test_nogdrive.json` run command.

## Acknowledgements

We thank the Pointer, Agent-S, and VLAA teams, as well as the broader OSWorld agent community, for open research and tooling that informed the development of Intelligence Indeed.
