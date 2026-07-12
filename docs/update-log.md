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
