# Romeu Oliveira

**Software and AI engineer.** Ten years of work that started in test automation, moved through Go backends and data analysis, and since 2024 has focused on taking AI agents, RAG assistants and system integrations into production.

Belo Horizonte, Brazil · [LinkedIn](https://www.linkedin.com/in/romeuow/) · romeuow@gmail.com · Open to remote work (Brazil or international) and hybrid in Belo Horizonte.

---

## Contents

1. [Career](#career)
2. [Real-world cases](#real-world-cases)
3. [Public portfolio](#public-portfolio)
4. [How I work](#how-i-work)
5. [Tooling stack](#tooling-stack)
6. [Education and languages](#education-and-languages)

---

## Career

| Period | Role | Sector | Scope |
|---|---|---|---|
| Jun 2026 – present | AI Software Developer | Energy | Voice and chat agents integrated with the CRM, company-wide MCP server, LLM-based conversation grading, Claude Enterprise skills |
| Jul 2025 – Jun 2026 | AI Software Developer | Sustainability consulting | RAG assistants with source citations, SQL and semantic-search agents, document pipelines, AI backend-for-frontend |
| Aug 2024 – Jul 2025 | AI Engineer | Performance marketing agency | RAG chatbots, database-querying agent, image processing, media data pipelines |
| Feb 2024 – Aug 2024 | Senior Data Analyst | Performance marketing agency | Marketing data warehouse, analyses and dashboards |
| Feb 2022 – Jan 2024 | Data Analyst | International remittance fintech | Data analysis and data science projects, visualization, cloud |
| Jan 2021 – Dec 2021 | Data Analyst | Software platform startup | Data acquisition, storytelling, A/B test design and analysis |
| Sep 2018 – Jan 2021 | Back End Developer | Software platform startup | Go backend, infrastructure, a complete CLI |
| Sep 2017 – Sep 2018 | Full Stack Developer | Software houses | Web applications at two companies |
| Jan 2015 – Jun 2016 | Test Analyst | Software house | Requirements analysis, automated tests (RFT), Java unit tests |

Three phases: **quality and backend** (2015 to 2021), **data** (2021 to 2024) and **applied AI** (2024 onward). Each one feeds the next: testing became the habit of automated validation in AI systems, and data analysis became the basis for measuring agents with real metrics instead of impressions.

---

## Real-world cases

Problem, solution and end-to-end flow of each delivery. Code, data, client names and figures are confidential; what follows is the engineering pattern and the business outcome.

### Energy sector (Jun 2026 – present)

**1. AI voice and chat support integrated with the CRM**
Problem: thousands of calls and messages a month hitting a human first-level support team, with customer information scattered across CRM, analytics database and billing.
Solution: a voice AI answers the phone and a chatbot answers WhatsApp. Both locate the customer by phone, tax ID or installation code, answer questions through RAG, issue duplicate invoices and hand over to a human when needed.
Flow: call or message arrives → voice platform or Blip calls the API → audio transcription when needed → routing to the specialised agent (FAQ, sales, cancellation, plan change, power outage) → CRM and Postgres lookups → reply as text or synthesised speech → at the end of the interaction a signed webhook writes contact, call record, recording and transcript to the CRM, idempotent against redeliveries → cost per interaction recorded.
Outcome: automated first-level support with full traceability in the CRM and a daily report on volume, resolution, abandonment, cost and satisfaction.

**2. Company-wide MCP server for AI agents**
Problem: every agent was born with its own duplicated integrations to the CRM, the database and report publishing.
Solution: a single MCP server exposing those capabilities with typed contracts, authentication, PII masking in logs and contract tests. Any MCP client (Claude, IDEs, orchestrators) uses the same tools.
Flow: MCP client → `tools/list` → `tools/call` → service validates input → CRM HTTP client or parameterised Postgres query → structured response; HTML presentations published under a stable link served by the same process.
Outcome: centralised integrations reused by voice agents, internal assistants and reporting automations.

**3. Grading 100% of sales conversations with an LLM judge**
Problem: sales leadership manually reviewed a tiny sample of conversations and found improper promises too late.
Solution: a pipeline that grades every conversation against a versioned rubric, quotes passages as evidence, verifies the evidence exists, flags risks with deterministic rules and aggregates by salesperson and criterion.
Flow: conversation extraction → PII redaction → parallel grading per criterion (LangGraph) with structured output → evidence verification → risk rules → report and alerts. Prompt regression in CI prevents a rubric tweak from silently degrading scores.
Outcome: full coverage, consistent ranking and same-day compliance alerts.

### Sustainability consulting (Jul 2025 – Jun 2026)

**4. Internal policy assistant with source citations**
Problem: employees lost time hunting for rules across dozens of policies and HR answered the same questions repeatedly.
Solution: hybrid-search RAG, streamed answers citing passage and document, FAQ matching before retrieval, per-answer feedback and an admin panel for HR to manage documents and review poorly rated answers.
Flow: document ingestion with section-aware chunking and idempotent reindexing → embeddings and lexical index in Postgres with pgvector → question → FAQ match → hybrid search with rank fusion → generation with numbered citations over SSE → feedback persisted for improvement.
Outcome: verifiable answers, fewer repeated questions to HR and a feedback-driven improvement loop.

**5. Agent platform for the client ecosystem**
Problem: consulting teams needed to query clients' structured data and documents, generate report text against acceptance criteria and keep a knowledge base current.
Solution: an AI backend-for-frontend in FastAPI with LangGraph graphs: a chatbot with a SQL agent and a semantic-search agent, processing of user-uploaded documents (header, footer, tables, Q&A), generation and review of Q&A pairs for the knowledge base, template-based report text. SharePoint integration and Redis-backed streaming.
Outcome: consultants got answers about client data and documents from a single assistant, with report text generated and reviewed against explicit criteria.

### Performance marketing agency (2024 – 2025)

**6. AI agents over media data**
Problem: analysts spent hours categorising ad creatives and answering questions about campaign performance.
Solution: Airflow pipelines collect ad objects and metrics from media platforms into bronze and silver layers; an insights API categorises creatives with an LLM and answers natural-language questions by generating SQL over the base; promptfoo tests keep prompt regressions under control.
Flow: daily DAG collects ads and insights → normalisation into the analytical layer → analyst asks in natural language → agent generates and runs SQL → answer with the figures and the query used.
Outcome: automatic categorisation and on-demand answers about campaigns, freeing analysts for recommendation work.

---

## Public portfolio

The cases above are confidential. The repositories below are **generic reimplementations, with synthetic data, of the patterns applied in production**, written to show how I structure, test and document a service. Each README includes the use case, architecture, a demo mode that needs no credentials, tests and a security section.

| Project | Matching real case | Technical highlights |
|---|---|---|
| [**mcp-toolkit**](https://github.com/romeuow/mcp-toolkit) | Company-wide MCP server (case 2) | Streamable HTTP, Bearer auth, rate limiting, HTML sanitisation, snapshot contract tests |
| [**webhook-relay**](https://github.com/romeuow/webhook-relay) | Voice → CRM integration (case 1) | HMAC with anti-replay, idempotency verified at the destination, retry with backoff, binaries in S3, stateless |
| [**conversation-grader**](https://github.com/romeuow/conversation-grader) | Conversation grading (case 3) | LangGraph fan-out per criterion, structured output, verified evidence, PII redaction, prompt regression |
| [**policy-rag**](https://github.com/romeuow/policy-rag) | Policy assistant (case 4) | Hybrid search with RRF, pgvector and Alembic, SSE, FAQ, feedback, React |
| [**academic**](https://github.com/romeuow/academic) | Education | ODE/PDE solvers and eigenvalue algorithms from scratch in NumPy |

Test coverage above 95% and green CI on all of them.

---

## How I work

### Evidenced in the portfolio

- **Every external integration behind an interface**, with a fake implementation for tests and demo mode. Suites run offline in seconds; nothing reaches `main` without lint, type checks and a green pipeline.
- **Security at the edge**: signatures verified before parsing, constant-time comparisons, strict input validation, PII kept out of logs and prompts.
- **Observability from day one**: structured JSON logs with request IDs, metrics, and estimated LLM cost per job.
- **Documented decisions**: each README has a decision-versus-alternative table and an honest section on what is not covered.
- **Automated deployment**: multi-stage Docker images running as non-root, Compose for local and production, smoke tests after each deploy.
- **Strong typing and security testing** as part of the definition of done, not an afterthought.

### Methodology

- **Scope in writing before code.** I turn ambiguous requests into a short proposal with scope, assumptions and acceptance criteria, validated with stakeholders. When the problem is still fuzzy, a prototype in days beats a specification in weeks.
- **Incremental delivery, measured.** Sprints with a written proposal and a closing report when there is a client; continuous flow with small production deliveries when there is a product. Either way, a dashboard or daily report shows usage, cost and quality.
- **Bridge between business and technology.** I am comfortable as the hands-on specialist, as the technical reference for architecture and standards, or as the generalist covering backend, infra, data or frontend when the moment calls for it.
- **AI as a force multiplier, with guardrails.** Most of the code I ship today is written with AI assistance (Claude Code, Claude Enterprise, Copilot) across planning, implementation, testing and documentation. What makes it safe is the discipline around it: a detailed brief before delegating, mandatory automated tests, independent verification of critical paths, and evaluation suites that fail CI when model behaviour drifts.
- **Direct, specific feedback.** In code review, in regular one-on-ones and in team retrospectives. I would rather hear the concrete problem and the suggestion than a vague impression.
- **Learning by building.** Personal projects, primary-source documentation and papers, and exchange with peers keep the stack current.

---

## Tooling stack

**Languages**: Python (primary), Go, TypeScript, SQL, Java (early career), C/C++ (academic)

**AI and LLMs**: Anthropic API and Claude Enterprise (skills, MCP), OpenAI API (GPT, Whisper, TTS, File Search), LangChain, LangGraph, RAG, LLM-as-judge, structured outputs, tool calling, prompt engineering, embeddings and vector stores (pgvector, Pinecone), Docling and document OCR, image processing

**AI evaluation and observability**: promptfoo, Langfuse, LangSmith, prompt regression suites, cost per token, structured JSON logging

**Backend**: FastAPI, Flask, Starlette, Pydantic, SQLAlchemy/SQLModel, Alembic, gunicorn/uvicorn, HMAC-signed webhooks, idempotency, SSE/streaming, REST APIs

**Data**: PostgreSQL, Redis, Databricks, Airflow, Pandas, NumPy, SciPy, scikit-learn, Jupyter, data warehouse modelling, A/B testing, Looker Studio

**Cloud and infrastructure**: AWS (EC2, ECS Fargate, S3, RDS, Lambda, Cognito, CloudFront, IAM/OIDC), Terraform, Docker and Docker Compose, Nginx, Portainer, Certbot, GitHub Actions

**Frontend**: React + Vite, Angular, TypeScript, HTML/SCSS

**Integrations**: HubSpot (CRM), Blip (chatbots), ElevenLabs (voice), SharePoint, Open Finance (Pluggy), n8n

**Quality**: pytest, coverage and snapshot contract tests, vitest, ruff, mypy, Rational Functional Tester (historical), offline unit and integration tests with fakes, security testing

**Everyday tools**: uv and Poetry, Git and GitHub CLI, Claude Code, VS Code, Makefile, architecture docs with Mermaid

---

## Education and languages

**BSc in Computational Mathematics**, Universidade Federal de Minas Gerais (UFMG), 2012 to 2018. Grounding in numerical methods, optimisation and machine learning, which still shapes how I reason about models, error and cost.

Portuguese native. English full professional proficiency.

---

Happy to talk about applied AI engineering, Python backends and integration architecture. Reach me on [LinkedIn](https://www.linkedin.com/in/romeuow/).
