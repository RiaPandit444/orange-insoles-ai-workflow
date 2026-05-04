#  AI Competitive Intelligence Workflow
### Built during AI & Data Analytics Internship | Orange Insoles (2025)

---

## Overview

This project is an end-to-end AI automation system I built during my internship to give a small business CEO the ability to independently research competitors, analyze consumer trends, and generate market content — all without writing a single query or hiring an analyst.

The system connects a structured database (Baserow) to Claude AI through custom-built skills, agents, and MCP server connectors, orchestrated through n8n automation workflows. The result: the CEO can ask a plain-English question and receive a synthesized, data-backed answer or draft article in seconds.

---

##  Workflow Architecture

![AI Competitive Intelligence Workflow Architecture](<./AI workflow.png>)

*Four interconnected pipelines built in n8n: (1) content extraction from ProHQ, (2) topic extraction via Claude (Anthropic), (3) theme extraction and aggregation via Claude, and (4) vector embedding and import using OpenAI Embeddings + Qdrant Vector Store for semantic search and scoring.*

---

##  Project Files

*   **[n8n Workflow JSON](<./Flows 1 & 2.json>)** — The raw orchestration logic for the four interconnected pipelines.
*   **[Claude Custom Skill (.md)](<./articles-agent(CompanyInfoRedacted).md>)** — Modular instructions and prompt engineering used for consistent content generation and trend analysis.

---

##  Tech Stack

| Tool | Role |
|------|------|
| **n8n** | Workflow automation & orchestration |
| **Claude (Anthropic)** | LLM for topic extraction, theme analysis & content generation |
| **MCP Servers** | Model Context Protocol connectors linking Claude to external data |
| **Baserow** | Structured database for storing and retrieving market data |
| **OpenAI Embeddings** | Converts text data into vector representations |
| **Qdrant Vector Store** | Stores and queries embeddings for semantic similarity search |
| **ProHQ** | Source platform for content and transcript extraction |
| **AI Agents** | Autonomous multi-step task execution |
| **Custom Skills** | Modular prompt-based instructions for consistent Claude behavior |
| **Connectors** | Bridges between data sources, workflows, and the LLM |

---

##  Pipeline Breakdown

### Pipeline 1 — Extract Content from ProHQ
Pulls transcripts and raw content from ProHQ via HTTP request, processes the list, edits fields, and stores structured records in Baserow for downstream analysis.

```
HTTP Request → GET List → Split Out → Edit Fields → Create Row (Baserow)
```

### Pipeline 2 — Topic Extraction
Reads content rows from Baserow, loops through each item, and passes them to Claude (Anthropic Chat Model) via an Information Extractor node. Claude identifies and extracts key topics, which are then split, formatted, and written back to Baserow.

```
Get Rows (Baserow) → Loop Over Items → Edit Fields → Claude (Topic Extraction)
→ Edit Fields → Split Out → Set Payload → Create Row (Baserow)
```

### Pipeline 3 — Theme Extraction
Aggregates all extracted topics, passes them to Claude for higher-level theme identification, and stores the resulting themes back in Baserow. This layer turns granular topics into strategic themes for the CEO.

```
Get All Topics (Baserow) → Set Topic → Aggregate → Claude (Theme Extraction)
→ Split Out → Create Themes (Baserow)
```

### Pipeline 4 — Import Topics, Themes & Score Data (Vector Embeddings)
Loops through all processed rows, generates vector embeddings via OpenAI, stores them in a Qdrant Vector Store for semantic search and scoring, and writes the final enriched records back to Baserow.

```
Execute Workflow Trigger → Get Rows (Baserow) → Loop Over Items
→ OpenAI Embeddings + Qdrant Vector Store → HTTP Request → Edit Fields → Create Row (Baserow)
```

---

##  What I Built

### Competitive Intelligence Pipeline
- Compiled and cleaned competitor and market data into a structured Baserow database
- Built n8n workflows to automatically pull, process, and feed data into Claude for analysis
- Identified top consumer search trends and key product differentiators

### Custom Claude Skills
- Wrote modular skill `.md` files that give Claude consistent, repeatable instructions for specific tasks (competitor analysis, trend summarization, article drafting)
- Skills are reusable across workflows and easily updated as business needs change

### Vector Search & Scoring
- Converted processed topics and themes into vector embeddings using OpenAI
- Stored embeddings in Qdrant for semantic similarity search, enabling the system to score and surface the most relevant competitive insights automatically

### AI Agents & Connectors
- Built agents capable of autonomous multi-step tasks — pull content → extract topics → identify themes → score and store
- Created MCP server connectors so Claude can read directly from Baserow without manual data exports

### CEO-Facing Workflow
- Designed the system so a non-technical user could trigger workflows and receive polished outputs with no coding required
- Use cases: generating new market articles, analyzing competitor positioning, surfacing top consumer search trends

---

##  Key Skills Demonstrated

- **AI Workflow Automation** — n8n, MCP servers, multi-stage pipelines
- **LLM Integration** — Claude (Anthropic), prompt engineering, information extraction
- **Vector Search** — OpenAI Embeddings, Qdrant Vector Store, semantic scoring
- **Data Pipeline Design** — raw content → structured DB → LLM → embeddings → output
- **Competitive Intelligence** — market research, topic/theme extraction, consumer behavior
- **Business Application of AI** — built for a real CEO with real business decisions

---

##  Repository Structure

```
orange-insoles-ai-workflow/
│
├── README.md
├── assets/
│   └── AI_workflow.png       # n8n workflow screenshot
├── workflows/                # n8n JSON workflow files (anonymized)
├── skills/                   # Custom Claude skill .md files
├── agents/                   # Agent configuration documentation
└── samples/                  # Example outputs (no proprietary data)
```

> **Note:** All workflows and files in this repository have been anonymized. Proprietary company data, API keys, and client-specific configurations have been removed. The logic, architecture, and methodology are entirely my own work.

---

## Contact

**Ria Pandit** — Economics Graduate, Michigan State University '26
- 📧 Panditri@msu.edu
- 💼 [LinkedIn](https://linkedin.com/in/ria-pandit-ldr44)
- 🐙 [GitHub](https://github.com/RiaPandit444)
