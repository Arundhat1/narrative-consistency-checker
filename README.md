# Narrative Consistency Checker

An NLP system to verify whether a hypothetical character backstory is **consistent or contradictory** with a full-length novel (100k+ words), using retrieval-based evidence selection and LLM reasoning.

This project is built for **Track A**, focusing on **well-engineered use of NLP and GenAI**, rather than training new models.

---

## 🧠 Problem Overview

Given:
- A **full novel** (very long text)
- A **hypothetical backstory** for a character (not present in the novel)

The task is to determine whether the backstory:
- **(1) Consistent** with the events, character development, and narrative constraints of the novel  
- **(0) Contradictory** to the novel (explicitly or implicitly)

### Key challenges
- Long-context reasoning (novels cannot fit into LLM context)
- Global consistency over time
- Implicit contradictions (causal or narrative mismatch)
- Evidence-based decision making

---

## 🏗️ System Architecture

The solution is implemented as a **deterministic NLP pipeline**:

