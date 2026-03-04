#  PCDC Query Agent
> An intelligent agentic chatbot that understands natural language and routes user intent to specialized tools — including general inquiry, documentation browsing, and GraphQL cohort query generation for the PCDC data model.

---

##  Motivation

Researchers working with the [Pediatric Cancer Data Commons (PCDC)](https://commons.cri.uchicago.edu/pcdc/) often need to query complex patient cohort data. Building these queries manually requires deep knowledge of the GraphQL schema and PCDC data model — a significant barrier for clinicians and researchers.

This project aims to remove that barrier by letting users **describe a cohort in plain English** and automatically generating the corresponding GraphQL query — powered by an LLM-based routing agent.

---

##  Architecture Overview

```
User Input (Natural Language)
        │
        ▼
┌───────────────────┐
│   Routing Agent   │  ◄── Intent Classification (LLM)
└───────────────────┘
        │
   ┌────┴─────────────────────────────────────────┐
   │                      │                       │                 
   ▼                      ▼                       ▼
Tool 1               Tool 2                  Tool 3
General Inquiry      Docs Browser            GraphQL Generator
(FAQ / general)      (PCDC documentation)    (Cohort query builder)
```

- The **Routing Agent** classifies user intent and delegates to the right tool
- **Tool 1** handles general questions about PCDC, the data model, or the platform
- **Tool 2** searches and retrieves relevant documentation chunks (RAG-based)
- **Tool 3** generates valid GraphQL queries from natural language cohort descriptions, evaluated against saved PCDC filtersets

---

##  Tech Stack

| Layer | Technology |
|---|---|
| LLM Backend | OpenAI GPT-4 / Groq (LLaMA) |
| Agent Framework | Google ADK / LangChain |
| Backend API | Node.js + Express.js |
| GraphQL | PCDC Data Model Schema |
| Docs Retrieval | RAG pipeline (embeddings + vector search) |
| Evaluation | Saved filterset comparison |

---

##  Planned Features

- [x] Repository setup & architecture design
- [ ] Intent classification and routing agent
- [ ] Tool 1: General inquiry handler
- [ ] Tool 2: Documentation browser (RAG-based)
- [ ] Tool 3: GraphQL query generator from natural language
- [ ] GraphQL output evaluation against saved PCDC filtersets
- [ ] REST API wrapper for frontend integration
- [ ] Basic UI for testing the chatbot

---

##  Project Structure (Planned)

```
pcdc-query-agent/
├── agent/
│   ├── router.js          # Intent classification & tool routing
│   ├── tools/
│   │   ├── general.js     # Tool 1: General inquiry
│   │   ├── docs.js        # Tool 2: Documentation browser
│   │   └── graphql.js     # Tool 3: GraphQL generator
├── api/
│   └── server.js          # Express.js API layer
├── evaluation/
│   └── eval.js            # GraphQL output evaluator
├── docs/
│   └── architecture.md    # Detailed design notes
├── .env.example
├── package.json
└── README.md
```

---

##  Getting Started

> ⚠️ This project is currently in active development. Setup instructions will be updated as the codebase evolves.

```bash
# Clone the repo
git clone https://github.com/[your-username]/pcdc-query-agent.git
cd pcdc-query-agent

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Add your OpenAI / Groq API keys

# Start the server
npm run dev
```

---

##  Evaluation Strategy

GraphQL outputs will be evaluated by:
1. **Structural validity** — does the query conform to the PCDC schema?
2. **Semantic accuracy** — does it match saved filterset equivalents?
3. **Edge case handling** — complex multi-condition cohort descriptions

---

## 🔗 Related Resources

- [PCDC Official Site](https://portal.pedscommons.org/login)
- [FHIR Documentation](https://www.hl7.org/fhir/documentation.html)
- [GraphQL Docs](https://graphql.org/learn/)
- [Google ADK](https://developers.google.com/adk)

---

## 👤 Author

**Subhojeet Prasad**
B.Tech Computer Science & Engineering | Gargi Memorial Institute of Technology
[GitHub](https://github.com/Prasad1-S) · [LinkedIn](https://www.linkedin.com/in/subhojeetprasad/)

---

## 📌 Status

> 🟡 **In Progress** — Being developed as part of GSoC 2026 preparation for the PCDC / UChicago org.
