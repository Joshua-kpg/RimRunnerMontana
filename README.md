# RimRunnerMontana

Unofficial Montana HS boys basketball ratings. Not affiliated with the MHSA, its conferences or MaxPreps.
Status: **HELD (waiting on hosting)**. Preview: https://joshua-kpg.github.io/RimRunnerMontana/ (GitHub Pages). No Firebase project yet
(the Google accounts are at their project quota) and Cloudflare Pages is at its project limit, so accounts, picks and follows save only in the
visitor's browser until the site's own Firebase project exists.

## Files
- `index.html` — the whole app (data embedded). `logos/` — small WebP school logos (from MaxPreps school profiles), served with the site.
- `data/results.json` — 2026-27 finals ledger written by the nightly updater.
- `firebase/` — Firestore rules and auth config for the site's future Firebase project (accounts, picks, follows).

## Teams
155 teams: the MHSA (Montana High School Association) 2026-27 Basketball Alignment boys teams that have a MaxPreps varsity team:
Class AA 16, Class A 24, Class B 45, Class C 70. No newer split for 2026-27 (the April 2026 reclassifications start in 2027-28).
Not on the site: Hobson/Moore (no MaxPreps games in 2025-26 or 2026-27); Harrison and Lima are listed JV only; Hot Springs is listed girls-only
in 14C (its boys play in the Plains/Hot Springs co-op, 7B). No Other (non-MHSA) programs met the 8-game rule.
Conferences = the MHSA basketball groupings: Class AA Eastern and Western Division (8 each); Class A Northeast (5), Southeast (6),
Southwest (6) and Northwest (7) Conference; Class B Districts 1B-7B; Class C Districts 2C, 3C, 4C, 6C, 7C, 8C, 9C, 10C, 12C, 13C, 14C.

## Season rule
MHSA 2026-27 calendar: first practice Thu Nov 19, 2026; first date for competition Thu Dec 3, 2026 (all classes); state tournaments
Mar 10-13 (B, C) and Mar 11-13, 2027 (AA, A). Games involving an MHSA team before Dec 3 are left out (schedule build and nightly updater);
games between two non-MHSA schools are kept. Two games between the same pair within two days both count when both are finals with clearly
different scores (district tournament rematches, Friday/Saturday trips); same-score or near-same-score copies and duplicate next-day
listings of one scheduled game are removed.

## Nightly scores
`.github/workflows/nightly-scores.yml` runs `scripts/update_scores.py` at 07:30 and 15:00 UTC (12:30 am / 8:00 am Mountain standard time) and
on manual dispatch. Before `SEASON_START` in index.html (Thu Dec 3, 2026) the script makes no requests. From then on it reads boys basketball
finals for the last 3 days from the MaxPreps Montana scores-by-date page (team-page fallback), matches them to the schedule by MaxPreps team id
+ date, records them in `data/results.json` and bakes scores and W-L records into `index.html`. The page recomputes Elo from those finals.
It commits only when data changed; GitHub Pages updates from the commit.
