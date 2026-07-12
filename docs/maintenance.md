# Maintenance Guide

## Source Policy

This public repository does not store raw X/Twitter exports, private spreadsheets, local data paths, or internal curation datasets.

Public traceability is maintained through each case heading:

```md
### Case X: Title (source URL, by author profile URL)
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

## Recurring Update Contract

The scheduled update runs every two days at 10:00 Asia/Shanghai and searches X with the exact phrase `"seed audio"` over the preceding 48 hours.

- Add no more than 10 high-confidence use cases per run; quality takes priority over filling the cap.
- Preserve unsure candidates in local review evidence and drop unsupported, duplicate, or irrelevant candidates.
- Run the handoff verifier, README/data validator, localization parity check, R2 origin check, template audit, repository review, conversion-surface audit, and public-link audit before publication.
- Push only when all P0/P1 findings are zero. A clean verified no-op is valid when no candidate qualifies.
- A run is complete only after the published commit and GitHub Actions result are read back from GitHub.

See [Recurring Update Contract](recurring-update-contract.md) for the full public contract.

## Quick Start

The repository includes an EvoLink-only Quick Start section in every README. It keeps both the published Seed-Audio package path and a minimal official API request:

- Install: `npm i evolink-seed-audio`
- API key: `https://evolink.ai/dashboard/keys?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=api_key`
- Model page: `https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=quickstart&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=model_link`
- NPM package: `https://www.npmjs.com/package/evolink-seed-audio`
- Endpoint: `POST https://api.evolink.ai/v1/audios/generations`
- Model: `doubao-seed-audio-1-0`

Do not replace this section with non-EvoLink provider snippets. All generated external jump links should include GitHub UTM parameters.

## Video Playback

Video posters in README files must render from the public R2 URL recorded as `media.poster_url` and link directly to the R2-hosted MP4 URL recorded as `media.remote_url`. Image cases must render from `media.remote_url`.

The repository keeps local preview thumbnails under `media/cases/`, but it does not keep MP4 files in git. R2 video URLs use the public R2 domain plus this object-key prefix: `github-repo/Awesome-Seed-Audio-1.0-Guide-and-Usecases/videos/`.

Do not point README thumbnails at GitHub `blob/main/*.mp4` pages, `raw.githubusercontent.com` MP4 URLs, or local `media/cases/*.mp4` paths. If a video changes, upload the new MP4 to R2, update `media.remote_url`, run `python3 scripts/build_readmes.py`, and re-run `python3 scripts/validate_repo.py`.

## Rights And Media Policy

Repository-written README text, generated metadata, and maintenance documentation are licensed under CC BY 4.0. Public creator posts, attached media, downloaded thumbnails, and downloaded videos remain attributed to their original creators and source URLs.

See [MEDIA_RIGHTS.md](../MEDIA_RIGHTS.md) before reusing media outside this repository. If a creator, rights holder, or platform representative asks for correction or removal, open a correction issue and remove the affected media promptly.

## Suggested GitHub About

Description:

> Curated Seed-Audio 1.0 use cases for narration, audio drama, reference voices, provider integrations, and audio-first video workflows.

Website:

> https://evolink.ai/seed-audio-1-0?utm_source=github&utm_medium=about&utm_campaign=awesome-seed-audio-1.0-usecases&utm_content=website

Topics:

`seed-audio`, `seed-audio-1-0`, `doubao`, `ai-audio`, `audio-generation`, `text-to-audio`, `voiceover`, `audio-drama`, `ai-video-workflow`, `evolink`, `multilingual-readme`
