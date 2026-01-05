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
Novel Text
↓
Chunking + Embedding
↓
Vector Index (Retrieval)
↓
Backstory → Atomic Claims
↓
For each claim:
Retrieve relevant passages
↓
LLM-based consistency judgment
↓
Aggregate claim-level decisions
↓
Final Prediction (0 / 1) + Rationale

---

## 🔍 Approach Details

### 1. Novel Chunking
- The novel is split into overlapping chunks to handle long context.
- Chunking is designed to preserve narrative continuity while enabling retrieval.

### 2. Backstory Decomposition
- The backstory is broken into **atomic, verifiable claims** (e.g., childhood, education, fears, relationships).
- Each claim is checked independently against the novel.

### 3. Evidence Retrieval
- Semantic embeddings are used to retrieve the most relevant novel passages for each claim.
- Multiple passages from different parts of the novel are retrieved to capture global context.

### 4. Consistency Checking
- For each (claim, evidence) pair, an LLM determines whether the evidence:
  - **SUPPORTS**
  - **CONTRADICTS**
  - is **NEUTRAL**
- The model is prompted to reason explicitly before assigning a label.

### 5. Aggregation
- Any hard contradiction leads to a final label of **0 (Contradict)**.
- Otherwise, the backstory is labeled **1 (Consistent)**.
- A short textual rationale is generated summarizing key evidence.

---

## 🛠️ Tech Stack

- **Python**
- **Pathway** – data ingestion and document handling
- **Sentence Transformers** – semantic embeddings
- **LLM (API-based)** – claim extraction and reasoning
- **Vector similarity search** – evidence retrieval

---

## 📁 Project Structure
narrative-consistency-checker/
│
├── data/ # Input data (not tracked in git)
├── pipeline/ # Core pipeline modules
│ ├── chunking.py
│ ├── claims.py
│ ├── retrieval.py
│ ├── consistency.py
│ └── aggregate.py
│
├── notebooks/ # Experiments / analysis
├── main.py # End-to-end pipeline runner
├── requirements.txt
└── report.md # Detailed methodology & analysis
---

## 📊 Output Format

The system produces a CSV file with:

| Story ID | Prediction | Rationale |
|--------|------------|-----------|
| XYZ123 | 0 or 1 | Brief explanation of contradictions or support |

---

## ⚠️ Limitations

- Implicit narrative contradictions may still be ambiguous.
- Retrieval quality heavily affects reasoning accuracy.
- The system does not train new models; it relies on pretrained embeddings and LLMs.

---

## 🚀 Future Improvements

- Chapter-level summaries for stronger global reasoning
- Temporal modeling of character attributes
- Hybrid keyword + semantic retrieval
- Structured JSON outputs for consistency judgments

---

## 👤 Author

**Arundhati Datta Hangargekar**  
Computer Science & Engineering (3rd Year)  
Focus: NLP, ML systems, long-context reasoning




