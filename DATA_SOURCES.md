# Sources, permissions and coverage

Primary integrated source: [Retrosheet (history); baseballr / SportsDataverse (current schedule)](https://www.retrosheet.org/gamelogs/index.html).

The information used here was obtained free of charge from and is copyrighted by Retrosheet. Interested parties may contact Retrosheet at www.retrosheet.org. Current MLB schedule is republished by SportsDataverse/baseballr-data; original MLB rights retained. Personal research deployment only pending redistribution review.

Other source-specific links:

- nflverse data and license: https://github.com/nflverse/nflverse-data
- hoopR NBA data: https://github.com/sportsdataverse/hoopR-nba-data
- hoopR D-I data: https://github.com/sportsdataverse/hoopR-mbb-data
- cfbfastR data publication: https://github.com/sportsdataverse/cfbfastR-cfb-data
- fastRhockey NHL data: https://github.com/sportsdataverse/fastRhockey-nhl-data
- baseballr schedule archive: https://github.com/sportsdataverse/baseballr-data
- Retrosheet permissions and downloads: https://www.retrosheet.org/downloads/csvdownloads.html
- Retrosheet game-log fields: https://www.retrosheet.org/gamelogs/glfields.txt

Only this sport’s adapter runs. No source requires an existing Odds API key. The data worker has an explicit host allowlist and rejects other API hosts. No direct ESPN scraping is enabled. No proprietary logo or premium statistical dataset is distributed. Preserve upstream notices and verify original league/dataset rights before public redistribution; an open-source wrapper license does not by itself license every underlying league asset. College football’s dataset-specific redistribution terms remain a public-release blocker.

## Snapshot coverage at build time

```json
[
  {
    "season": 2023,
    "teams_with_completed_games": 30,
    "registered_teams": 30,
    "schedule_games": 2430,
    "latest_final": "2023-10-01"
  },
  {
    "season": 2024,
    "teams_with_completed_games": 30,
    "registered_teams": 30,
    "schedule_games": 2429,
    "latest_final": "2024-09-30"
  },
  {
    "season": 2025,
    "teams_with_completed_games": 30,
    "registered_teams": 30,
    "schedule_games": 2430,
    "latest_final": "2025-09-28"
  },
  {
    "season": 2026,
    "teams_with_completed_games": 30,
    "registered_teams": 30,
    "schedule_games": 2472,
    "latest_final": "2026-10-19"
  }
]
```

These counts describe source observations, not independently certified official membership completeness. The current college-basketball preseason registry uses the latest available standings plus published conference membership; verify new-season changes when an official standings file becomes available. See the live coverage table for later updates.

## Expanded integrations and remaining gaps

Official current-season MLB regular-season hitting/pitching summaries now populate Season cells marked with † for all 30 teams, including AVG/OBP/SLG/OPS, ERA/WHIP, strikeout/walk rates and a computed team FIP. These summaries have a separate scope from rolling/postseason scoring; 2026 detailed game-box rolling splits remain unavailable. A bounded recent/upcoming official schedule refresh also records explicitly probable pitchers, their throwing hand and observed season statistics. Probable is not confirmed, and no starter forecast adjustment is assumed.

Official MLB season and probable-pitcher data use a few bounded personal-research summary requests; no game-log/player-history bulk API fetch is enabled. Original MLB terms apply. No paid feed, Odds API key or premium grades are used. See the runtime source/coverage metadata and each per-metric sample count. Injury, weather, future goalie confirmations and proprietary metrics remain incomplete.

## Current-year MLB team game logs

Official source: https://statsapi.mlb.com/api/v1/teams/stats?stats=gameLog&group=hitting,pitching&season=2026&sportIds=1&gameType=R&limit=10000 (plus F/D/L/W postseason types). Publisher MLB Advanced Media; original MLB rights/terms remain. The current-year worker makes at most five cached team-game log requests, not thousands of per-game requests. It joins only known final games with matching identities and reconciled runs, preserving exact pitching outs and missing fields. A response reaching its 10,000-row-per-group cap fails as potentially truncated. Historical years are not fetched on routine current-year updates.

Retrosheet reuse policy was verified at https://www.retrosheet.org/downloads/csvdownloads.html. Required attribution is displayed prominently in the app and retained in source documentation. Retrosheet data do not certify official MLB feed accuracy; both sources can publish corrections.
