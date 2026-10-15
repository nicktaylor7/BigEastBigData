 # Big East Big Data

An unofficial fan site for Big East men's basketball stats. You can drill down from the whole conference to a single team and then to a single player. The leaderboards hold up because shooting percentages require a minimum number of attempts, and the advanced metrics are explained in plain language.

> **Status:** Prototype built on 2023–24 data. Weekly automatic updates are planned for the 2026–27 season.

---

## Features

### Conference → Team → Player drill-down
- **Conference:** conference-wide numbers, a "How the teams stack up" chart with 17 selectable metrics and the conference average marked, and a sortable table of every team. Tap any team to open it.
- **Team:** a team profile split into **Overall**, **Offense** and **Defense**, each metric ranked out of 11 and marked ▲/▼ against the conference average. There's also a "Where the points come from" breakdown and a sortable full roster. Tap any player to open him.
- **Player:** stat line, role on the team (usage rate, share of team points, points per 40, starts), conference rank in every category, a **Stretch run** split (through Feb 13 vs. the rest of the season), and full season totals.

Every page has breadcrumbs (`Big East › Creighton › Baylor Scheierman`) for moving back up a level.

### Leaders
Top 5 or Top 10 in 13 categories: points, rebounds, assists, steals, blocks, offensive rebounds, minutes, usage rate, assist/turnover, FG%, 3PT%, FT% and true shooting %. A **One per team** toggle limits each list to one player per school.

### Players
Every player on a Big East roster in one searchable table. Filter by team or minimum games, and sort by any column.

### Compare
Head-to-head comparison of any two players in every category, with the better number highlighted.

### Trends
The biggest risers and drops in points per game between two snapshots (mid-February and season's end). Weekly snapshots will turn this into a full season timeline.

---

## Data

### Sources
| Data | Source |
|---|---|
| Final season totals (players, team totals, opponent totals) | Official cumulative stats pages on each school's athletics website |
| Mid-season snapshot (Feb 13, 2024) | Hand-entered spreadsheet of each team's top rotation players |

The schools covered are Butler, Creighton, DePaul, Georgetown, Marquette, Providence, Seton Hall, St. John's, UConn, Villanova and Xavier.

All 11 school sites use the same stats page layout, so one parser handles every team. Each page includes games, starts, minutes, made and attempted shots for FG, 3PT and FT, offensive and defensive rebounds, assists, turnovers, steals, blocks and fouls for every player, plus **team and opponent totals**.

### Validation
Every import is checked before it goes on the site:

- **Points check:** each player's points must equal `2 × (FGM − 3PM) + 3 × 3PM + FTM`
- **Totals check:** player rows must add up to the team's official Total row (team rebounds and team turnovers aside)
- **Sanity checks:** made shots can't exceed attempts, and season totals can't go down between snapshots
- **Duplicate rows:** merged automatically (for example, a player listed twice after a jersey number change)
- **Name matching:** names are normalized across sources (handling "Last, First" vs. "First Last", Jr./II suffixes and accents), with a small alias list for known spelling differences

On the 2023–24 data, all 147 players passed the points check, and every team's player rows reconciled with its official totals. Comparing snapshots caught one impossible value in the hand-entered sheet: a player's February 3-point line was higher than his final season total.

---

## Metrics

### Team metrics
Possessions use the standard box-score estimate:

```
Possessions ≈ FGA − Offensive Rebounds + Turnovers + 0.475 × FTA
```

| Metric | Definition |
|---|---|
| **Net rating** | (Points scored − points allowed) per 100 possessions |
| **Tempo** | Average possessions per game (both teams) |
| **PPP** | Points per possession |
| **PPC** | Points per chance, like PPP but every offensive rebound starts a new chance: `PTS ÷ (FGA + TO + 0.475 × FTA)` |
| **eFG%** | `(FGM + 0.5 × 3PM) ÷ FGA` |
| **TOV%** | Turnovers per possession |
| **ORB% / DRB%** | Share of available offensive or defensive rebounds grabbed |
| **FTR** | Free-throw attempts per field-goal attempt |
| **3PAr** | Share of field-goal attempts taken from three |
| **Defensive versions** | The same metrics calculated from opponent totals (D-PPP, D-eFG%, D-TOV%, D-FTR) |

Together, eFG%, TOV%, ORB% and FTR on both ends make up Dean Oliver's **Four Factors**.

### Player metrics
| Metric | Definition |
|---|---|
| **TS%** | `PTS ÷ (2 × (FGA + 0.44 × FTA))` |
| **eFG%** | `(FGM + 0.5 × 3PM) ÷ FGA` |
| **Usage rate** | Share of team possessions a player uses while on the floor: `(FGA + 0.44 × FTA + TO) × (Team MIN ÷ 5) ÷ (MIN × (Team FGA + 0.44 × Team FTA + Team TO))` |
| **Points per 40** | `PTS ÷ MIN × 40` |
| **A/TO** | Assists ÷ turnovers |

### Qualifying rules
The minimums scale with the season, so the leaderboards work from opening week:

| Leaderboard | Requirement |
|---|---|
| All | Played in at least **75% of team games** (minimum 3) |
| FG% and TS% | 3+ field-goal attempts per team game (minimum 10 total) |
| 3PT% | 1.5+ three-point attempts per team game (minimum 6 total) |
| FT% | 1.5+ free-throw attempts per team game (minimum 6 total) |
| Assist/turnover | 2+ assists per team game |
| Usage rate | 10+ minutes per game |

An "Early season" notice appears automatically until teams have played 8 games.

---

## Tech

- **One self-contained HTML file:** HTML, CSS and vanilla JavaScript with no framework and no build step. The data is embedded as JSON.
- **Mobile-first:** responsive layout, scrollable tables with sticky first columns, and light and dark themes that follow the device setting.
- **Hash routing:** pages can be linked directly, e.g. `#conference`, `#leaders`, `#team-uconn`, `#player-cam-spencer`.
- **Fonts:** Big Shoulders Display and Libre Franklin from Google Fonts.

### Running locally
Open the HTML file in any modern browser. No server or install is needed.

---

## Roadmap

- [ ] **Weekly automatic updates** for 2026–27: pull all 11 school stats pages, run the validation checks, save a dated snapshot, and refresh the site
- [ ] **Week-by-week trends**: scoring race over time, hot and cold streaks
- [ ] **Game logs**: last-5-games form; home/away and conference/non-conference splits
- [ ] **Standings and schedule**: records, results and next-game cards on team pages
- [ ] **Player bios**: class, position, height, hometown, transfer history
- [ ] **Award races**: Player of the Year, Freshman of the Year, All-Big East tracker
- [ ] **Opponent-adjusted efficiency**
- [ ] **Shareable graphics**: weekly "Top 5" images for social media

---

## Disclaimer

This is an independent fan project. It is **not affiliated with, endorsed by, or connected to** the BIG EAST Conference, the NCAA, or any member school. Team names are used only to identify the teams. Statistics come from public official sources and are credited above.
