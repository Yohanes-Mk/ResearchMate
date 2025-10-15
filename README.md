# ResearchMate 🧠📄 — Autonomous Research Assistant

[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![LLM](https://img.shields.io/badge/LLM-Gemini%201.5%20Flash-9cf)]()
[![arXiv](https://img.shields.io/badge/Data-arXiv-red)]()
[![PubMed](https://img.shields.io/badge/Data-PubMed-0a7)]()
[![PDF](https://img.shields.io/badge/Export-ReportLab-lightgrey)]()

ResearchMate is a **multi-agent backend system** that automates academic research: it **finds papers (arXiv/PubMed + local docs), synthesizes findings with Gemini, edits for clarity, and exports a structured PDF** — all from a single command.

---

## Problem → Solution
**Problem.** Literature reviews are slow and repetitive: searching, triaging, synthesizing, formatting, and referencing.

**Solution.** ResearchMate runs a **configurable pipeline**:
1) collect relevant articles,
2) synthesize them into a structured report,
3) polish tone/format,
4) export a professional **PDF** with references.

---

## Key Features
- 🔎 Multi-source ingestion: **arXiv, PubMed, local documents**
- 🤖 Multi-agent pipeline: **Research → Summariser → Editor**
- 📄 Professional export: **Markdown → PDF (ReportLab)**
- ⚙️ Config-driven, modular design
- 🧪 Backend-only (CLI). UI planned.

---

## Architecture (high level)
```mermaid
flowchart TD
    A[User Input: Research Topic] --> B[Research Agent<br/>Collects Papers (arXiv, PubMed, Local)]
    B --> C[Summariser Agent<br/>Synthesizes Structured Report]
    C --> D[Editor Agent<br/>Polishes Tone & Cohesion]
    D --> E[PDF Generator<br/>Markdown → PDF + References]
```

### Module Map
- `agents/`
  - `research_agent.py`: Orchestrates tools, builds article set
  - `summariser_agent.py`: Gemini synthesis with academic sections + numbered refs
  - `editor_agent.py`: Style/clarity pass
  - `base_agent.py`: Shared behavior
- `tools/`
  - `arxiv_tool.py`, `pubmed_tool.py`: External search + fetch
  - `document_search_tool.py`: Local corpus matches
  - `base_tool.py`: Shared behavior
- `workflows/orchestrator.py`: Runs the end-to-end pipeline
- `configs/settings.py`, `configs/pipeline_config.yaml`: Keys, paths, pipeline options
- `outputs/articles/*`, `outputs/final_report.pdf`: Artifacts

### Results & Metrics (typical run)
| Metric               | Result          | Notes                    |
|----------------------|-----------------|--------------------------|
| Avg runtime          | ~1m45s/topic    | 10 runs, laptop baseline |
| Articles fetched     | ~14             | arXiv + PubMed mix       |
| Content relevance    | ~85%            | Manual vs abstracts      |
| LLM tokens           | ~8k             | Prompt + context         |
| Hands-free automation| 100%            | Topic → PDF              |

_Numbers are indicative; your hardware, network, and API limits may vary._

### Quickstart
```bash
git clone <your-repo-url>
cd researchmate
python -m venv .venv && source .venv/bin/activate  # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt
```

#### Configure
Edit `configs/settings.py`:

```python
GEMINI_API_KEY = "YOUR_KEY"
DATA_PATH = "data/"
OUTPUT_PATH = "outputs/"
```

#### Run
```bash
python main.py --topic "AI in Healthcare"
```

- **Artifacts:** `outputs/final_report.pdf`, `outputs/articles/*.pdf` (plus search traces)
- **Example Output:** See `outputs/final_report.pdf` for a sample generated on "AI in Healthcare".

### Tech Stack
| Layer | Tools | Role |
|-------|-------|------|
| Core | Python 3.10+ | Primary logic |
| Agents | Custom (CrewAI-style) | Research / Summarise / Edit |
| LLM | Gemini 1.5 Flash | Synthesis & editing |
| Data | arXiv, PubMed, local files | Sources |
| Export | ReportLab | PDF generation |
| Config | YAML + Python | Pipeline tuning |

### Roadmap
- Streamlit UI with live progress
- Dockerfile + GitHub Actions CI
- Batch topics & caching
- Source dedup + ranking
- Inline cite linking to PDFs
- Model adapters (OpenAI, Claude)

### Repository Structure
```text
researchmate/
├─ agents/
├─ tools/
├─ workflows/
├─ configs/
├─ outputs/
├─ docs/
│  ├─ ARCHITECTURE.md
│  └─ PROJECT_SUMMARY.md
├─ main.py
├─ requirements.txt
└─ README.md
```

### License & Author
- **License:** MIT (see `LICENSE`)
- **Author:** Yohannes Nigusse

### Hiring Snapshot (Resume)
- Built an autonomous multi-agent research assistant integrating arXiv/PubMed + Gemini to generate academic PDF reports (<2 min/topic, ~85% relevance).
