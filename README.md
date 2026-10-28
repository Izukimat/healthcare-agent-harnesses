# Agent Harnesses in Healthcare — Initial Reading Plan

**Research Team: Izuki, Peter & Karen**

**Objective:** Develop a shared understanding of agent harness engineering, examine existing research in healthcare, and identify opportunities for original research.

### Priority Definitions

- **Essential** — Read carefully; important for our shared research direction.
- **Recommended** — Read the main concepts, findings, and relevant sections.
- **Optional** — Reference material or technical deep dive; revisit as needed.

---

## Week 1 — Foundations: Agents, Harnesses & Evaluation

**Goal:** Understand what an agent harness is, how it differs from an LLM or agent framework, and why execution-time control matters.

| Reading | Video digest | Focus | Peter & Karen | Izuki |
|---|---|---|---|---|
| **1. [Building Effective Agents — Anthropic](https://www.anthropic.com/research/building-effective-agents)** | [▶ Watch (3:39)](#reading-1-video-digest) | The differences between LLMs, workflows, and autonomous agents. Understand tool calling, agent loops, routing, and orchestration. Focus on *when agents are necessary* and when simpler workflows are preferable. | **Essential** | **Essential** |
| **2. [What Is an Agent Harness? — Google Cloud](https://cloud.google.com/discover/agent-harness)** | Not planned (short reading) | The fundamental definition and architecture of a harness. Understand execution loops, tool management, context, memory, state persistence, guardrails, and observability. Identify which responsibilities belong to the model versus the surrounding system. | **Essential** | **Essential** |
| **3. [Demystifying Evals for AI Agents — Anthropic](https://www.anthropic.com/research/demystifying-evals-for-ai-agents)** | [▶ Watch (4:51)](#reading-3-video-digest) | How to evaluate agents beyond final-answer accuracy. Understand outcome evaluation, execution traces, code-based graders, model-based graders, expert human evaluation, and the importance of realistic failure scenarios. | **Essential** | **Essential** |
| **4. [LLM06: Excessive Agency — OWASP](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/)** | — | Why excessive permissions, tool access, and autonomy create safety risks. Consider how these risks could manifest in clinical environments, particularly with EHR access, medication orders, and other consequential operations. | **Essential** | **Recommended** |

**Video digests:** Videos for Readings 1 and 3 are optional introductions prepared by Izuki; use the linked original articles for the full discussions. Reading 2 is short, so no companion video is planned. Video digests for selected longer readings are in progress. Reading priorities remain unchanged.

### Questions for our first discussion

1. What distinguishes an LLM, an agent, an agent framework, and an agent harness?
2. Which harness capabilities are most important for healthcare, and why?
3. Why might a clinically correct final answer still conceal an unsafe execution process?

---

## Week 2 — Harness Engineering: Architecture & Implementation

**Goal:** Understand the mechanisms inside an agent harness, particularly state management, verification, recovery, tracing, and tool-level safeguards.

| Reading | Video digest | Focus | Peter & Karen | Izuki |
|---|---|---|---|---|
| **5. [Effective Harnesses for Long-Running Agents — Anthropic](https://www.anthropic.com/research/effective-harnesses-for-long-running-agents)** | — | Challenges of maintaining progress across long-running tasks and limited context windows. Understand state continuity, structured handoffs, context compaction, and why agents can lose track of previously completed actions. | Recommended | **Essential** |
| **6. [Harness Engineering: Leveraging Codex in an Agent-First World — OpenAI](https://openai.com/index/harness-engineering/)** | — | How engineering teams design environments, observability, constraints, feedback loops, and infrastructure that enable reliable autonomous operation. Focus on harness engineering as a systems discipline rather than purely prompt engineering. | Optional | **Essential** |
| **7. [Persistence & State Management — LangGraph](https://github.com/langchain-ai/docs/blob/main/src/oss/langgraph/persistence.mdx)** | — | Checkpoints, persisted state, interruption recovery, durable execution, and the distinction between short-term execution state and long-term memory. Consider the consequences of interrupted or duplicated clinical transactions. | Optional | **Essential** |
| **8. [OpenAI Agents SDK — Architecture & Documentation](https://openai.github.io/openai-agents-python/)** | — | A practical reference for agent loops, tools, handoffs, sessions, guardrails, and tracing. Examine which components are implemented by the SDK and which safeguards remain the application's responsibility. | Optional | **Essential** |
| **9. [Guardrails — OpenAI Agents SDK](https://openai.github.io/openai-agents-python/guardrails/)** | — | Input, output, and tool-level validation. Understand the difference between checking an agent's response and preventing a potentially harmful external action before execution. | Recommended | **Essential** |
| **10. [Synthea — Synthetic Patient Data](https://synthetichealth.github.io/synthea/)** | — | Explore how synthetic patient histories, medications, allergies, and encounters can support controlled healthcare AI experiments without requiring identifiable patient records. Consider the clinical realism and limitations of synthetic cases. | Recommended | Recommended |

### Suggested exercise

Build or demonstrate a minimal agent interacting with a simulated medication record. Compare its behavior with and without basic execution safeguards.

**Discussion questions:**

1. What happens if an agent retries a medication update after a timeout?
2. How can a harness distinguish an unsuccessful operation from an operation that succeeded but returned no confirmation?
3. Which safety checks should be deterministic, and which require clinical judgment?

---

## Week 3 — Existing Original Research in Healthcare Agents

**Goal:** Understand what has already been demonstrated, how previous experiments were designed, and what scientific questions remain open.

| Reading | Video digest | Focus | Peter & Karen | Izuki |
|---|---|---|---|---|
| **11. [MedicalHarness: A Controlled Evaluation of LLMs and Agent Harnesses on Medical Tasks](https://arxiv.org/abs/2610.05778)** — 2026 preprint | — | A direct comparison of multiple models and harnesses across medical tasks. Focus on the experimental controls, outcome variability, ablation studies, and model–harness interactions. Identify what this work establishes and what remains untested. | **Essential** | **Essential** |
| **12. [MedHarnessBench: A Unified Benchmark for Healthcare Agent Evaluation](https://arxiv.org/abs/2610.15714)** — 2026 preprint | — | Seven healthcare-specific evaluation dimensions, including workflow continuity, auditability, verification, and conduct boundaries. Examine whether these dimensions reflect real clinical risks and whether their measurements adequately capture safety. | **Essential** | **Essential** |
| **13. [Benchmarking Large Language Model-Based Agent Systems for Clinical Decision Tasks — npj Digital Medicine](https://www.nature.com/articles/s41746-026-02443-6)** — 2026 | — | Controlled evaluation of medical agent systems against baseline LLMs. Focus on modest performance gains, computational costs, hallucination mitigation, benchmark selection, and the relationship between agent complexity and practical value. | Recommended | **Essential** |
| **14. [AgentClinic: A Multimodal Benchmark for Tool-Using Clinical AI Agents — npj Digital Medicine](https://www.nature.com/articles/s41746-026-02674-7)** — 2026 | — | How simulated clinical encounters can be used for agent evaluation. Explore the strengths and weaknesses of simulated patients, multimodal information gathering, and multi-step clinical decision-making. | Recommended | Recommended |
| **15. [FHIR-AgentEval: A Modular Sandbox for Benchmarking Clinical LLM Agents — npj Digital Medicine](https://www.nature.com/articles/s41746-026-03348-0)** — 2026 | — | Evaluation of agents using realistic FHIR operations and a resettable server. Pay particular attention to server-state validation, deterministic evaluation, memory configurations, and controlled ablation experiments. | Recommended | **Essential** |

### Questions for our research discussion

1. Which findings from MedicalHarness and MedHarnessBench are convincing, and which need stronger validation?
2. Are existing benchmarks measuring clinical safety, or primarily technical task completion?
3. How could we design an experiment that answers a question these studies have not addressed?
4. Which research questions could produce findings generalizable beyond healthcare?

**Expected output:** A preliminary research-gap matrix comparing existing studies, their evaluation methods, limitations, and possible extensions.

---

## Week 4 — Clinical Context, Research Gaps & Future Review

**Goal:** Connect harness engineering to established healthcare safety principles, identify promising research questions, and begin organizing literature for a potential review paper.

| Reading | Video digest | Focus | Peter & Karen | Izuki |
|---|---|---|---|---|
| **16. [A Comprehensive Survey of AI Agents in Healthcare — Journal of Biomedical Informatics](https://doi.org/10.1016/j.jbi.2026.105045)** — 2026 | — | A broad survey synthesizing more than 200 healthcare-agent studies. Understand the existing taxonomy, clinical applications, evaluation methods, and gaps. Determine how a harness-focused review could contribute something distinct from a general survey of healthcare agents. | **Essential** | Recommended |
| **17. [SAFER Guides — U.S. Office of the National Coordinator for Health IT](https://healthit.gov/clinical-quality-and-safety/safer-guides/)** | — | Established principles for safe EHR operation, patient identification, computerized order entry, system management, and organizational responsibilities. Translate these clinical safety requirements into potential harness design constraints and evaluation metrics. | **Essential** | Recommended |
| **18. [HL7 FHIR — MedicationRequest Resource](https://hl7.org/fhir/R4/medicationrequest.html)** | — | Understand how medication orders are represented in a structured clinical information system. Examine identifiers, statuses, patient references, and workflow semantics relevant to simulated agent actions. | Recommended | Recommended |

### Questions for our fourth discussion

1. Which existing healthcare safety requirements could become enforceable harness constraints?
2. Which failure modes are insufficiently covered by current medical-agent benchmarks?
3. Is there a scientifically novel question that we can test within a controlled, synthetic environment?
4. What would distinguish a future review titled *Agent Harnesses in Healthcare* from existing reviews of healthcare AI agents?

**Expected output:** A shortlist of two or three possible Original Research questions, supported by a literature-gap analysis.

---

## Expected Outcomes After Four Weeks

By the end of this initial reading phase, we should aim to produce:

1. **A shared conceptual framework** distinguishing models, agents, agent frameworks, runtime harnesses, and evaluation harnesses.
2. **A preliminary healthcare harness taxonomy**, identifying the components most relevant to clinical safety and workflow reliability.
3. **A research-gap matrix** covering the most relevant existing studies and their limitations.
4. **A short list of Original Research opportunities**, assessed for novelty, clinical relevance, experimental feasibility, and generalizability.
5. **An initial literature collection** that can eventually support a separate review paper.

Our immediate goal is not to decide on a final manuscript title or journal. It is to become sufficiently familiar with the field to formulate a defensible and genuinely novel research question.

The technical and clinical readings are intentionally weighted differently. We do not all need to understand implementation details at the same depth, but we should all be able to evaluate the research questions, experimental assumptions, and significance of the findings.


---

## Watch video digests

Play these viewing copies directly on GitHub. Full-size original MP4 downloads are also available below each player.

### Reading 1 video digest

[Building Effective Agents — Anthropic](https://www.anthropic.com/research/building-effective-agents) · **3:39** · prepared by Izuki

https://github.com/user-attachments/assets/c339906d-bfc1-4900-a497-e605aed41d1c

[Download original MP4](https://github.com/Izukimat/healthcare-agent-harnesses/releases/download/reading-01-digest/reading-01-building-effective-agents.mp4)

### Reading 3 video digest

[Demystifying Evals for AI Agents — Anthropic](https://www.anthropic.com/research/demystifying-evals-for-ai-agents) · **4:51** · prepared by Izuki

https://github.com/user-attachments/assets/7af09962-7f1b-4c91-a877-d5f4c093bccd

[Download original MP4](https://github.com/Izukimat/healthcare-agent-harnesses/releases/download/reading-03-digest/reading-03-demystifying-evals-for-ai-agents.mp4)
