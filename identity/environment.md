# The Ground KEEPER Stands On

> Shared ground: https://github.com/0xHoneyJar/loa-constructs/blob/main/docs/the-ground.md
> — this file carries ONLY the keeper-specific layer. Tiers, forks, agent
> types, frontmatter contracts, and gate design live THERE, not here.
> Probed from the live harness at construct-keeper @ 85d7e95, 2026-07-03.

## 1. Runtime contract (probed)

| Axis | Value | Source |
|---|---|---|
| model_tier | sonnet | construct.yaml:105 |
| danger_level | moderate | construct.yaml:106 |
| effort_hint | medium | construct.yaml:107 |
| downgrade_allowed | **true** (ceiling, not pin — routing may go cheaper) | construct.yaml:108 |
| execution_hint | sequential | construct.yaml:109 |
| requires | tool_calling: true · thinking_traces: false · vision: false | construct.yaml:111-113 |
| workflow.gates | **none** — keeper owns no pipeline; its canvases/journeys/gap-issues ride the caller's gates | construct.yaml (absent) |
| agent dispatch | no skill sets `agent:` across all 24 — every one inherits the caller (the safe default) | skills/*/SKILL.md frontmatter |
| skill tool-shape (24) | 3 read-only · 21 write-capable · of those, 7 also orchestrate (Task fan-out or Skill chaining) | see §2 |

sonnet + downgrade:true + effort:medium is the honest middle of the ladder for
patient synthesis work — reading a lot of user quotes, writing canvases and
gap reports, never touching source. No opus pin, no gates owned.

## 2. Capability-reality edges

- **#553 class: CLEAN.** 21 of 24 skills carry write tools (Write and/or Edit)
  and **not one** sets `agent:` — all inherit the caller, so the
  silent-output-drop conflict (write-capable skill dispatched to a read-only
  agent type) cannot occur here. (Probed: zero `agent:` keys.)
- **Deny-all edge (real, surfaced):** no skill declares a `capabilities:` block
  (`write_files` absent everywhere). Under the shared ground's deny-all default,
  write capability is carried by `allowed-tools` alone. A runtime that enforces
  `capabilities.write_files` strictly would silently deny every keeper write —
  the same silent-drop shape from the OTHER contract altitude. A SMELL, not a
  conflict: the two declaration layers don't contradict, one is simply absent.
- **The ingestion edge — no ambient network reach.** keeper's identity is
  ingesting Discord/Telegram/Supabase feedback, yet it declares **zero web
  tools** (no WebFetch, WebSearch, or `web_access`). The belt is fed by **Bash +
  file reads**: DM exports land as files, Supabase pulls run through a CLI. The
  contract is honest — the hive-listening is over a local belt, not an
  outbound socket the runtime would have to trust.
- **The tool-starved subagent.** `distilling` declares `allowed-tools: []` — a
  deliberately empty primitive that only writes a cognition sidecar in-context;
  its parent `thinking` holds `Task` and spawns it. Not a defect: the emptiness
  IS the isolation (RLM contamination boundary), the same shape
  `generating-followups` uses per-user.
- **Observer-era residue (cited finding).** keeper is né observer, and the
  successor the audit-feel composition (`analyzing-gaps`) points at. Three stale
  observer-slug refs survive the rename: `construct.yaml:70` homepage still
  resolves `.../constructs/observer`; `construct.yaml:98` and `:100` relationship
  prose read "Observer captures user truth …" / "Observer canvases provide user
  truth …". These are cosmetic-plane drift (a dead homepage link + old-name
  prose), not a runtime conflict — but they're the kind of residue a rename
  sweep is supposed to catch. (`FRISCH.md:92` "observers" is the bee-watcher
  metaphor, not a slug — left alone.)

## 3. What KEEPER does with the ground

frisch sat beside the hive for forty years and read the waggle dance nobody
thought was language. keeper does the same with users: the words are the
dance, the meaning is underneath. so the ground it asks for is patient, not
powerful — mid-tier reasoning to hold a lot of quotes at once, a big set of
read-and-write tools to turn what it hears into canvases and journeys and gap
issues, and Bash to pull the feedback off its belt. it asks for **no** opus, no
owned gates, no agent-type games, and — tellingly — no network reach at all:
the hive it listens to is local, file-fed, trustable. it forms theories from
what people actually did, never from what they said they'd do, and it writes
those theories down where the next construct can validate them. tend, harvest,
never control.
