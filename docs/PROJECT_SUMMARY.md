Project Summary
Path	Purpose	Notes
agents/base_agent.py	Shared agent interface	Execute contract
agents/research_agent.py	Multi-source article collection	Tracks article metadata in orchestrator
agents/summariser_agent.py	Gemini synthesis to academic format	Numbered references only
agents/editor_agent.py	Tone and structure polishing	Enforces consistency
tools/*_tool.py	Concrete data access	arXiv, PubMed, local
workflows/orchestrator.py	Pipeline runner	Logging + state
configs/settings.py	Keys/paths/models	Keep out of VCS if containing secrets
configs/pipeline_config.yaml	Feature flags + limits	Reproducibility
outputs/	Artifacts	PDFs + traces
