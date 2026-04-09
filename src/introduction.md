# AI Technical Reference

*Last reviewed: April 2026*

## Purpose

This book is a personal, curated knowledge base built by and for a Certified AI Governance Professional. It exists to solve one problem: **bridging the gap between regulatory language and technical reality**.

When the EU AI Act references "appropriate levels of accuracy, robustness and cybersecurity" (Article 15), what does that mean in engineering terms? When a development team presents a model card claiming "bias-mitigated training," what specifically should you look for? When ISO 42001 requires evidence of "AI system performance monitoring," what does that evidence actually look like?

This reference answers those questions.

## Who This Is For

One person — the author. This is not a textbook, a tutorial, or an introduction to AI. It is a working reference for someone who:

- Conducts AI governance assessments across multiple regulatory frameworks
- Needs to engage credibly with ML engineers, data scientists, and AI product teams
- Must translate between regulatory requirements and technical implementation
- Reviews model documentation, risk assessments, and technical evidence artifacts

## How This Book Is Organized

| Part | Focus | When You Reach For It |
|------|-------|-----------------------|
| **I. Neural Network Foundations** | How neural networks work at the component level | When you need to understand what "weights," "training," or "gradient descent" actually means |
| **II. The Transformer Architecture** | The specific architecture behind modern LLMs | When reviewing system documentation that references attention, encoders, or transformer blocks |
| **III. Large Language Models** | How LLMs are built, trained, and deployed | When assessing training practices, fine-tuning claims, or inference configurations |
| **IV. Technical Governance Concepts** | The technical concepts that appear in regulatory requirements | Your primary daily reference — model cards, bias, explainability, benchmarks, red-teaming |
| **V. Regulatory Technical Deep-Dives** | Framework requirements mapped to engineering practices | When you need to know exactly what technical evidence satisfies a specific obligation |
| **VI. Professional Reference** | Glossary and research paper reading guide | Quick lookups and skill-building |

## How to Use This Reference

- **Use the search** (magnifying glass icon or press `S`) — it indexes every chapter. If a developer mentions "LoRA" in a meeting, search it.
- **Start with Part IV or V** if you need something for an active assessment. Parts I–III are background reading.
- **Every chapter has a "Governance Relevance" section** that explicitly connects the technical concept to regulatory language you encounter in your work.
- **Diagrams are intentional**, not decorative. Each one reduces cognitive load on a specific concept. Study them.

## Conventions

> **Governance Relevance** — Callout boxes like this appear in every chapter. They bridge the technical content to specific regulatory requirements, articles, or assessment scenarios.

Terms that appear in the **Glossary** are **bolded** on first use in each chapter.
