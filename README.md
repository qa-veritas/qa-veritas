## AI-Native Infrastructure Quality Engineering

I build agents that operate on infrastructure safely — clusters, nodes,
workloads, storage, networks — and the engineering substrate that makes
them trustworthy: deterministic evidence before model reasoning,
read-before-write safety loops, capacity-aware feasibility, observable
verification, and operational memory that lives in a git tree.

The throughline across everything here: an agent is only as good as the
facts you hand it and the checks you hold it to. So I parse the hard
facts deterministically, let the model reason, and confirm the result
with a signal I can point at in a code review.

### What I'm building

| Repo | The idea it proves |
|------|--------------------|
| [resource-ledger](https://github.com/qa-veritas/resource-ledger) | Operate infrastructure from a git tree (inventory + contract + runbook + journal) with a feasibility CLI that refuses changes that don't fit recorded capacity. |
| [state-triage](https://github.com/qa-veritas/state-triage) | A deterministic pipeline wrapped around one capable agent: parse facts, classify, plan cheapest-first, investigate, synthesize — the model never counts. |
| [loglens](https://github.com/qa-veritas/loglens) | Code-aware log intelligence: slice a multi-GB log, find the *first* error (not the loudest), and correlate every `file:line` token back to the source that emitted it. |
| [skillpack](https://github.com/qa-veritas/skillpack) | Progressive-disclosure agent skills: cheap metadata always loaded, full instructions on match, heavy resources only when referenced. |
| [runbook-forge](https://github.com/qa-veritas/runbook-forge) | Generate an honest runbook from a resource's inventory + change journal, so every documented step has actually been performed and verified. |
| [intent-verify](https://github.com/qa-veritas/intent-verify) | Declare desired state as intent; verify it with checks that return `verified` / `failed` / `inconclusive` — never "probably fine." |

They share a worldview and compose: a change is checked for feasibility
against capacity, turned into observable verification, journaled, and —
when something breaks — triaged from parsed facts and the code that
emitted the failing log line.

### Ideas I keep coming back to

- **Determinism around nondeterminism.** Parse exact counts, statuses,
  and error signatures with cheap scripts *before* the model reasons, so
  the final answer never depends on an LLM counting.
- **Read before write.** Check feasibility against recorded capacity,
  act minimally and reversibly, verify with an observable signal, then
  write the result back. Reality wins over the file; if they disagree,
  fix the file.
- **Verification is the artifact.** A change isn't done when it's
  applied — it's done when a health endpoint, an open port, or a
  reconverged cluster says so.
- **Memory that survives turnover.** Inventory, contracts, runbooks, and
  an append-only journal in a git tree mean the next session — human or
  agent — inherits what was learned.

Every repo is small, runnable, MIT-licensed, and CI-checked. Read one in
a sitting.
