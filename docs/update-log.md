# Update Log

## June 29, 2026

- Rebuilt the repository to follow the EvoLink usecase repository template.
- Collected recent X/Twitter `"seed audio"` content from June 24-29, 2026 through the local search workflow.
- Accepted 93 deduplicated recent posts from 182 raw returned posts.
- Revisited the original X/Twitter post and thread context for 20 candidate usecases.
- Applied the final strong-evidence policy: retained 11 source-reviewed usecases and removed weak or lower-utility candidates from the public README set.
- Updated `data/use-cases.json` with 11 renumbered strong-evidence cases and source-grounded notes.
- Downloaded related media for all 11 retained cases into `media/cases/` and rendered the media in generated README files.
- Updated `data/use-case-translations.json` and rebuilt English plus 10 localized README variants.
- Converted the preset voice list into a documentation jump instead of a front-loaded README section.
- Added banner asset, community files, issue templates, maintenance docs, and public source index.
- Kept internal source-review artifacts out of the public repository while preserving public source links and case metadata.
- Updated static validation so the current acceptance target is `case_count=11`, `localized_readmes=11`, full localized case translation coverage, downloaded case media, and a clean public file set.
- Published the verified update to `Evolink-AI/Awesome-Seed-Audio-1.0-Guide-and-Usecases` on branch `main`.
- Removed the previous Case 11 provider-access item, renumbered the final public set to 11 cases, expanded each remaining case into more actionable source-grounded notes, and added `docs/case-label-audit.md`.
- Changed video presentation to clickable thumbnails that open GitHub Pages player pages under `docs/player/` instead of non-playable GitHub blob pages or raw MP4 download links.
- Updated README links so key acquisition points to EvoLink Dashboard Keys, banner and model CTAs point to the Seed-Audio model page, and Quick Start uses `npm i evolink-seed-audio`; all generated external links include GitHub UTM parameters.

## July 7, 2026

- Uploaded all public case MP4 videos to Cloudflare R2.
- Rebuilt README thumbnail links so clicking a preview image opens the corresponding public R2 MP4 URL.
- Removed local `media/cases/*.mp4` files from the git worktree and added an ignore rule to keep future MP4 downloads out of GitHub.
- Kept local JPG thumbnails in `media/cases/` for README previews.

## July 12, 2026

- Ran the recurring exact-phrase `"seed audio"` search over a fixed 48-hour window.
- Reviewed 14 in-window candidates: selected 1 high-confidence workflow, marked 3 unsure, and dropped 10 question-only, hype-only, duplicate, unrelated, or showcase-only posts.
- Added Case 12: a Claude-to-Seed-Audio-to-Premiere workflow that separates music, sound effects, and voice passes before manual timing and fade control.
- Uploaded the Case 12 source screenshot to the repository's locked Cloudflare R2 namespace and preserved the tracked local source image.
- Updated English and all 10 localized README files while preserving source URL, author URL, case number, evidence type, date, and stable anchor parity.
- Added `data/usecase-update-config.json` so recurring updates use the repository's localized case-heading prefixes and structured-data boundary.
- Updated the generated Quick Start to include the verified `POST https://api.evolink.ai/v1/audios/generations` request and closed conversion-surface P0/P1 findings before publication.

## July 14, 2026

- Ran the recurring exact-phrase `"seed audio"` search over a fixed 48-hour window ending at the collector timestamp.
- Reviewed 21 in-window candidates: selected 1 high-confidence workflow, marked 3 unsure, and dropped 17 weak, duplicate, question-only, incidental, or showcase-only posts.
- Added Case 13: a reference-audio fight-commentary timing evaluation that uses a finished Seedance edit, GPT-5.6-written commentary, and Seed Audio timeline prompting.
- Preserved the public prompt boundary by linking the selected parent post while grounding the case notes in the public thread reply that exposes the exact Midjourney, Seedance 2.0, and Seed Audio prompts.
- Uploaded the Case 13 poster image and MP4 to the repository's locked Cloudflare R2 namespace, kept the tracked local poster, and kept the MP4 out of git.
- Rebuilt English and all 10 localized README files, player pages, and structured case data while preserving source URL, author URL, case number, evidence type, date, anchor parity, and R2 media URLs.
- Expanded the generated Quick Start into a runnable async create-task plus poll flow so the repo passes the current conversion-surface contract for async models.

## July 16, 2026

- Ran the recurring exact-phrase `"seed audio"` search over the fixed 48-hour window ending at collector timestamp `2026-07-16T10:05:27.755966+00:00`.
- Reviewed 22 in-window candidates: selected 2 high-confidence workflows, marked 3 unsure, and dropped 17 launch-only, incidental, duplicate, media-only, or overlapping posts.
- Added Case 14: a MiniMax Hub motion-graphics workflow that clones the creator voice in Seed Audio, uses narration as the timing spine, and then builds storyboard, text, shape animation, BGM, and subtitles around it.
- Added Case 15: an autonomous Glif-agent evaluation that rewrites an existing video's tone, uses Seed Audio to generate a matching replacement voiceover, and flags pacing plus music as unresolved review points.
- Uploaded the Case 14 and Case 15 poster images and MP4 files to the repository's locked Cloudflare R2 namespace, kept the tracked local poster JPG files, and kept the MP4 files out of git.
- Updated `data/use-cases.json`, `data/use-case-translations.json`, and `data/source-index.json` while preserving case order, source attribution, stable anchors, media URL format, and locale parity.
- Rebuilt English and all 10 localized README files plus GitHub Pages player pages from the updated structured data.
