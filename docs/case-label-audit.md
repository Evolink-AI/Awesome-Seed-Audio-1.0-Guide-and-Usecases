# Case Label Audit

Date: 2026-07-16

This audit checks whether each public case is detailed enough to be useful and whether its `Type` label matches the linked source evidence.

## Label Rules

| Type | Use when |
|---|---|
| Tutorial | The source gives a reusable prompt, workflow, or step sequence that readers can adapt. |
| Demo | The source shows a concrete output or use pattern, but does not provide enough steps to be a tutorial. |
| Evaluation | The source reports hands-on quality, limits, cost, or production risk. |
| Integration | The source proves a provider, tool, MCP, or product access route. |
| Benchmark | The source includes an explicit comparison method or benchmark setup. |
| Limit | The source is mainly useful because it documents a constraint or failure mode. |

## Public Cases

| Case | Public Type | Evidence fit | Audit decision |
|---:|---|---|---|
| 1 | Tutorial | The source gives a concrete audio-first workflow: Seed Audio prompt, image prompt, and Seedance video prompt for a six-speaker scene. | Keep as Tutorial. It has reusable prompt structure and a visible workflow chain. |
| 2 | Evaluation | The source tests audio planning for an existing multi-clip video and preserves the mismatch issue between effects and on-screen action. | Keep as Evaluation. The value is the test method plus the limitation, not a finished recipe. |
| 3 | Tutorial | The source states a three-step workflow: generate audio, generate key visual, use both as Seedance references. | Keep as Tutorial. It is a concise official recipe readers can reproduce. |
| 4 | Tutorial | The source includes a two-minute prompt/script with INTENT, AESTHETIC, EXECUTION, ambience, voices, and dialogue. | Changed from Demo to Tutorial. The prompt format is reusable and detailed enough to learn from. |
| 5 | Demo | The source shows scene-level audio generation from a compact museum-guide prompt, including generated dialogue and character voices. | Keep as Demo. It proves capability, but does not provide enough production steps to be Tutorial. |
| 6 | Tutorial | The source describes a reference-voice MC workflow: generate a one-minute MC voice, split it, then use it for Seedance lip-sync. | Keep as Tutorial. It gives a practical sequence and a known downstream caveat. |
| 7 | Integration | The source announces audio generation inside Claude through Higgsfield MCP, including voiceover, cloning, and dubbing routes. | Keep as Integration. It is provider-route evidence, not a quality evaluation. |
| 8 | Evaluation | The source reports Japanese stability, emotion following, reference-audio precision, reference-mode limits, and high-voice artifacts. | Keep as Evaluation. It is strongest as a hands-on quality and limitation checklist. |
| 9 | Demo | The source narrates a public AITA-style story and frames it as a repeatable social content engine. | Keep as Demo. It shows a content pattern, while rights and growth validation remain outside the source. |
| 10 | Evaluation | The source tests image-guided character voice casting with three short lines and reports pitch/tone instability. | Keep as Evaluation. It defines an early casting use and an explicit production risk. |
| 11 | Evaluation | The source compares Seed Audio against native Seedance audio for voice acting and foley, and mentions low-cost 15-second tests. | Keep as Evaluation. It supports a cheap pre-production testing role, but not a complete final workflow. |
| 12 | Tutorial | The source gives a reusable sequence: Claude writes separate music-bed and SFX prompts, Seed Audio generates isolated passes, and Claude assembles them in Premiere for manual tuning. | Keep as Tutorial. The steps and isolation rationale are explicit, while the quality claim remains framed as the creator's production preference. |
| 13 | Evaluation | The selected parent post shows the finished fight clip, while the public thread reply publishes the exact Midjourney, Seedance 2.0, and Seed Audio prompts plus the timing-mismatch limitation. | Keep as Evaluation. The workflow is concrete and reusable, but the source explicitly says timing still drifted after repeated attempts. |
| 14 | Tutorial | The source publishes a step-by-step MiniMax Hub motion-graphics workflow: clone the creator voice with Seed Audio, generate narration, storyboard a 15-second piece, then add text, shape animation, BGM, and subtitles around the narration timeline. | Keep as Tutorial. It exposes a reusable narration-first production sequence rather than a launch-only integration mention. |
| 15 | Evaluation | The source documents an autonomous remix test: a Glif agent watches a video, rewrites the script, uses Seed Audio for a similar replacement voiceover, and reports pacing plus music limitations. | Keep as Evaluation. The workflow is concrete, but the author explicitly frames it as an experiment with unresolved quality issues. |

## Removed

The previous WaveSpeedAI provider-access case was removed from the public set. It showed availability and controls, but was less useful than the remaining workflow and evaluation cases for readers trying to learn how to apply Seed-Audio.

## Result

- Public cases: 15
- Strong-evidence cases retained: 15
- Removed cases in this audit pass: 1
- Type labels changed in this audit pass: Case 4 from Demo to Tutorial; Case 13 added as Evaluation; Case 14 added as Tutorial; Case 15 added as Evaluation
