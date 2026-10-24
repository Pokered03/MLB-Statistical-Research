# MLB publication checkpoint — 2026-10-24

Public repository created with user approval: https://github.com/Pokered03/MLB-Statistical-Research

This is an independent development build, not full project completion. No other sports application was modified. Deployment is pending.

- **42 tests passed**, 4 unrelated sport tests skipped (2.02 seconds).
- Current-year team-game logs fill detailed batting and team-pitching metrics for all **2465/2465** completed scheduled games, across all 30 teams. Both batting and pitching runs reconcile to the final before either box is accepted. Unknown identities, conflicting duplicates, impossible observed counts and invalid outs are rejected; absent fields are never fabricated as zero.
- Current-year collection uses five bounded official team-game log endpoints rather than per-game fan-out. Regular-season totals remain a separate marked scope. Historical Retrosheet data retain the required attribution.
- Local AppTest: cold render 0.547 seconds; switching p95 0.090 seconds over 64 switches; peak app RSS 153.19 MiB. Local worker refresh: 4.52 seconds from cache, peak RSS 238.39 MiB. HTTP health/root checks passed. Actual host and mobile checks remain outstanding.
- The separate free refresh workflow is prepared but still inactive until enabled on this public repository.

Unsupported bullpen-role modeling, verified injuries/weather, ballpark factors, wRC+, xFIP, Statcast and calibrated starting-pitcher matchup adjustments remain incomplete. Future probable pitcher reports are timestamped and not confirmation. Spread/total confidence remains PASS without validated historical-line/category support.
