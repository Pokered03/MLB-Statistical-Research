# MLB hosted validation — 2026-10-24

Live dashboard: https://mlb-statistical-research.streamlit.app/

Repository: https://github.com/Pokered03/MLB-Statistical-Research

Public visibility was approved by the user. This application, SQLite store, analysis engine and refresh workflow operate separately from NFL, NBA and the existing Multi-Sport Value Engine. Those applications were not changed.

## Source and software verification

- A fresh Git clone at 8d8b5a00142ae515ee120fddf0c71694c8574df7 matched all 49 prepared tracked files byte for byte. No missing or changed files.
- The independent clone passed **42 tests**, with 4 unrelated sport cases skipped (2.15 seconds). Later run-label and season-phase changes also passed all 42 in the isolated MLB project (2.16 seconds).
- Current-season official logs supplied both team boxes for **2,465 / 2,465 completed scheduled games**, across all **30 teams**. Both teams' runs scored and runs allowed must match the final; exact integer pitching outs and plausible observed count totals are required. Wrong opponents/seasons, conflicting duplicates and invalid records are rejected. Missing values stay missing.
- Collection uses five bounded team-game requests for current-year R/F/D/L/W competition, not per-game or per-player fan-out. Routine updates do not reload prior historical seasons. Historical Retrosheet attribution is prominent in the UI and included in source notices.
- Local 64-switch AppTest: cold render **0.547 seconds**, switching p95 **0.090 seconds**, peak app RSS **153.19 MiB**. Local cached worker: **4.52 seconds**, peak RSS **238.39 MiB**. Both resource targets passed. Local HTTP health/root checks passed.

## Initial live checks

- Independent Streamlit Community Cloud deployment: main/app.py, Python 3.12, stable PyArrow 24.0.0 pin.
- October 24 scheduled Tampa Bay–Milwaukee comparison rendered current offensive, defensive and situational statistics, with actual recent and venue batting/pitching splits.
- Official timestamped probable pitchers were visible in the context panel and explicitly marked **not confirmed**. Their season data are descriptive; no calibrated pitcher effect is applied to projections.
- Last 3/5/10 switching, manual Yankees–Mets search/comparison, neutral venue, historical 2025 season, and manual spread -1.5 / total 8.5 inputs worked. These input checks do not validate confidence against historical market lines.
- Calendar selection of October 25 correctly displayed an empty schedule and nearby dates; October 26 switched to the reverse scheduled matchup at Tropicana Field.
- A second browser session rendered independently while the first remained active. This is a basic two-session check, not a stress/load test.
- Sampled hosted process peak **171.2 MiB**. Exposed cgroup limit **3072 MiB**; sampled container usage **668.3–701.9 MiB**, including other processes and file cache. The app is below its 350 MiB development target in these initial checks. Long-term peaks remain unverified.
- First hosted refresh https://github.com/Pokered03/MLB-Statistical-Research/actions/runs/40117467451 **succeeded in 54 seconds**. The live app picked up the resulting **2026-10-24T17:44:49.306083+00:00** worker timestamp.

- Final correction refresh https://github.com/Pokered03/MLB-Statistical-Research/actions/runs/40117889349 **succeeded in 42 seconds**. The live app exposed its **2026-10-24T17:50:07.934485+00:00** update timestamp and corrected 292/3,698 early/later validation buckets.
- A controlled reboot of only this MLB deployment recovered successfully. The page reloaded current engine labels (Runs scored / game), matchup statistics and rolling controls; post-restart sampled process peak was **165.0 MiB** with container usage **699.3 MiB**. This verifies one ordinary restart, not extended crash or failure testing.

## Statistical validation and limits

The team-scoring baseline has 3,990 chronological held-out games: Brier about 0.246 versus a 0.25 constant-probability baseline; calibration error about 0.011; run-margin MAE about 3.529; total-runs MAE about 3.622. The latter is slightly worse than the report's simple total baseline (about 3.584); do not describe the total model as superior. These measurements do not establish profitable forecasts or comprehensive pitcher-aware accuracy.

The early-season reporting boundary was corrected: model eligibility requires 10 prior fitted games, so early uses 10–29 and later uses 30+ (minimum of the two teams). Local rerun produced **292 early** and **3,698 later** held-out cases, with Brier approximately 0.2452/0.2457 and run-margin MAE 3.551/3.527. The earlier below-10 bucket was necessarily empty. The same earlier calibration block is used for both phase reports; no calibrator is refitted on the held-out cases. Weekly fit counts may lag exact game-day counts.

Win probabilities are conditional research estimates with displayed limitations, not a model-reliability percentage. Spread/total confidence stays **PASS** without verified historical-line and confidence-category tests.

## Automatic updates

ENABLE_FREE_REFRESH=true is enabled. Daily cron **10:29 UTC** — 6:29 AM Eastern during daylight time and 5:29 AM during standard time, subject to GitHub scheduling delays. The workflow requires a public repository, uses a standard free ubuntu-latest runner, and creates no cache/artifact storage. No paid APIs, Odds API credits or paid hosting are configured. Public schedules may pause after inactivity. This is daily updating, not immediate end-of-game settlement.

## Outstanding work

Real iPhone and MacBook-specific verification, sustained multi-user load, extended crash/failure recovery and hosted stability checks remain. Requested bullpen-role/workload modeling, calibrated starting-pitcher effects, reliable injury/weather integrations, park factors, handedness matchup splits, wRC+, xFIP and Statcast are incomplete. Missing metrics remain N/A. Regular-season dagger cells and postseason-inclusive recent/venue windows have different documented scopes.

**Status: live development build with initial hosted checks; not full completion of this dashboard or the six-dashboard project.** NHL, College Football and College Basketball remain separate development builds awaiting their own publication/deployment checks.

## Maintenance note

With the bounded-memory server configuration, imported engine modules can remain cached through a code rerun. Reboot the individual deployment after changing imported engine code, then verify displayed labels and version behavior. Routine data-only refreshes use database-revision cache keys and were observed without requiring a reboot.
