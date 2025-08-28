# 📄 Project Report: A Predictive Model for Jargon Identification and Simplification

**Project:** Development of a Heuristic-Based Jargon Simplifier  

---

## 1. Introduction
The goal of this project was to develop a system capable of identifying and simplifying domain-specific jargon within a given sentence.  
The project evolved from a simple dictionary-lookup approach to a more sophisticated predictive model.  
This model learns the statistical and grammatical characteristics of jargon from a sample dataset and applies this knowledge to identify and simplify new, previously unseen jargon in novel sentences.  

This report details:
- Data collection methods  
- The rationale for the chosen non-neural approach  
- Key challenges and lessons learned  

---

## 2. Data Collection Method
The project utilized a **two-pronged data collection strategy** to build its predictive capabilities.  
The model required examples of jargon and a baseline understanding of general language use to differentiate the two.

### 🔹 Primary Jargon Corpus (`dataset_1.csv`)
- A user-provided CSV containing sentence pairs.  
- Each pair had an **Original** sentence with jargon annotated (e.g., `**collusion**`) and a **Simplified** sentence with plain-language equivalents.  
- Built a *jargon frequency profile* — counts of how often each word appears in specialized contexts.  

### 🔹 General English Baseline Corpus (NLTK’s Brown Corpus)
- One million words from 15 genres (news, fiction, academic, etc.).  
- Served as a statistical baseline of “normal” English.  
- By comparing word frequency in this corpus vs. the jargon corpus, the model identifies jargon candidates.  

---

## 3. Non-Neural Approach Chosen and Rationale
Unlike modern NLP systems that default to neural networks, this project used a **heuristic-based statistical model**.  

### 📊 Model Logic
- **Statistical Rarity Score**:  
  - Calculates a “jargon score” as the ratio of frequency in the jargon corpus vs. the general corpus.  
  - High score → strong jargon candidate.  
- **Grammatical Role**:  
  - POS tagging using NLTK.  
  - Only nouns (`NN, NNS, NNP, etc.`) are considered as potential jargon.  
- A word is flagged as jargon **only if**:  
  - It surpasses the rarity score threshold, **and**  
  - It is tagged as a noun.  

### ✅ Why This Approach?
- **Interpretability** → Every decision is explainable.  
- **Data Efficiency** → Works with small datasets.  
- **Computational Speed** → Lightweight; no GPUs required.  
- **Targeted Solution** → Directly models the intuitive definition of jargon.  

---

## 4. Challenges and Lessons Learned

### ⚡ Challenge 1: Evolving from Memorization to Prediction  
- **Issue**: Initial approach looked like dictionary lookup.  
- **Lesson Learned**: Treat dataset as a statistical sample, not a lookup list.  

### ⚡ Challenge 2: Environment Instability and Tooling  
- **Issue**: Errors with package installations (spaCy, NLTK).  
- **Lesson Learned**: Stability of the development environment is critical; flexibility to pivot tools is vital.  

### ⚡ Challenge 3: The Nuance of “Simplification”  
- **Issue**: WordNet sometimes returns s
