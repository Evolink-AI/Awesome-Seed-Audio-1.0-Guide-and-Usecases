# Pull Request Checklist

## Case Evidence

- [ ] Every new case has a public source link.
- [ ] Every new case has a creator profile link.
- [ ] Claims are grounded in the source and do not invent prompts, scores, audio results, or pricing.
- [ ] Case type is one of: Demo, Tutorial, Evaluation, Integration, Benchmark, Limit.
- [ ] Date uses `YYYY-MM-DD`.

## README Structure

- [ ] Each new case has a stable `<a id="case-x"></a>` anchor.
- [ ] Case heading uses `### Case X: [Title](source-link) (by [@author](author-link))`.
- [ ] Menu links point to `#case-x`.
- [ ] English and localized README files keep the same case order and source links.
- [ ] No raw source exports, internal curation datasets, or local source paths are committed.

## Maintenance

- [ ] `docs/maintenance.md` still reflects current repository policy.
- [ ] `python3 scripts/build_readmes.py` has been run when case data changed.
- [ ] `python3 scripts/validate_repo.py` passes.

## Media And Public Surface

- [ ] README media renders from the repository's public R2 prefix; no new GitHub-hosted MP4 or public placeholder URL was introduced.
- [ ] `data/use-cases.json` records the matching `media.remote_url` and, for video, `media.poster_url`.
- [ ] The banner in every README matches `data/usecase-update-config.json`.
- [ ] EvoLink landing, key, model, and documentation links retain the required GitHub UTM fields.
- [ ] `Related Repositories` contains only verified public repositories or an explicit no-separate-repository statement.
- [ ] Public links, R2 objects, and rendered GitHub media have been checked before publication.
