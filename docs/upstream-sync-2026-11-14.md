# Upstream sync audit — 2026-11-14

The fork's November 14 Devin/OpenCode adoption is reconciled with upstream `Fei2411/real-api-pricing` as of upstream commit `3d1be6c8bd62a74a3b50c10eeace124b7241a5a9`. The fork's pre-sync head was `c8f307e7097e7ab9b49653168f309128628ef60b`; their common ancestor was `d2df196fe37960e88037c512fb5508021ef7157c`. The Git histories diverged by 74 upstream commits and two fork commits.

## Preservation checks

- All upstream adopted rows outside OpenCode Go/Go Plus/Go Teams and Devin Pro × SWE-2 were compared field-for-field against upstream's `data/adopted.csv` and matched.
- OpenCode retains 29 models per tier across Go ($10), Go Plus ($40) and Go Teams ($20/member): 87 plan/model rows with `data_date=2026-11-14`. Three legacy 2026-10-30 single-model date overrides were removed so the official family-wide adoption date applies consistently.
- Devin Pro × SWE-2 retains the permanent Desktop/CLI no-incremental-token-charge benefit, `data_date=2026-11-12`, and an empty `promo_until`. This does **not** imply unlimited throughput, free Cloud sessions, or zero subscription price.
- The newer upstream Claude, Devin and ChatGPT sample decisions, benchmark methodology, and supporting research files are retained.

## Regeneration

The GitHub Actions reconciliation job re-ran `build_adopted.py`, `compute.py`, the i18n synchronization/check, README stats, static/interactive chart generation, publication checks, and website tests/build. It produced **404 plan × model points**, while preserving the upstream rows outside the targeted allowances.

This audit reflects the **November 14 adoption snapshot**, not a new claim that every vendor was reverified on that date. OpenAI's planned December shared quota remains a policy note; no post-change absolute token allowance is assumed.

The one-off sync workflow was removed from the final merge tree. PR #4 and its CI checks are the release gate.
