# AI Technical Reference

**A curated personal knowledge base on LLM internals, neural network architecture, and AI governance technical concepts — built by a Certified AI Governance Professional.**

A desktop reference book that bridges the gap between ML engineering and AI governance. Every chapter connects technical concepts (attention mechanisms, RLHF, tokenisation) to specific regulatory requirements (EU AI Act articles, ISO 42001 controls, NIST AI RMF measures) — so a governance professional can speak the language of the engineers and vice versa.

---

## Why This Exists

An AI Governance Professional needs to understand **what's under the hood** — not at researcher depth, but enough to assess risks, review model cards, evaluate benchmarks, and hold informed conversations with ML engineers. Commercial courses cover policy; this tool covers the technical substrate that policy regulates.

---

## What's Inside

**36 chapters across 6 parts**, each with Mermaid diagrams, comparison tables, and a Governance Relevance callout linking concepts to specific regulatory citations.

| Part | Chapters | Coverage |
|------|:--------:|----------|
| **I. Neural Network Foundations** | 1–4 | Neurons, training loop, loss functions, optimizers, history from perceptrons to transformers |
| **II. Transformer Architecture** | 5–11 | Attention, multi-head attention, positional encoding, layer norm, FFNs, tokenisation, encoder/decoder architectures |
| **III. Large Language Models** | 12–20 | Pre-training, fine-tuning, RLHF, inference, context windows, hallucination, emergent capabilities, prompt engineering, RAG |
| **IV. Technical Governance Concepts** | 21–29 | Model cards, weights & parameters, bias & fairness, explainability, benchmarks, AI system vs model, training data, red-teaming, guardrails |
| **V. Regulatory Deep-Dives** | 30–34 | EU AI Act high-risk requirements, GPAI obligations, ISO 42001 controls, NIST Measure function, cross-framework comparison |
| **VI. Professional Reference** | 35–36 | How to read ML research papers, A–Z glossary |

---

## Regulatory Frameworks Referenced

Every governance callout cites specific provisions from:

- **EU AI Act** — Articles 9–15 (high-risk), Articles 53 & 55 (GPAI), Annexes IV & XI
- **ISO/IEC 42001:2023** — Annex A control areas A.2–A.10
- **NIST AI RMF 1.0** — GOVERN, MAP, MEASURE, MANAGE functions and subcategories
- **ISO/IEC 23894:2023** — AI risk management guidance

---

## Technical Stack

| Component | Technology |
|-----------|-----------|
| Book engine | **mdBook** (Rust-native Markdown → HTML) |
| Diagrams | **mdbook-mermaid** (inline Mermaid rendering) |
| Desktop wrapper | **Tauri 2** (standalone .exe, no browser required) |
| Theme | Navy, full-text search enabled |

**Zero npm. Zero Node.js. Pure Rust toolchain.**

---

## Project Structure

```
mdBook-tool/
├── book.toml              # mdBook configuration
├── src/
│   ├── SUMMARY.md         # Table of contents (drives sidebar)
│   ├── introduction.md    # Landing page
│   ├── part1_foundations/  # Chapters 1–4
│   ├── part2_transformers/ # Chapters 5–11
│   ├── part3_llm/          # Chapters 12–20
│   ├── part4_governance/   # Chapters 21–29
│   ├── part5_regulatory/   # Chapters 30–34
│   └── part6_reference/    # Chapters 35–36
├── src-tauri/             # Tauri 2 desktop shell
│   ├── src/main.rs        # Entry point (5 lines)
│   ├── tauri.conf.json    # Window config, build hooks
│   └── icons/             # App icons (all platforms)
├── reference-docs/        # Primary regulatory source texts
└── book/                  # Built HTML output (gitignored)
```

---

## Build & Run

**Prerequisites:** Rust stable toolchain, `mdbook`, `mdbook-mermaid`

```bash
# Install tools (one-time)
cargo install mdbook mdbook-mermaid

# Build the book (HTML output in book/)
mdbook build

# Serve locally with hot-reload
mdbook serve --open

# Build standalone desktop .exe
cargo tauri build
```

The built installer is at `src-tauri/target/release/bundle/nsis/AI Technical Reference_0.1.0_x64-setup.exe`.

---

## Author

Built as a personal professional reference tool by a **Certified AI Governance Professional (CAIGP)** to support technical fluency in LLM internals, neural network architecture, and the regulatory frameworks that govern them.

Companion tool to the [GRC Command Centre](https://github.com/jahboukie) — together they cover both the operational compliance workflow and the technical knowledge base.
