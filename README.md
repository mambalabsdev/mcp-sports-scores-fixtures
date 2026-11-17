# Sports Scores and Fixtures MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-sports-scores-fixtures)](https://www.npmjs.com/package/@mambalabsdev/mcp-sports-scores-fixtures) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-sports-scores-fixtures)](https://github.com/mambalabsdev/mcp-sports-scores-fixtures/blob/main/LICENSE)

An MCP server for the Mamba Labs Sports Scores and Fixtures actor on Apify. Scores, live status, and fixtures by date across leagues.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give leagues and a date or date range. The actor reads ESPN's public scoreboard and returns one row per game with teams, status, score, period scores, winner, start time, and venue. Refused reads and summary rows are free.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-sports-scores-fixtures": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-sports-scores-fixtures"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_sports_scores_fixtures` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get last night's NBA and NHL results."
- "Show today's Premier League and Champions League games."
- "List every Celtics game in November 2026."

## Tool

`get_sports_scores_fixtures`. One tool. Example arguments:

```json
{
  "leagues": [
    "basketball/nba"
  ],
  "date_from": "2026-11-16",
  "max_games": 10
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `leagues` | array | no | ESPN league paths such as basketball/nba or soccer/eng.1, or names such as nfl, premier league, champions league, college football, ufc. Empty means NBA, NFL, NHL, MLB, and the Premier League. Tennis is not read here. |
| `date_from` | string | no | First schedule day as YYYY-MM-DD, or today, yesterday, or tomorrow. ESPN files games by US Eastern time. |
| `date_to` | string | no | Last schedule day. Empty means the same as date from. A run reads at most 62 days and 400 league days. |
| `statuses` | array | no | scheduled, live, final, postponed, canceled, suspended, delayed, other, or the shortcuts finished and upcoming. Empty means all. |
| `teams` | array | no | Keep games where a team or fighter name or abbreviation holds one of these words, such as celtics or BOS. |
| `max_games` | number | no | Stop after this many game rows. Default 500. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `game-row`, one game | $0.0018 | $0.00171 | $0.00162 | $0.00153 |
| `empty-read`, one league and day with no fitting game, after the first 2 free | $0.001 | $0.00095 | $0.0009 | $0.00085 |
| `apify-actor-start`, per run start | $0.002 | $0.002 | $0.002 | $0.002 |

Summary rows, refused reads, refused input, and the first 2 empty reads are free. Mamba Labs pays the platform costs of the run. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/sports-scores-fixtures](https://apify.com/mambalabs/sports-scores-fixtures)

## License

MIT. See [LICENSE](LICENSE).
