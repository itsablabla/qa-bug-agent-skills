---
name: fix-ai-agent-features
description: Fix defects in LLM and agent features — prompt injection, data leakage, unsafe output handling, excessive tool agency, runaway cost, inconsistent or ungrounded outputs — with server-side permission checks, escaping, budgets, and grounding rules. Use for any model- or agent-driven feature bug.
---
# Fix AI and Agent Features

## Procedure
1. Treat model input and output as untrusted. Escape output before HTML, shell, SQL, or templates.
2. Injection: separate instructions from data; strip or quarantine instruction-like content from retrieved pages, emails, files, and API responses; never let content trigger tools on its own.
3. Agency: tools check the user's permissions on the server; consequential actions need approval enforced outside the model.
4. Leakage: scope retrieval and memory by tenant; keep secrets out of prompts.
5. Cost and loops: token, time, and tool-call budgets with hard stops.
6. Consistency: fix the cause of score drift (temperature, nondeterministic inputs, unstable rubric); prove spread on 3+ runs is within tolerance.
7. Grounding: every claim maps to provided evidence; free versus paid content can't leak through paraphrase.
8. Check each OWASP Agentic item (ASI01–ASI10) touched by the change.

## Exit criteria
The tester's AI suite passes, including injection cases, budgets trip correctly, and consistency is within tolerance.

Counterpart of tester skill: `qa-ai-agent-testing`.
