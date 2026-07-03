# Maintenance Guide

## Source Policy

This public repository does not store raw X/Twitter exports, private spreadsheets, local data paths, or internal curation datasets.

Public traceability is maintained through each case heading:

```md
### Case X: [Title](source-link) (by [@author](author-link))
```

The source link points to the public post or public source, and the author link points to the creator profile.

## Case Selection Rules

Include only high-signal Seed-Audio 1.0 cases with concrete evidence:

- narration, dubbing, voiceover, or audiobook workflows
- audio-first video workflows
- hands-on audio scene, dialogue, musical scene, or soundscape demos
- reference voice, character voice, or image-guided audio tests
- provider, framework, assistant, or API integration notes
- pricing, quality, latency, limitation, or caveat reports

Exclude:

- pure hype or reaction-only posts
- prediction-only posts
- duplicate quote posts without new evidence
- unsupported claims without source context
- invented prompts or inferred results
- raw source exports, local monitor files, or private curation notes

## Update Checklist

1. Confirm the source is public and directly related to Seed-Audio 1.0.
2. Choose the best category based on the actual evidence.
3. Add a stable `<a id="case-x"></a>` anchor.
4. Use the `### Case X` heading format exactly.
5. Write a bold, reusable usage takeaway.
6. Keep notes grounded in the source.
7. Add `Type: ... | Date: YYYY-MM-DD`.
8. Rebuild the Menu and all localized README files with `python3 scripts/build_readmes.py`.
9. Re-run `python3 scripts/validate_repo.py`.
10. Confirm generated public links use the canonical repository owner `Evolink-AI`.

## Quick Start

The repository includes an EvoLink-only Quick Start section in every README. The section should use the Seed-Audio agent skill package rather than a raw API curl snippet:

- Install: `npm i evolink-seed-audio`
- API key: `https://evolink.ai/dashboard/keys?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases`
- Model page: `https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases`
- NPM package: `https://www.npmjs.com/package/evolink-seed-audio?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases`

Do not replace this section with non-EvoLink provider snippets. All generated external jump links should include GitHub UTM parameters.

## Video Playback

Video thumbnails in README files should link to GitHub Pages player pages under `docs/player/case-XX.html`.

The player pages use standard HTML video controls and load MP4 assets from `../../media/cases/`. Keep GitHub Pages configured to serve the `main` branch root so `docs/player/` and `media/cases/` are both available at:

`https://evolink-ai.github.io/Awesome-Seed-Audio-1.0-Guide-and-Usecases/`

Do not point README thumbnails directly at GitHub `blob/main/*.mp4` pages or `raw.githubusercontent.com` MP4 URLs. GitHub blob pages do not reliably render a video player for repository MP4 files, and raw MP4 links can download instead of opening a playback page.

## Rights And Media Policy

Repository-written README text, generated metadata, and maintenance documentation are licensed under CC BY 4.0. Public creator posts, attached media, downloaded thumbnails, and downloaded videos remain attributed to their original creators and source URLs.

See [MEDIA_RIGHTS.md](../MEDIA_RIGHTS.md) before reusing media outside this repository. If a creator, rights holder, or platform representative asks for correction or removal, open a correction issue and remove the affected media promptly.

## Suggested GitHub About

Description:

> Curated Seed-Audio 1.0 use cases for narration, audio drama, reference voices, provider integrations, and audio-first video workflows.

Website:

> https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=readme&utm_campaign=awesome-seed-audio-1.0-usecases

Topics:

`seed-audio`, `seed-audio-1-0`, `doubao`, `ai-audio`, `audio-generation`, `text-to-audio`, `voiceover`, `audio-drama`, `ai-video-workflow`, `evolink`, `multilingual-readme`
