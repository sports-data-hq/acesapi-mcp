# AcesAPI MCP server

[![AcesAPI MCP connector](https://glama.ai/mcp/connectors/io.github.noahowsh/acesapi/badges/score.svg)](https://glama.ai/mcp/connectors/io.github.noahowsh/acesapi)

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-listed-0b7285?style=flat-square)](https://registry.modelcontextprotocol.io/v0/servers?search=io.github.noahowsh/acesapi)

**The tennis data API.** ATP and WTA singles matches with every set and tiebreak score, tournament draws round by round, player profiles, weekly rankings, head to head, surface splits, our own Elo by surface, and sportsbook moneylines on Grand Slam and Masters / WTA 1000 matches. REST API and MCP server. 500 free credits every month, no card.

Website: https://acesapi.com?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp · Docs: https://acesapi.com/docs?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp · Get a key: https://acesapi.com/signup?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp

```
You:    "What is Carlos Alcaraz's record on clay against top-10 players?"
Claude: [calls get_surface_splits]

You:    "Who leads the Sinner and Alcaraz head to head, and how many of their meetings were finals?"
Claude: [calls get_head_to_head]

You:    "Which moneylines were posted for the 2025 US Open men's final?"
Claude: [calls get_matches, then get_match]
```


## Run it locally (stdio)

Most clients connect to `https://mcp.acesapi.com/mcp` directly. For a client that launches a local process instead:

```bash
git clone https://github.com/sports-data-hq/acesapi-mcp.git && cd acesapi-mcp && npm install
ACESAPI_API_KEY=your_key node index.js
```

```json
{ "mcpServers": { "acesapi": { "command": "node", "args": ["/path/to/acesapi-mcp/index.js"], "env": { "ACESAPI_API_KEY": "your_key" } } } }
```

It forwards to the hosted server with your key, so every tool and credit cost is the same.

## Try it now, no key

- **A free season of tennis data:** the last completed season as CSV (games, standings, player season totals and our ratings). [Download the zip](https://github.com/sports-data-hq/acesapi-mcp/releases/download/season-pack/acesapi-season-pack.zip) or browse [what's in it](data/README.md).
- **Open it in Colab:** [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sports-data-hq/acesapi-mcp/blob/main/notebooks/acesapi-season-pack.ipynb) loads the pack and answers three questions in a minute.
- **Ask Claude without a key:** install the skills below; `season-pack-offline` answers from the pack until you connect.

**With a free key it does far more:** every earlier season, today's games, play-by-play, lineups, odds and player props with their history and movement, and every skill below running on live data. [Get a free key](https://acesapi.com/signup?utm_source=github&utm_medium=readme&utm_campaign=acesapi-try-now): 500 credits a month, no card.

## Skills

4 Claude skills for tennis ship in this repo, plus 13 analytics skills for models, backtests, calibration and comparing a model with the market. Every number in an answer comes from a live AcesAPI tool call, and odds are information only: no stakes, no picks.

Claude Code:

```
/plugin marketplace add sports-data-hq/acesapi-mcp
/plugin install tennis-data@acesapi
/plugin install sports-analytics-core@acesapi
```

Codex: `codex plugin marketplace add sports-data-hq/acesapi-mcp`. Any agent that reads skills: `npx skills add sports-data-hq/acesapi-mcp`.

| Skill | What it does |
|---|---|
| `tennis-head-to-head` | Two players' history: results by surface and round, sets and tiebreaks |
| `tennis-match-preview` | One-page preview: form, surface records, Elo by surface, head to head and the market |
| `tennis-surface-form` | Record, sets, tiebreaks and Elo by surface and season |
| `tennis-tournament-simulation` | Title chances for a tournament from the draw and surface Elo |

The analytics skills: `backtesting`, `data-pipeline`, `elo-engineering`, `feature-engineering`, `market-vs-model`, `model-building`, `odds-market-analysis`, `prediction-tracker`, `probability-calibration`, `season-pack-offline`, `sports-data-preflight`, `visualization`, `walk-forward-validation`.

Real answers on live data, with the credits each used: [example answers](https://github.com/sports-data-hq/sportsdatahq-skills/tree/main/docs/examples/tennis).

All nine sports' skills live in [sports-data-hq/sportsdatahq-skills](https://github.com/sports-data-hq/sportsdatahq-skills). The copies here are synced from there, so please open issues and pull requests there.

## Useful pages

- [Docs](https://acesapi.com/docs?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): every endpoint with parameters and live examples
- [Tennis odds](https://acesapi.com/odds?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): upcoming ATP and WTA matches with each sportsbook's moneyline
- [Data atlas](https://acesapi.com/docs/atlas?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): what exists and where coverage is partial
- [Guides](https://acesapi.com/guides?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): Python walkthroughs for surface Elo, head to head, rankings, set scores and surface splits
- [Data](https://acesapi.com/data?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): [results](https://acesapi.com/data/tennis-results-api?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp), [rankings history](https://acesapi.com/data/tennis-rankings-history?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp), [odds history](https://acesapi.com/data/tennis-odds-history?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp)
- [Pricing](https://acesapi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp): credits per call, 500 free every month
- [Surface Elo explained](https://acesapi.com/glossary/surface-elo?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp)

## Python

The official Python client is on PyPI: [acesapi](https://pypi.org/project/acesapi/).

```bash
pip install acesapi
export ACESAPI_API_KEY=sk_live_...
```

```python
from acesapi import Client

client = Client()

ranks = client.get_rankings(limit=5)
for row in ranks["rankings"]:
    print(row["rank"], row["name"], row["points"])
```

Typed errors for a bad key, no credits left, not found and rate limits, automatic retries, and `to_dataframe` for pandas.

## Quick start

This is a hosted (remote) MCP server over Streamable HTTP. There is nothing to install.

**Claude Code**

```bash
claude mcp add --transport http acesapi "https://mcp.acesapi.com/mcp?key=YOUR_API_KEY"
```

**Claude Desktop, Cursor and other clients**

```json
{
  "mcpServers": {
    "acesapi": {
      "url": "https://mcp.acesapi.com/mcp?key=YOUR_API_KEY"
    }
  }
}
```

The key can also be sent as an `x-api-key` header or `Authorization: Bearer`. Connecting and listing tools works without a key; calling a tool needs one.

**REST**

```bash
curl -X POST https://mcp.acesapi.com/v1/list_tournaments -H "x-api-key: YOUR_API_KEY"
```

Every tool is `POST /v1/{tool}` with a JSON body.

## Examples

Runnable Python (standard library only) and Node 18+ (no dependencies) examples live in [`examples/`](examples/):

- [`examples/python/quickstart.py`](examples/python/quickstart.py) and [`examples/node/quickstart.mjs`](examples/node/quickstart.mjs): schedule plus a headline call.
- [`examples/python/tennis_head_to_head_surface_elo.py`](examples/python/tennis_head_to_head_surface_elo.py): Two players side by side.

```bash
export ACESAPI_API_KEY=your_key
python3 examples/python/quickstart.py
node examples/node/quickstart.mjs
```

See [`examples/README.md`](examples/README.md) for details. Get a free key (500 credits a month, no card) at https://acesapi.com/signup?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp.

## Use it in

- **Claude, ChatGPT, Cursor, VS Code, Gemini CLI, Grok, Perplexity, Le Chat:** add `https://mcp.acesapi.com/mcp` as a remote MCP server. Step-by-step for each: https://acesapi.com/mcp?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp
- **Gemini CLI:** `gemini extensions install https://github.com/sports-data-hq/acesapi-mcp`
- **Cursor:** the [SportsDataHQ plugins for Cursor](https://github.com/sports-data-hq/sportsdatahq-cursor-plugins)
- **Google Sheets:** `=SDHQ("acesapi","list_tournaments")` fills a live table: https://sportsdatahq.com/sheets?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp
- **REST:** `POST https://mcp.acesapi.com/v1/<tool>` with an `x-api-key` header: https://acesapi.com/docs?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp

## Tools (14)

| Tool | What it returns |
|------|-----------------|
| `list_tournaments` | A season's tournaments with dates, surface, status and champion |
| `search_players` | Find players by name or country |
| `get_tournament` | A tournament's draw and results, round by round, with every set |
| `get_matches` | Match results by day, tournament or season, with set and tiebreak scores |
| `get_schedule` | Upcoming and in-progress matches for the next days |
| `get_odds` | Each sportsbook's opening and closing moneylines for a match or a whole tournament, with the games handicap and total |
| `get_match` | One match: sets, tiebreak points, seeds, ratings, what the score says and its sportsbook lines |
| `get_rankings` | Weekly ranking lists since 2007, or one player's ranking history |
| `get_ratings` | Our Elo ratings, overall or by surface |
| `get_head_to_head` | Two players' meetings, wins by surface and in finals |
| `get_surface_splits` | A player's record by surface: sets, games, tiebreaks, deciding sets |
| `get_player_stats` | A player's season statistics from scores, by round and opponent rank |
| `get_player` | Profile, ranking, ratings, career record, titles and recent matches |
| `get_player_matches` | A player's matches with scores and ratings, filtered by season, surface or opponent |

Leagues: tennis (default, ATP), wta (pass `league: "wta"` to any tool).

## Data

- ATP and WTA singles since 2007 (qualifying from 2022) with set and tiebreak scores
- Tournament draws and results round by round; weekly rankings since 2007
- Head to head, surface splits, player season statistics derived from scores, our Elo overall and by surface
- Sportsbook moneylines, returned in the `odds` array of `get_match` (there is no separate odds tool): Grand Slam matches from mid-2020 and ATP Masters and WTA 1000 matches from August 2024, pre-match, refreshed hourly; the array is empty for other tournaments
- No serve statistics (aces, double faults, break points)

Coverage by season, read live from the database: https://acesapi.com/docs?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp

## Pricing

500 free credits every month, no card. Plans: Starter $19/mo (10,000 credits), Pro $49/mo (30,000), Scale $149/mo (125,000), Business $299/mo (300,000). Wallet top-ups from $5, never expire. https://acesapi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp

## Attribution

Surfaces and ratings are ours. Not affiliated with the ATP, WTA, ITF or any tournament.

## License

MIT for the contents of this repository. Data terms as above.

## Use with Codex

The SportsDataHQ skills marketplace also works in Codex (it reads `.agents/plugins/marketplace.json`):

```bash
codex plugin marketplace add sports-data-hq/sportsdatahq-skills
```

Install `tennis-data`, which bundles the tennis skills and the AcesAPI MCP server.

## Use with Gemini CLI

```bash
export ACESAPI_API_KEY=your_key
gemini extensions install https://github.com/sports-data-hq/acesapi-mcp
```

The extension adds the AcesAPI MCP server (https://mcp.acesapi.com/mcp) and sends the key in the `x-api-key` header. Get a free key (500 credits a month) at https://acesapi.com/signup?utm_source=github&utm_medium=readme&utm_campaign=acesapi-mcp.
