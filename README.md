# Romeu Oliveira

**Engenheiro de software focado em sistemas com IA em produção**: agentes, servidores MCP, RAG, avaliação de LLMs e os backends que sustentam tudo isso.

Belo Horizonte, MG · [LinkedIn](https://www.linkedin.com/in/romeuow/) · romeuow@gmail.com

*Software engineer building production AI systems (agents, MCP servers, RAG, LLM evaluation) and the Python backends behind them. Based in Brazil, open to remote work.*

---

## Sobre

Trabalho há vários anos levando IA generativa para operação real em empresas do setor de energia e de consultoria em sustentabilidade: atendimento por voz integrado a CRM, avaliação automática de conversas comerciais, assistentes de políticas internas com citação de fonte, e a camada de ferramentas que permite a agentes de IA agirem sobre sistemas de negócio com segurança.

O código dessas empresas é privado. Os repositórios abaixo são **reimplementações genéricas, com dados sintéticos, dos padrões que apliquei em produção**, escritas para mostrar como eu estruturo, testo e documento um serviço.

Formação em Engenharia pela UFMG, com base em métodos numéricos e otimização.

## Projetos em destaque

| Projeto | O que resolve | Destaques técnicos |
|---|---|---|
| [**mcp-toolkit**](https://github.com/romeuow/mcp-toolkit) | Servidor MCP que expõe CRM, base de clientes e publicação de páginas para agentes de IA | Streamable HTTP, auth Bearer, rate limiting, sanitização de HTML, testes de contrato com snapshot, fakes para rodar sem credenciais |
| [**policy-rag**](https://github.com/romeuow/policy-rag) | Assistente RAG full-stack para políticas internas, com citações e painel admin | Busca híbrida (vetorial + BM25) com RRF, pgvector + Alembic, streaming SSE, FAQ antes do RAG, feedback, React + Vite |
| [**conversation-grader**](https://github.com/romeuow/conversation-grader) | Avaliação de 100% das conversas de vendas com LLM-as-judge | LangGraph com fan-out por critério, saída estruturada validada, evidências verificadas no texto, redação de PII, regressão de prompts no CI |
| [**webhook-relay**](https://github.com/romeuow/webhook-relay) | Ponto único de entrada de webhooks de provedores externos para o CRM | HMAC com anti-replay, idempotência verificada no destino, retry com backoff e jitter, binários em S3, stateless |
| [**academic**](https://github.com/romeuow/academic) | Métodos numéricos da graduação | Solvers de EDO/EDP e autovalores implementados do zero em NumPy |

Todos têm README com caso de uso, arquitetura, instruções de execução em modo demo, seção de testes e de segurança. Cobertura de testes acima de 95% e CI verde em cada um.

## Stack

**Backend e IA**: Python 3.12+, FastAPI, Pydantic, LangGraph, Anthropic SDK, MCP, uv, pytest
**Dados**: PostgreSQL, pgvector, Redis, SQLAlchemy/Alembic, Pandas
**Infra**: Docker, GitHub Actions, AWS (EC2, S3, RDS, Lambda), Terraform, Nginx
**Frontend**: TypeScript, React, Angular

## Como eu trabalho

- **Toda integração externa atrás de uma interface**, com implementação fake para testes e demo. Testes rodam offline em segundos.
- **Segurança na borda**: autenticação verificada antes do parse, comparação em tempo constante, validação estrita de entrada, PII fora dos logs e dos prompts.
- **Decisões documentadas**: cada README tem tabela de decisão versus alternativa, e uma seção honesta do que não está coberto.
- **Observabilidade desde o início**: logs JSON com request id, métricas e custo estimado de LLM por job.

---

Aberto a conversas sobre engenharia de IA aplicada, backends Python e arquitetura de integrações. Me chame no [LinkedIn](https://www.linkedin.com/in/romeuow/).
