# Case Label Audit

Date: 2026-06-29

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

## Removed

The previous WaveSpeedAI provider-access case was removed from the public set. It showed availability and controls, but was less useful than the remaining workflow and evaluation cases for readers trying to learn how to apply Seed-Audio.

## Result

- Public cases: 11
- Strong-evidence cases retained: 11
- Removed cases in this audit pass: 1
- Type labels changed in this audit pass: Case 4 from Demo to Tutorial
