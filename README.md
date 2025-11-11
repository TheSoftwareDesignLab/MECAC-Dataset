# MECAC: Multi-Ecosystem Mobile Accessibility Commit Corpus

##  Overview

**MECAC (Multi-Ecosystem Accessibility Commits Dataset)** is a public dataset containing **54,901 commits** related to **accessibility** extracted from **48 open-source mobile applications** built with **Kotlin, Java, Flutter, and Swift**.  

The dataset supports empirical research on how accessibility concerns **emerge, are documented, and evolve** throughout the software development lifecycle.  

Each commit includes:
-  **Standard metadata** (hash, author, timestamp, repository, programming languages).  
-  **The original developer-written message.**  
-  **A regenerated message** generated from the commit diffset using **Gemini 2.5 Flash**.  

This dual-message representation enables comparative analysis of human versus AI-generated descriptions, focusing on clarity, expressiveness, and semantic alignment with the corresponding code changes.

---

## Methodology

### Keyword Extraction and Semantic Clustering
- An initial list of accessibility-related keywords was derived from a **systematic literature review**.  
- Each keyword was embedded using **SentenceTransformer (all-mpnet-base-v2)** and clustered with **UMAP** and **HDBSCAN**, forming conceptual groups (e.g., *screen reader*, *contrast*, *gestures*, *focus*).  

### Commit Retrieval
- **48 GitHub repositories** were analyzed, totaling **603,738 commits**.  
- Only commits whose original messages contained at least one accessibility-related keyword were included, resulting in **54,901 relevant commits**.  

### LLM-Based Message Regeneration
- Each commit’s diffset was processed through **Gemini 2.5 Flash**, producing a **Conventional Commits–style** message.  
- The process used batching, throttling, and error handling for full reproducibility.  

### Manual Validation
- A stratified sample of **382 commits** was manually reviewed by two independent evaluators.  
- Around **39%** were confirmed as accessibility-related, covering all ecosystems (notably Flutter and Kotlin).  

---

##  Dataset Structure
The dataset is organized as follows:

dataset/

    master.csv → Master index file with metadata (repo, hash, author, date, keywords)

    commits/ → Original commit messages

    gen_commits/ → Regenerated AI messages

    diffsets/ → Code diffs (.patch) for each commit

The `master.csv` file is the main entry point, including commit identifiers, authors, matched keywords, and programming languages.

---

##  Analysis and Findings

A **keyword co-occurrence analysis** revealed three main thematic clusters:

-  **Semantic labeling and screen reader support** (*label*, *contentDescription*, *talkback*, *voiceOver*).  
-  **Interaction and navigation focus** (*focus*, *tap*, *gesture*).  
-  **Visual adaptability** (*dark mode*, *theme*, *UI*).  

These clusters demonstrate that accessibility work is multifaceted and often intersects with general UI maintenance and assistive technology support.

---

##  Reproducibility

Included in the repository:
-  Exact **prompt template** used for message regeneration.  
-  **Batch processing script** with throttling and error handling.  
-  Clear instructions for re-running with alternative LLMs.  

**Key design decisions:**
- **Keyword-based retrieval** for topic precision.  
- **Regeneration from diffsets**, not from original messages, to represent actual code-level intent.  
- **Separate storage** of original and regenerated messages for comparison.  

---

##  Known Limitations
- The filtering process relies on commits that **explicitly mention accessibility**, possibly omitting relevant but implicit changes.  
- Manual validation was performed on a stratified subset (382 commits), not on the full dataset.  

---

##  Future Work

Future research directions include:
1. **Evaluating the impact of regenerated messages** on accessibility detection — determining whether linguistic improvements increase or decrease keyword and semantic detection accuracy.  
2. **Training supervised learning models** to automatically classify accessibility-related commits.  
3. **Performing temporal and behavioral analyses** to understand how accessibility practices evolve over time and across ecosystems.  
4. **Integrating contributor-level metadata and static code analysis** to explore how accessibility issues are introduced, discussed, and resolved.  

---

##  Data Availability

The full dataset — including original and regenerated commit messages, diffsets, and the master index — is publicly available at:

 **[https://thesoftwaredesignlab.github.io/MECAC-Dataset/](https://thesoftwaredesignlab.github.io/MECAC-Dataset/)**  
