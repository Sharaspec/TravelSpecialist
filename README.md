# TravelSpecialist

A team of Claude Code subagents that plans multi-year travel:

| Year | Trip | Status |
|---|---|---|
| 2027 | Cabo San Lucas, Mexico (4 days / 3 nights) | Flights + hotel covered; needs daily expense plan |
| 2028 | 7-day cruise | Needs budget ranges, line/route selection |
| 2030 | Japan | Needs budget ranges, savings plan, full itinerary |

Trip details live in [`TRIPS.md`](TRIPS.md). Save finished plans in `plans/<year>-<trip>/`.

## The agent team (Claude Managed Agents)

Each agent is a file in `agents/<name>/agent.md` (settings at the top, instructions below), synced to your Anthropic account with the `ant` CLI. The **Travel Director** is the lead: it has the other 12 as its team and hands them work. All agents are tagged `project: travel-specialist`.

| # | Agent | What it does |
|---|---|---|
| 1 | `travel-director` | Lead planner: owns the multi-year roadmap and delegates to the others |
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

The shared environment (`environments/travel.yaml`) has open internet access so agents can search airline, cruise, hotel and government sites. Agents research and recommend only; they never book or pay.

## Setup

1. Install the `ant` CLI (version 1.40.0 or later) and sign in:

```bash
ant auth login
```

2. Preview what will be created:

```bash
ant apply --dry-run agents environments
```

3. Create all 13 agents and the environment (writes `claude-lock.json` with their IDs; commit it):

```bash
ant apply agents environments
```

4. Start a session in the Claude Console with the **Travel Director** agent and the `travel-specialist-env` environment, then ask, e.g. *"Build my Cabo day-by-day spending plan"* or *"Give me low / mid / high budgets for a 7-day cruise in 2028."*

To change an agent, edit its file and run `ant apply agents environments` again; that makes a new version.

## Costs
Managed Agents is a beta Anthropic product billed per token plus session run time. The Travel Director can start **workflow runs** (several specialists in parallel) for big requests like "plan all three trips", which uses more tokens. To turn that off, set `workflows: {type: disabled}` in `agents/travel-director/agent.md`. Setting a spending limit on each session is a good idea.
