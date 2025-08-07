# ArtOS — Research Prototype

**ArtOS** is a student-led research project exploring the design of an **LLM-aware operating layer** that can run large language models under strict security, anti-hallucination, and capability-scoped controls.

The goal is to treat an LLM **not as a trusted decision-maker**, but as an **untrusted coprocessor** operating within a controlled environment.  
This project investigates how operating system principles (capabilities, sandboxing, syscall mediation, auditing) can be adapted to the unique security and reliability challenges of LLM-based systems.

---

## 🎯 Research Objectives
1. **Investigate hallucination-resistant architectures** for LLM-powered systems.
2. **Design and prototype a capability-based syscall interface** for LLMs.
3. **Integrate retrieval-anchored output validation** to ensure grounded answers.
4. **Evaluate sandboxing approaches** (e.g., WASM, microVMs) for LLM tools.
5. **Develop auditing and policy enforcement mechanisms** tailored for AI agents.

---

## 🧩 Research Questions
- How can traditional OS security models (e.g., capability systems, mandatory access control) be adapted to control LLM behaviour?
- What schema enforcement and fact-checking methods most effectively reduce hallucinations?
- How can we prevent LLMs from executing unsafe tool actions (e.g., prompt injection, SSRF) without overly restricting functionality?
- Can a syscall broker for LLMs be made general-purpose, supporting different AI models and domains?

---

## 📐 Proposed Architecture (Prototype)

User Query  
↓  
LLM Interface (Untrusted)  
↓  
Syscall Broker (Go)  
  • Capability Check  
  • SchemaGuard  
  • FactGuard  
↓  
Policy Engine (Rust)  
↔  
Tool Sandbox (WASM)  
↓  
Audit Ledger (Tamper-evident)

--- 


---

## 📅 Research Plan & Milestones

### Phase 1 – Literature Review (Weeks 1–2)
- Study existing OS capability systems and AI safety tooling.
- Review LLM security and hallucination mitigation research.

### Phase 2 – Architecture Design (Weeks 3–4)
- Define syscall broker interface and capability token format.
- Draft JSON Schemas for tool inputs/outputs.
- Select sandboxing technology (WASM for MVP).

### Phase 3 – Prototype Implementation (Weeks 5–8)
- Build broker (Go) with schema validation and audit logging.
- Implement policy engine (Rust) with basic allow/deny rules.
- Create two WASM tools (`retriever`, `kv`).

### Phase 4 – Testing & Evaluation (Weeks 9–10)
- Simulate normal usage, malicious prompts, and injection attempts.
- Measure hallucination rate reduction vs. baseline LLM.

### Phase 5 – Reporting (Weeks 11–12)
- Document architecture, implementation details, and test results.
- Identify limitations and future work.

---

## 🛡️ Security Principles
1. **LLM is never root** — all actions require explicit, scoped capability tokens.
2. **Grounded output** — every answer must be supported by retriever-sourced citations.
3. **Schema-constrained communication** — outputs are validated before acceptance.
4. **Fail closed** — if validation or policy checks fail, the operation is blocked.

---

## 📜 License
MIT (Open for research and educational use)

