# Padel Tournament Formats

A comprehensive reference for every tournament format supported by PadelTour. Each section describes how pairs are formed, how rounds are structured, how scoring works, and how the winner is determined. This document is the authoritative spec for feature planning, data modeling, and UI design.

---

## Table of Contents

1. [Americano](#1-americano)
2. [Mexicano](#2-mexicano)
3. [Mixed Americano](#3-mixed-americano)
4. [Team Americano](#4-team-americano)
5. [Team Mexicano](#5-team-mexicano)
6. [Round Robin / League](#6-round-robin--league)
7. [Knockout / Single Elimination](#7-knockout--single-elimination)
8. [Double Elimination](#8-double-elimination)
9. [Swiss System](#9-swiss-system)
10. [King of the Court](#10-king-of-the-court)
11. [Pool Play + Knockout (Hybrid)](#11-pool-play--knockout-hybrid)
12. [Appendix: Official Match Score Formats (FFT)](#appendix-official-match-score-formats-fft)

---

## 1. Americano

### Overview
The most popular social padel format. Players rotate partners every round so that everyone plays with and against different people. Scoring is **individual** — your personal points accumulate regardless of who your partner is. Designed for mixed-skill groups where everyone gets equal court time.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 4 |
| Optimal players | 8–16 (even numbers work best) |
| Minimum courts | 1 |
| Recommended courts | 2+ (enables simultaneous matches) |

### Pair/Team Formation
- **Round 1**: Partners assigned randomly.
- **Subsequent rounds**: Partners rotate so each player is paired with a different person each round. The goal is for every player to partner with every other player at least once.

### Round Structure
- Each match is played to a fixed number of points: typically **16**, **24**, or **32** points.
- Each side serves a fixed number of times (usually 4) before serve passes to opponents.
- Matches last approximately **10–15 minutes** at 24 points.
- Number of rounds = (number of players − 1) to ensure full rotation, or fewer rounds for a shorter event.

### Scoring
- Every point won counts toward the **individual player's** running total — both players on the winning side get the winning score, both on the losing side get the losing score.
- Example: match ends **24–16** → each player on the winning pair gets **+24** pts; each on the losing pair gets **+16** pts.
- Points accumulate across all rounds.

### Winner Determination
- After all rounds, the player with the **highest cumulative point total** wins.
- Tiebreaker: if two players are level, a head-to-head comparison or a golden point play-off may be used.

### Typical Duration
| Players | Courts | Duration |
|---------|--------|----------|
| 8 | 2 | ~1.5–2 hrs |
| 12 | 3 | ~2 hrs |
| 16 | 4 | ~2–2.5 hrs |

### Variations
- **Mixed Americano** — see [Section 3](#3-mixed-americano).
- **Short Americano** — matches played to 16 pts for a quicker session.
- **Long Americano** — matches to 32 pts for a more competitive feel.

---

## 2. Mexicano

### Overview
Mexicano starts like Americano but adds **dynamic re-seeding** after every round. Players who are performing well are paired together, and players who are struggling are also paired together, creating increasingly fair and competitive matches as the tournament progresses.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 4 |
| Optimal players | 8–12 (even numbers) |
| Minimum courts | 1 |
| Recommended courts | 2–4 |

### Pair/Team Formation
- **Round 1**: Random pairing (same as Americano).
- **Subsequent rounds**: Live leaderboard is used to re-seed:
  - Players ranked **1 & 3** are paired → play against players ranked **2 & 4**.
  - Players ranked **5 & 7** are paired → play against players ranked **6 & 8**.
  - Pattern continues down the leaderboard.
- This means top performers play against each other and bottom performers play against each other.

### Round Structure
- Same match format as Americano (fixed point target, rotating serve).
- Typically **3–5 rounds** total.
- Re-seeding happens after **every** completed round.

### Scoring
- Same as Americano: **individual cumulative points**.
- Points from every match add to the personal running total.

### Winner Determination
- Player with the **highest cumulative point total** after all rounds wins.

### Typical Duration
~2 hours for 8–12 players.

### Variations
- **Team Mexicano** — see [Section 5](#5-team-mexicano).
- Can be combined with a knockout final between the top 4 players.

---

## 3. Mixed Americano

### Overview
A variant of standard Americano with the added constraint that every pair **must be one male and one female player**. Popular for social club nights and mixed-gender events.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 4 (2M + 2F) |
| Optimal players | 8–16 (equal M/F split preferred) |
| Minimum courts | 1 |

### Pair/Team Formation
- **Round 1**: Random male–female pairing.
- **Subsequent rounds**: Rotation ensures each male plays with a different female partner each round.
- With unequal M/F counts, some players may repeat partners — the app should flag this.

### Round Structure
Same as standard Americano.

### Scoring
Same as standard Americano — individual cumulative points.

### Winner Determination
- Overall winner: player (M or F) with the highest total points.
- Optional: separate male and female rankings.

### Typical Duration
Same as standard Americano.

---

## 4. Team Americano

### Overview
Players form **fixed pairs** at the start and remain together for the entire tournament. Scoring is **team-based** — both members of a pair share the same score. The format is like Americano but with stable partnerships and team standings instead of individual standings.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 8 (4 teams of 2) |
| Must be divisible by | 4 |
| Optimal players | 8–16 |
| Minimum courts | 1 |
| Recommended courts | 2+ |

### Pair/Team Formation
- Teams of 2 are formed **before** the tournament starts (manually assigned or randomly drawn).
- Teams do **not** rotate partners — the pair is fixed.
- Scheduling: each team plays every other team (round-robin style) or a set number of matches.

### Round Structure
- Each match is played to a fixed point target (16, 20, 24, or 32 points).
- Each team serves 4 times before serve rotates.
- Multiple rounds to maximise matches between all team pairings.

### Scoring
- **Both players** on the winning team receive the winning match score; both on the losing team receive the losing score.
- Example: match ends **18–14** → Team A gets **+18** pts each; Team B gets **+14** pts each.
- Cumulative team score = sum of both rounds.

### Winner Determination
- Team with the **highest combined cumulative score** wins.

### Typical Duration
2–3 hours for 4–8 teams.

### Variations
- Can add a knockout final between the top 2 or 4 teams.

---

## 5. Team Mexicano

### Overview
Combines the **fixed-team** concept of Team Americano with the **dynamic re-seeding** of Mexicano. Fixed pairs are re-matched each round based on the live team leaderboard, so top teams face top teams and bottom teams face bottom teams as the tournament progresses.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 8 (4 teams of 2) |
| Must be divisible by | 4 |
| Optimal players | 8–16 |
| Minimum courts | 1 |

### Pair/Team Formation
- Teams of 2 are fixed before the tournament.
- **Round 1**: Random match-ups between teams.
- **Subsequent rounds**: Teams re-matched by leaderboard position (same Mexicano logic applied at team level):
  - Teams ranked **1 & 3** → play against teams ranked **2 & 4**.
  - Teams ranked **5 & 7** → play against teams ranked **6 & 8**.

### Round Structure
Same as Team Americano.

### Scoring
Same as Team Americano — team cumulative points.

### Winner Determination
Team with the **highest cumulative score** wins.

### Typical Duration
2–3 hours.

---

## 6. Round Robin / League

### Overview
Every team (or player pair) plays against every other team exactly once. Results are tracked as wins/losses/draws with league points awarded. Ideal for club leagues or long-form events where ensuring every team faces every other team matters more than speed.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 6 (3 teams) |
| No upper limit | (scales with scheduling) |
| Minimum courts | 1 |
| Recommended courts | = ⌊ teams / 2 ⌋ for simultaneous play |

### Pair/Team Formation
- Fixed teams or player pairs established before the tournament.
- The schedule is generated so each team plays every other team once (full round robin) or twice (double round robin).

### Round Structure
- Each match uses **standard padel scoring** (sets and games) or a fixed-point format — configurable by the organiser.
- Schedule generated using a round-robin algorithm (e.g., circle method).
- Total matches = n × (n − 1) / 2 for n teams.

### Scoring
- **League points**: typically 3 pts for a win, 1 pt for a draw, 0 pts for a loss (configurable).
- Tiebreakers: head-to-head result → game difference → games won.

### Winner Determination
- Team with the **most league points** at the end of all matches wins.

### Typical Duration
Highly variable: a 4-team round robin in an afternoon (~3 hrs); a 10-team league across multiple weekends.

### Variations
- **Double Round Robin**: each pair of teams plays twice (home & away).
- Often used as a **group stage** feeding into a knockout phase (see [Section 11](#11-pool-play--knockout-hybrid)).

---

## 7. Knockout / Single Elimination

### Overview
A bracket-based tournament where **one loss = elimination**. High stakes, exciting format used in championships and competitive events. The field is halved after each round until only one winner remains.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum teams | 4 |
| Ideal team count | Power of 2 (4, 8, 16, 32) |
| Non-power-of-2 | Handled with byes in round 1 |
| Minimum courts | 1 |
| Recommended courts | Multiple for simultaneous matches |

### Pair/Team Formation
- Fixed teams drawn into a bracket before the tournament.
- Seeding can be random or based on ranking.
- Bracket is fixed after the draw — winners advance, losers are eliminated.

### Round Structure
- Each match uses standard padel scoring.
- Rounds: Round of 16 → Quarterfinals → Semifinals → Final.
- Optional: third-place play-off match.

### Scoring
- Win/loss only — no cumulative point tracking.
- Winning a match = advance to the next round.

### Winner Determination
- The team that wins the **Final** is the tournament champion.

### Typical Duration
| Teams | Courts | Duration |
|-------|--------|----------|
| 8 | 2 | ~3–4 hrs |
| 16 | 4 | ~4–5 hrs |

### Variations
- **Seeded bracket**: top-ranked teams are placed to avoid meeting until late rounds.
- **Random draw**: no seeding, fully random placement.

---

## 8. Double Elimination

### Overview
Like single elimination, but a team must **lose twice** before being eliminated. After the first loss, a team drops into a "losers' bracket" and can still fight back to win the tournament. More forgiving and more total matches than single elimination.

### Player & Court Requirements
Same as single elimination. Works best with 4, 8, or 16 teams.

### Pair/Team Formation
- Fixed teams drawn into a **winners' bracket**.
- After first loss → dropped into **losers' bracket**.
- Losers' bracket winner plays winners' bracket winner in the grand final.
  - If winners' bracket team wins: they are champion.
  - If losers' bracket team wins: a decisive final is played (since neither team has two losses yet).

### Round Structure
- Standard padel match scoring.
- More rounds than single elimination (roughly 2× the matches).

### Scoring
Win/loss only within each bracket match.

### Winner Determination
- Team that wins the **grand final** (or decisive final) with fewer than 2 losses is champion.

### Typical Duration
~1.5–2× longer than single elimination for the same field size.

---

## 9. Swiss System

### Overview
A non-eliminating format where everyone plays a fixed number of rounds and is **always paired against an opponent with a similar record**. No one is knocked out. Popular when organisers want fair, competitive matches throughout without the elimination stakes of a bracket.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum teams | 4 |
| Optimal teams | 8–32 |
| Minimum courts | 1 |
| Rounds | Typically ⌈log₂(n)⌉ for n teams |

### Pair/Team Formation
- **Round 1**: Random pairing.
- **Subsequent rounds**: Teams paired against opponents with the **same or closest win-loss record** who they have not yet played.
- No team is ever eliminated — everyone plays every round.

### Round Structure
- Standard padel match scoring per round.
- Fixed number of rounds (usually 4–6 for 8–32 teams).
- After all rounds, final standings are ranked.

### Scoring
- **Points**: win = 1, draw = 0.5, loss = 0.
- Tiebreakers: opponent win percentage (Buchholz score), head-to-head, game difference.

### Winner Determination
- Team with the **highest accumulated Swiss points** wins.
- Often the top 2–4 teams proceed to a knockout final.

### Typical Duration
3–4 hours for a typical 8-team Swiss with 4 rounds.

---

## 10. King of the Court

### Overview
A fast-paced, social format. One court is designated the **"King court"**. The team on it defends their position — if they win, they stay; if they lose, they move off and the next team moves up. Great for social events with many players and limited courts.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum players | 6 |
| Minimum courts | 2 (1 king court + 1 challenger court) |
| Works well with | 8–20 players on 2–4 courts |

### Pair/Team Formation
- Teams can be fixed pairs or rotating partners (configurable).
- A queue of teams waits to challenge the king.
- Losing team from the king court joins the back of the queue.

### Round Structure
- Short matches: typically **7–11 points** or a time limit (e.g., 8 minutes).
- When a match finishes on the king court:
  - **Winning team stays** on the king court.
  - **Losing team** moves to the lowest challenger court (or to the queue if courts are full).
  - Teams on other courts each move up one court.
  - Next team from the queue enters the lowest court.

### Scoring
- Each **point won** on the king court counts toward your personal or team score.
- Points on challenger courts may also count (configurable).
- The team/player with the most king-court points wins.

### Winner Determination
- Player or team with the **most accumulated points** (or most time spent as "king") wins.

### Typical Duration
~1–1.5 hours as a standalone event; often used as a warm-up or social wind-down.

---

## 11. Pool Play + Knockout (Hybrid)

### Overview
A two-stage format: teams are divided into **pools** (groups) that play a mini round-robin, then the **top teams from each pool** advance to a knockout bracket. Balances the guarantee of multiple matches for everyone with the excitement of elimination finals. Used in most major padel tournaments worldwide.

### Player & Court Requirements
| Parameter | Value |
|-----------|-------|
| Minimum teams | 8 (e.g., 2 pools of 4) |
| Common structures | 4 pools of 4, 3 pools of 4, 2 pools of 4 |
| Minimum courts | 2+ |

### Pair/Team Formation
**Stage 1 — Pool Play:**
- Teams drawn into pools (seeded or random).
- Within each pool: full round robin (every team plays every other team in the pool).

**Stage 2 — Knockout:**
- Top 1 or 2 teams from each pool advance.
- Standard single-elimination bracket seeded by pool performance.

### Round Structure
- Pool matches: standard padel scoring (sets or fixed points).
- Knockout matches: standard padel scoring (best of 3 sets or similar).

### Scoring
- Pool stage: league points (3 win / 1 draw / 0 loss) + game difference for tiebreaking.
- Knockout stage: win/loss only.

### Winner Determination
- Team that wins the **knockout Final** is champion.

### Typical Duration
Full day event (4–8 hours) for 8–16 teams.

### Variations
- **Repechage**: some eliminated teams from pool play enter a consolation bracket.
- **Double pools**: two rounds of pool play before knockout begins.

---

## Appendix: Official Match Score Formats (FFT)

Used in FFT (Fédération Française de Tennis)-sanctioned padel competitions. Relevant when the app needs to support official match score entry.

| Format | Description | Use Case |
|--------|-------------|----------|
| **A1** | 3 sets to 6 games; tiebreak at 6–6 in each set | Standard competition |
| **A2** | Same as A1 but with a decisive point at deuce | Faster standard matches |
| **B1** | 2 sets of 6 games with tiebreak at 6–6; 3rd set replaced by a 10-point super tiebreak | Semi-finals, time-limited events |
| **E** | 1 super tiebreak to 10 points | Classification matches, rain-shortened matches |
| **F** | 1 set of 4 games with a decisive point/game | Ultra-short format, warm-ups, tie deciders |

---

## Quick Comparison

| Format | Partnership | Scoring Type | Skill Matching | Best For | Est. Duration |
|--------|-------------|-------------|---------------|----------|---------------|
| Americano | Rotating | Individual pts | Static | Social, mixed levels | ~2 hrs |
| Mexicano | Rotating | Individual pts | Dynamic | Competitive, fair | ~2 hrs |
| Mixed Americano | Rotating (M+F) | Individual pts | Static | Mixed-gender social | ~2 hrs |
| Team Americano | Fixed | Team pts | Static | Established pairs | 2–3 hrs |
| Team Mexicano | Fixed | Team pts | Dynamic | Strategy + fairness | 2–3 hrs |
| Round Robin | Fixed | League pts | None | Club leagues | Variable |
| Knockout | Fixed | Win/loss | Bracket | Championships | 3–5 hrs |
| Double Elimination | Fixed | Win/loss | Bracket | Fairer knockout | 4–6 hrs |
| Swiss System | Fixed | Swiss pts | Dynamic | Fair, no elimination | 3–4 hrs |
| King of Court | Fixed/Rotating | Pts on king court | None | Social, many players | 1–2 hrs |
| Pool + Knockout | Fixed | League → Win/loss | Bracket | Major tournaments | Full day |
