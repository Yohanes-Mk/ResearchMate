ResearchMate Architecture
Dataflow
Topic input (CLI)

ResearchAgent → queries arXiv, PubMed, local docs → normalized {title, content} list

SummariserAgent (Gemini) → structured academic report (Title, Intro, Key Findings, Discussion, Conclusion, References with numbered inline citations)

EditorAgent → clarity/consistency polishing

PDF renderer → outputs/final_report.pdf

Sequence (simplified)
mermaid
Copy code
sequenceDiagram
    participant U as User
    participant O as Orchestrator
    participant R as ResearchAgent
    participant S as Summariser
    participant E as Editor
    participant P as PDF Engine

    U->>O: topic
    O->>R: collect(topic)
    R-->>O: articles[{title, content}]
    O->>S: synthesize(articles, topic)
    S-->>O: draft_markdown
    O->>E: edit(draft_markdown)
    E-->>O: final_markdown
    O->>P: render(final_markdown)
    P-->>U: final_report.pdf
Config knobs
pipeline_config.yaml: tool enable/disable, limits, timeouts

configs/settings.py: keys, paths, model choice

Extension points
Add new Tool subclass (e.g., Semantic Scholar)

Swap LLM provider in SummariserAgent

Replace renderer (md→PDF) if desired
