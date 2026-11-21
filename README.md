# TravelSpecialist

A team of Claude Code subagents that plans multi-year travel:

| Year | Trip | Status |
|---|---|---|
| 2027 | Cabo San Lucas, Mexico (4 days / 3 nights) | Flights + hotel covered; needs daily expense plan |
| 2028 | 7-day cruise | Needs budget ranges, line/route selection |
| 2030 | Japan | Needs budget ranges, savings plan, full itinerary |

Trip details live in [`TRIPS.md`](TRIPS.md). Save finished plans in `plans/<year>-<trip>/`.

## The agent team (free: runs inside Claude Code)

No API key, no Anthropic Console account, no extra bill. The team runs inside Claude Code (app, web or terminal) and uses your existing Claude plan's usage.

- **Travel Director (lead):** the main Claude Code chat in this project. Its instructions are in [`CLAUDE.md`](CLAUDE.md). It hands tasks to the specialists and combines their answers.
- **12 specialists:** subagents in `.claude/agents/`.

| # | Agent | What it does |
|---|---|---|
| 1 | Travel Director (`CLAUDE.md`) | Lead planner: owns the multi-year roadmap and delegates to the others |
| 2 | `budget-specialist` | Budget ranges, savings plans, day-by-day spending |
| 3 | `flight-transportation-specialist` | Flights, fare timing, transfers, trains, getting to cruise ports |
| 4 | `lodging-specialist` | Hotels, resorts, rentals, cruise cabins |
| 5 | `cruise-specialist` | Cruise lines, routes, what's included vs. extra, port days |
| 6 | `itinerary-activities-planner` | Day-by-day plans, excursions, tours, restaurants |
| 7 | `documents-entry-specialist` | Passports, visas, entry rules, forms |
| 8 | `insurance-safety-advisor` | Travel insurance, health, safety, emergencies |
| 9 | `money-payments-specialist` | Currency, cards, ATMs, tipping |
| 10 | `rewards-deals-specialist` | Points, loyalty programs, sales timing |
| 11 | `culture-language-guide` | Etiquette, key phrases, customs |
| 12 | `packing-prep-coordinator` | Packing lists and prep checklists |
| 13 | `timeline-booking-coordinator` | Dated countdown checklists across all trips |

Agents research and recommend only; they never book or pay.

## How to use
1. Start a Claude Code session on this repository (claude.ai/code, the Claude app, or `claude` in a terminal).
2. Just ask, e.g. *"Build my Cabo day-by-day spending plan"* or *"Have the Cruise Specialist and Budget Specialist give me low / mid / high costs for a 2028 cruise."*
3. Type `/agents` to see the team.
