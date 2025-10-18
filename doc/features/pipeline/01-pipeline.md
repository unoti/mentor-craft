# Training Pair Completion Agent Pipeline

## Overview
This document proposes a follow-up agent workflow that takes an initial feature pitch and the final merged pull request, then builds a complete training pair capturing the full design journey. The pipeline focuses on gaps between the initial design document and the implemented solution so that future models learn how real projects evolve beyond the first draft.

## Objectives
- Produce a second-phase design narrative that reflects the final pull request scope, including emergent requirements.
- Capture question-and-answer exchanges that explain why the solution diverged from the initial document.
- Automate packaging of both halves of the training pair (initial concept document and retrospective completion doc) for fine-tuning.

## Inputs
1. **Initial feature document**: the concept or pitch committed before implementation.
2. **Final pull request**: merged code, final design notes, and PR description.
3. **Repository context**: relevant code snippets or transcripts referenced in the PR.

## Pipeline Stages
1. **Artifact Collection**
   - Retrieve the initial feature document and final PR metadata (description, linked issues, review comments).
   - Pull the diff and any attached design notes from the final PR.

2. **Gap Analysis Questioning**
   - Run an LLM agent that compares the initial document against the final PR.
   - Have the agent ask targeted questions about missing or expanded scope items—for example, new constraints, refactors, or bug fixes introduced during implementation.
   - Iterate until the agent can enumerate all significant differences and the rationale behind them.

3. **Retrospective Narrative Assembly**
   - Generate a structured completion document that answers the agent's questions and documents how each new issue was resolved.
   - Include sections for "Unexpected Challenges," "Implementation Adjustments," and "Testing & Validation."
   - Cite specific commits or code segments when referencing solutions.

4. **Training Pair Packaging**
   - Combine the initial feature document with the retrospective completion document into a standardized training pair schema (e.g., JSONL with `initial_context` and `final_context`).
   - Store metadata such as repository name, PR number, and timestamps for traceability.

## Output Format
- **Completion Document**: Markdown file that mirrors the tone and structure of the initial feature doc but highlights the actual work delivered.
- **Training Pair Artifact**: Serialized record ready for ingestion by the fine-tuning pipeline.

## Implementation Considerations
- Maintain a prompt library that nudges the questioning agent toward practical implementation details (tests added, edge cases handled, cleanup work).
- Integrate with version control APIs (GitHub/GitLab) to gather PR timelines and reviewer feedback.
- Support manual review/approval before finalizing each training pair to ensure accuracy.

## Open Questions
- How do we detect when the final PR bundles unrelated fixes that should form separate training pairs?
- What heuristics decide when the questioning loop has gathered enough context to finalize the retrospective document?
- Should we embed reviewer discussion threads directly into the training pair for richer supervision?

