# Big East Big Data

An unofficial fan site for Big East men's basketball stats. You can drill down from the whole conference to a single team and then to a single player. It covers the 2026–27 season as it happens, plus eight complete seasons going back to 2018–19. The leaderboards hold up because shooting percentages require a minimum number of attempts, and the advanced metrics are explained in plain language.

Developed by Nicholas Taylor. Part of the [Since '79](https://since79.org/) family of sites.

**🏀 Live site: [nicktaylor7.github.io/BigEastBigData](https://nicktaylor7.github.io/BigEastBigData/)**

> **Status:** 2026–27 is live and updated during the season. Each team shows a "stats through" date, so readers can see exactly which games are included. Eight complete seasons (2018–19 through 2025–26) are also available.

---

## Features

### Conference → Team → Player drill-down
- **Conference:** conference-wide numbers, a "How the teams stack up" chart with 17 selectable metrics and the conference average marked, and a sortable table of every team, including win-loss record. Tap any team to open it.
- **Team:** the team's record (with Big East record once conference play starts) and its most recent result, then a team profile split into **Overall**, **Offense** and **Defense**. Each metric is ranked out of 11 and marked ▲/▼ against the conference average. There's also a "Where the points come from" breakdown, a sortable full roster and a program trend (net rating every season).
- **Player:** stat line, role on the team (usage rate, share of team points, points per 40, starts), conference rank in every category, full season totals and a Big East career table for players with more than one season.

Every page has breadcrumbs (`Big East › Creighton › Baylor Scheierman`) for moving back up a level.

### Teams
All 11 programs as cards, each showing the record, net rating, points scored and allowed, and the top three scorers. Sort A–Z or best to worst.

### Leaders
Top 5 or Top 10 in 13 categories: points, rebounds, assists, steals, blocks, offensive rebounds, minutes, usage rate, assist/turnover, FG%, 3PT%, FT% and true shooting %. A **One per team** toggle limits each list to one player per school.

### Players
Every player on a Big East roster in one searchable table. Filter by team or minimum games, and sort by any column.

### Compare Players and Compare Teams
Head-to-head comparisons of any two players or any two teams, **from any season**. For example, you can put this year's team against its own best season since 2018–19. The better number in each row is highlighted, and for stats where lower is better (points allowed, turnovers) the comparison accounts for that.

### Season switcher
A season menu in the header switches the whole site to any season from 2018–19 to 2026–27. The current season opens by default.

### History
- **Team trends:** any team metric charted across all eight complete seasons, with one team highlighted against the rest of the conference and the conference average
- **Season by season:** each year's best team and its scoring, rebounding and assists leaders
- **Record book:** the best single seasons since 2018–19 in points, rebounds, assists, blocks, 3PT% and TS%, plus the best teams, offenses and defenses

The season in progress joins History and the record book once it's complete, so early-season numbers don't crowd out full seasons.

### Other Sites
Links to the sister sites, [Big East Gami](https://nicktaylor7.github.io/BigEastGami/) and the [Big East Coaching Tree](https://since79.org/BigEastCoachingTree/), plus the sources the numbers come from. A "Return to Since '79" link sits at the top and bottom of every page.

---

## Data

### Sources
| Data | Source |
|---|---|
| Player stats, team totals and opponent totals, 2018–19 to 2026–27 | Official cumulative stats pages and season stats PDFs on each school's athletics website |
| 2026–27 records and latest results | The same season stats PDFs |
| Final records, 2018–19 to 2025–26 | Big East season standings, checked against each team's games played |

The schools covered are Butler, Creighton, DePaul, Georgetown, Marquette, Providence, Seton Hall, St. John's, UConn, Villanova and Xavier.

Each source lists games, starts, minutes, made and attempted shots for FG, 3PT and FT, offensive and defensive rebounds, assists, turnovers, steals, blocks and fouls for every player, plus **team and opponent totals**.

### Validation
Every import is checked before it goes on the site:

- **Points check:** each player's points must equal `2 × (FGM − 3PM) + 3 × 3PM + FTM`
- **Totals check:** player rows must add up to the team's official Total row (team rebounds and team turnovers aside)
- **Sanity checks:** made shots can't exceed attempts, and season totals can't go down between updates
- **Freshness check:** during the season, any file that looks older than expected is fetched again before it's treated as current
- **Records check:** for every team-season, wins plus losses must equal games played
- **Duplicate rows and name matching:** duplicate rows are merged, and names are matched across sources (handling "Last, First" vs. "First Last", Jr./II suffixes and accents)

Across the eight complete seasons (1,169 player-seasons), every player passed the points check, and every team's player rows reconciled with its official totals. All 86 past team-season records match games played. Two inconsistencies come from the schools' own pages, and the site shows the numbers as published: Seton Hall's 2018–19 opponent totals are off by 2 points, and Villanova's 2026–27 player free-throw attempts add up to one more than the team total. School archives only go back to 2018–19 for every team, which is why the history starts there.

---

## Metrics

### Team metrics
Possessions use the standard box-score estimate:

```
Possessions ≈ FGA − Offensive Rebounds + Turnovers + 0.475 × FTA
```

| Metric | Definition |
|---|---|
| **Net rating** | (Points scored − points allowed) per 100 possessions. Not adjusted for strength of schedule |
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
The minimums scale with the season:

| Leaderboard | Requirement |
|---|---|
| All | Played in at least **75% of team games** (minimum 3) |
| FG% and TS% | 3+ field-goal attempts per team game (minimum 10 total) |
| 3PT% | 1.5+ three-point attempts per team game (minimum 6 total) |
| FT% | 1.5+ free-throw attempts per team game (minimum 6 total) |
| Assist/turnover | 2+ assists per team game |
| Usage rate | 10+ minutes per game |

**Early-season rule (2026–27 only):** until a team has played 10 games, every player who has appeared counts, and the total-attempt minimums are off (the per-game rates still apply). The usual rules switch back on automatically, team by team, at 10 games. An "Early season" notice appears until then. Past seasons always use the standard rules.

---

## Tech

- **One self-contained HTML file:** HTML, CSS and vanilla JavaScript with no framework and no build step. The data is embedded as JSON.
- **Newspaper design:** Playfair Display, Source Serif 4, Oswald and Barlow Semi Condensed from Google Fonts, on a paper-toned page.
- **Mobile-first:** responsive layout, a compact tab grid on phones, and scrollable tables with sticky first columns.
- **Hash routing:** pages can be linked directly, e.g. `#conference`, `#leaders`, `#compare-teams`, `#team-uconn`, `#player-cam-spencer`.

### Hosting
Hosted free on **GitHub Pages** from the `main` branch. Uploading a new `index.html` (same name) replaces the old one, and the live site updates within a minute or two.

### Running locally
Open `index.html` in any modern browser. No server or install is needed.

---

## Roadmap

- [ ] **Daily automatic updates** for 2026–27: pull all 11 schools' season stats, run the validation checks, and refresh the site
- [ ] **Coaching data**: head coach by season, linked with the [Big East Coaching Tree](https://since79.org/BigEastCoachingTree/)
- [ ] **Week-by-week trends**: scoring race over time, hot and cold streaks
- [ ] **Game logs**: last-5-games form; home/away and conference/non-conference splits
- [ ] **Player bios**: class, position, height, hometown, transfer history
- [ ] **Award races**: Player of the Year, Freshman of the Year, All-Big East tracker
- [ ] **Opponent-adjusted efficiency**
- [ ] **History before 2018–19**

---

## Disclaimer

This is an independent fan project. It is **not affiliated with, endorsed by, or connected to** the BIG EAST Conference, the NCAA, or any member school. Team names are used only to identify the teams. Statistics come from public official sources and are credited above.
