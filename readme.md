# Counter-Strike: Global Offensive Champions Match Tracker

A MongoDB-based data science project by Oliver You that tracks and analyses CS:GO championship matches using web scraping and aggregation pipelines.

---

## Project Overview

During the COVID-19 lockdown, Counter-Strike: Global Offensive (CS:GO) served as more than a game — it was a way to connect with friends. Years later in university, inspired by those shared experiences and a memorable esports tournament (PGL Major Antwerp 2022), this project explores CS:GO match data by sourcing, storing, and analysing statistics in a structured MongoDB environment.

---

## Dataset Description

- **Source**: Scraped from [bo3.gg](https://bo3.gg)
- **Matches Analysed**: 2022 PGL Major matches
- **Data Type**: Match metadata, teams, players, maps, stats, and simulated commentary

---

## Schema Design

The project uses six MongoDB collections:

### `matches`
- `match_id`, `title`, `tournament`, `date`
- `teams`: list of team IDs
- `score`, `map_ids`

### `teams`
- `team_id`, `team_name`
- `players`: list of player IDs
- `tournament`

### `players`
- `player_id`, `name`, `tournament`, `team_id`

### `maps`
- `map_id`, `name`, `times_played`

### `player_stats`
- `match_id`, `player_id`, `kills`, `deaths`, `assists`

### `commentary`
- `commentary_id`, `match_id`, `timestamp`, `text`, `tags`

All keys are uniquely generated using UUIDs for consistency and ease of reference.

---

## Data Ingestion

- Web scraper built using:
  - `BeautifulSoup4`, `requests`, `uuid`, `pymongo`
- Robust error-handling and duplicate prevention mechanisms
- HTML parsing logic refined over 30+ iterations

---

## Live Commentary Simulation

Since timestamped highlights were unavailable, a 2-minute mock simulation of live commentary was scripted. See the `.ipynb` notebook for execution instructions.

---

## Data Verification Functions

Implemented in Python with `pymongo`:

- `verify_single_team_per_player()`
- `verify_teams_in_matches()`
- `verify_player_stats_references()`
- `verify_maps_in_matches()`
- `verify_commentary_matches()`

These ensure referential integrity across the dataset.

---

## Aggregation Queries

1. **Full Match Summary**  
   Nested lookups and array queries to compile match data, participating teams, players, and commentary.

2. **Top KDA Players**  
   Identifies top players by computing KDA = (kills + assists) / deaths.

3. **Top Performer per Team/Match**  
   Lists the highest KDA scorer from each team in every match.

Additional explanation is available in the Jupyter Notebook.

---

## Project Files

- `match_tracker.ipynb`: Code for scraping, ingestion, and aggregation
- `README.md`: This file
- `data/`: (optional) Any manually backed up datasets

---

## References

- [bo3.gg: FaZe vs Natus Vincere (22 May 2022)](https://bo3.gg/matches/faze-vs-natus-vincere-22-05-2022)
- [bo3.gg: Spirit vs Furia (19 May 2022)](https://bo3.gg/matches/spirit-vs-furia-19-05-2022)
- [bo3.gg: ENCE vs Natus Vincere (21 May 2022)](https://bo3.gg/matches/ence-vs-natus-vincere-21-05-2022)
- [bo3.gg: FaZe vs Spirit (21 May 2022)](https://bo3.gg/matches/faze-vs-spirit-21-05-2022)
