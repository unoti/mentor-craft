# Ideas from the concept transcript to fold into the README and broader plan

The 00-concept transcript surfaces several tactical ideas that do not yet appear in the README. We should consider whether and how to incorporate each of these into the public narrative or the internal roadmap.

## Training data discipline and automation
- Establish a lightweight practice change where every feature begins with a committed "initial concept" artifact and ends with a committed final design + implementation snapshot. This check-in discipline unlocks automated pairing later.
- Build tooling that scans git history or pull requests to automatically detect those initial-vs-final checkpoints and assemble training pairs without manual curation.

## Richer supervision from past work
- Showcase example training pairs sourced from prior real-world projects so newcomers understand the depth and shape of the mentorship signal we expect to capture.
- Explore whether we can augment pairs with annotations inspired by prioritized experience replay (e.g., flagging especially surprising iterations) to bias fine-tuning toward the most informative sessions.

## Fine-tuning strategy questions
- Validate that LoRA-style adaptation is sufficient for capturing our workflows, and document decision criteria for escalating to fuller fine-tuning if capacity or quality ceilings appear.
- Consider a cadence (potentially daily) for regenerating adapted weights as new training pairs accumulate, so the agent evolves alongside ongoing projects.

## Evaluation and hypothesis testing
- Stand up a pipeline that extracts a sizable corpus of training pairs, then splits them into training and hold-out evaluation sets.
- Run an early experiment comparing design-doc quality when produced by the base model versus the fine-tuned model on the held-out prompts to quantify the delta and assess the core hypothesis that MentorCraft improves domain design effectiveness.
- Preserve a subset of hold-out examples for longitudinal re-testing so we can track drift as the model and data evolve.

