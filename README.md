# Northbridge Policy Briefing Assistant

An evidence-grounded policy briefing assistant designed to help advocacy teams answer policy-sensitive questions using approved internal documentation while reducing unsupported claims, causal overstatements, and out-of-scope policy responses.

## Overview

Advocacy and community-relations teams often need to respond quickly to questions involving organizational priorities, program outcomes, and policy positions. These responses must remain consistent with documented evidence and approved organizational positions.

The Northbridge Policy Briefing Assistant addresses this challenge by retrieving relevant evidence from approved internal documents, applying deterministic governance controls, and producing structured responses with document-level and page-level citations.

The system is designed to augment human policy review rather than replace it.

## Key Capabilities

- Evidence retrieval from approved internal PDF documents
- TF-IDF and cosine-similarity retrieval
- Two-stage relevance validation
- Document name and page-level citations
- Detection of unsupported causal or overclaim language
- Detection of topics outside documented strategic scope
- Abstention when sufficiently relevant evidence is unavailable
- Human-review escalation for policy-boundary questions
- Optional LLM-based response generation
- Deterministic fallback mode that operates without an LLM

## System Architecture

```text
User Question
      ↓
TF-IDF Retrieval
      ↓
Query-Level Relevance Gate
      ↓
Chunk-Level Relevance Gate
      ↓
Deterministic Guardrails
      ↓
 ┌──────────────┬──────────────┬─────────────────┐
 │  Supported   │  Overclaim   │  Out-of-Scope   │
 ↓              ↓              ↓
Answer       Answer +       Scope Boundary
+ Evidence   Limitations    + Human Review
      │
      └──────────────┐
                     ↓
            Structured Response
            + Source Citations

Weak / unrelated retrieval
      ↓
Abstain
      ↓
No unsupported citations
