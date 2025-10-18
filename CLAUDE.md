# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MentorCraft is an experimental framework for evolving LLM agents through iterative mentorship and workflow refinement. The core concept is to create a feedback loop where agents improve over time by learning from real-world design interactions.

**Current Status**: Early conceptual/planning phase. No implementation exists yet.

## Core Concept

The framework aims to capture training pairs from normal development workflows:
- **Input**: Initial vague feature requests or concepts
- **Output**: Refined design documents and tested implementations

These pairs are intended for:
- LoRA fine-tuning to adapt models to specific workflows
- Creating domain-specific training data
- Building retrieval-augmented memory systems

## Architecture Philosophy

### The MentorCraft Pipeline (Planned)

1. **Capture Sessions**: Store initial prompts and resulting designs/code
2. **Pair Examples**: Match vague requests to refined outputs
3. **Annotate** (optional): Add reasoning, tradeoffs, decision notes
4. **Tag & Store**: Categorize by topic, difficulty, or system area

### Key Design Principles

- Establish check-in discipline: commit "initial concept" artifacts before iteration, then commit final design + implementation
- Build tooling to scan git history/PRs to automatically detect initial-vs-final checkpoints
- Generate training pairs without manual curation
- Use LoRA-style adaptation for capturing workflows (escalate to fuller fine-tuning if needed)
- Consider daily regeneration of adapted weights as new training pairs accumulate

### Evaluation Strategy (Future)

From `doc/planning/ideas.md`:
- Extract corpus of training pairs, split into training and hold-out sets
- Compare design-doc quality: base model vs fine-tuned model on held-out prompts
- Preserve subset for longitudinal re-testing to track drift

## Repository Structure

```
doc/
  transcripts/     # Design discussions and concept explorations
  planning/        # Strategic planning documents and ideas
```

## Important Context

- This is an **experimental** project focused on the meta-problem of agent learning
- The name "MentorCraft" reflects the bidirectional nature of human-AI partnership
- Development workflow will itself become training data for the system
- Initial implementation language/framework not yet determined
- Target use case: coding agents that learn user preferences and domain patterns over time

## Future Implementation Areas

When implementing features, consider these planned capabilities:
- Training pair extraction from git history
- Automated pairing of initial concepts with final implementations
- Annotation tools for decision tradeoffs
- LoRA fine-tuning pipeline
- Evaluation harness for measuring adaptation quality
- Potential extensions: mentor feedback scoring, reflection loops, tool usage recording, session DAGs
