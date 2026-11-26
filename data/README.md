# AcesAPI season pack

The last completed season of tennis as CSV, free to use under the [AcesAPI Sample Data Licence](../DATA-LICENSE.md). Use it in anything you build, credit AcesAPI, and don't republish the files themselves.

**Download:** the latest `acesapi-season-pack.zip` from this repository's [season-pack release](https://github.com/sports-data-hq/acesapi-mcp/releases/tag/season-pack). `preview/` holds the first 100 rows of a few files.

Seasons: 2025. Season naming: the calendar year. Competitions, by their API id: atp, wta. No odds, props or play-by-play: those, every earlier season and live data are on the API, free to start at https://acesapi.com/signup?utm_source=github&utm_medium=pack&utm_campaign=acesapi-pack.

## Files

| File | Rows |
|---|---|
| `acesapi-atp-2025-matches.csv` | 3,909 |
| `acesapi-atp-2025-players.csv` | 293 |
| `acesapi-atp-2025-rankings.csv` | 150 |
| `acesapi-atp-2025-tournaments.csv` | 61 |
| `acesapi-wta-2025-matches.csv` | 5,860 |
| `acesapi-wta-2025-players.csv` | 547 |
| `acesapi-wta-2025-rankings.csv` | 150 |
| `acesapi-wta-2025-tournaments.csv` | 105 |

## Columns

- **matches**: `league`, `season`, `tournament`, `surface`, `draw`, `round`, `date`, `player1`, `player2`, `seed1`, `seed2`, `winner`, `score`, `outcome`, `sets1`, `sets2`
- **players**: `league`, `season`, `player`, `country`, `matches`, `wins`, `losses`, `hard_wins`, `hard_losses`, `clay_wins`, `clay_losses`, `grass_wins`, `grass_losses`, `other_wins`, `other_losses`, `titles`, `finals_lost`, `elo_end_of_season`, `elo_hard`, `elo_clay`, `elo_grass`
- **rankings**: `league`, `season`, `as_of`, `rank`, `player`, `country`, `points`
- **tournaments**: `league`, `season`, `tournament_id`, `name`, `start_date`, `end_date`, `city`, `country`, `major`, `surface`, `indoor`, `champion`, `runner_up`, `final_score`

Credit line for anything you publish: **Data: AcesAPI (acesapi.com)**
