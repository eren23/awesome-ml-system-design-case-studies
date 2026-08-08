---
id: cs2417
title: "Max Planck Institute for Biochemistry Builds Proteomics Research Expert GenAI Agent"
company: Max Planck Institute for Biochemistry
primary_category: genai
sub_category: agents
year: 2025
source_url: https://cloud.google.com/blog/products/ai-machine-learning/planck-institute-research-expert-gen-ai-agent
tags: [research-agent, proteomics, vertex-ai, scientific-llm, grounding]
---

# Max Planck Institute for Biochemistry Builds Proteomics Research Expert GenAI Agent
**Max Planck Institute for Biochemistry** · 2025 · [source](https://cloud.google.com/blog/products/ai-machine-learning/planck-institute-research-expert-gen-ai-agent)

## Problem
Mass spectrometry-based proteomics requires deep specialized expertise that creates a bottleneck when new lab members join, and the tacit knowledge of experienced researchers is regularly lost to academic turnover because complex hands-on procedures are rarely documented. Manual troubleshooting only catches errors after experiments have already failed, wasting costly equipment time and samples.

## Approach / System design
The institute built a multi-agent system orchestrated by a main coordinator agent that delegates to specialized sub-agents: a Lab Note Agent that analyzes experiment videos by comparing them to reference protocols, a Protocol Agent that generates publication-ready protocols from video and audio recordings, a Lab Knowledge Agent connected to Confluence, an Instrument Agent that retrieves real-time mass spectrometer performance metrics, and a Quality Control Memory Agent that persists troubleshooting decisions in BigQuery for institutional memory. Video and audio analysis uses Gemini's multimodal capabilities to detect procedural deviations, including missed steps, incorrect actions, and wrong ordering relative to the reference protocol.

## Key decisions
Using video as the primary input medium bridges the gap between AI assistance and hands-on laboratory work, enabling error detection without requiring manual annotation. Persisting troubleshooting decisions in a searchable BigQuery store creates a continuously improving institutional memory rather than one-off advice. The project was open-sourced to allow other domains requiring complex hands-on procedural guidance—such as manufacturing—to adapt the framework.

## Stack
Gemini models (Vertex AI, multimodal), Google Agent Development Kit (ADK), Google Cloud Storage, Confluence (via MCP), AlphaKraken MCP server (mass spectrometer monitoring), BigQuery (via MCP), GitHub (open-source release).

## Results
Evaluated on 28 recorded lab procedures: error detection recall was 74%, overall accuracy 77%, and precision 41% (false positives remain a known limitation). Protocol generation from video took an average of 2.6 minutes, approximately 10 times faster than manual creation, with generated protocols scoring an average of 4.4 out of 5 in quality assessments. The system is deployed with a 40-researcher group at the institute.

## Takeaways
Multimodal AI that compares video recordings against reference protocols enables a form of automated quality control in laboratory settings that was previously only achievable through expert supervision. Combining real-time instrument state with historical decision context allows the agent to give personalized, situationally appropriate guidance rather than generic protocol advice—a meaningful step toward AI systems that can reason about physical lab conditions.
