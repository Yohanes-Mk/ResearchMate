# ResearchMate Code Summary

## Core Workflow
| Module | Path | Highlights |
|:-------|:-----|:-----------|
| CLI Entry | `main.py` | Parses command-line flags, wires dependencies, invokes the orchestrator |
| Orchestration | `workflows/orchestrator.py` | Sequences agents, shares context, gathers metrics, persists run artifacts |
| Research Agent | `agents/research_agent.py` | Aggregates literature from arXiv, PubMed, and local corpora via pluggable tools |
| Summariser Agent | `agents/summariser_agent.py` | Crafts structured reports with Gemini prompts (sections, citations, tone constraints) |
| Editor Agent | `agents/editor_agent.py` | Normalizes voice, validates section coverage, and enforces citation ordering |

## Shared Infrastructure
| Area | Files | Purpose |
|:-----|:------|:--------|
| Agent Base | `agents/base_agent.py` | Common interface for prompt execution, context exchange, and logging hooks |
| Retrieval Tools | `tools/*_tool.py` | arXiv, PubMed, and document search implementations adhering to `BaseTool` |
| Configuration | `configs/settings.py`, `configs/pipeline_config.yaml` | API keys, model settings, feature flags, rate limits |
| Outputs | `outputs/` | Persisted inputs/outputs (raw articles, intermediate markdown, final PDF) |

## Development Notes
- Dependencies are declared in `requirements.txt`; project targets Python 3.10+.
- Logging is centralized in the orchestrator to surface agent-level progress.
- Add new capabilities by creating agent/tool subclasses and registering them in `pipeline_config.yaml`.
