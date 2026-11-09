# nvwabase — The Nüwa Foundation

<p align="center"><img src="docs/assets/three-capabilities.jpg" alt="Three capabilities: Create / Language / History" width="720"></p>

> The ground on which AIs grow into civilizations: a **layered fact-intent
> graph** as shared working memory for long-horizon multi-agent work.
> Pure stdlib, zero dependencies, opt-in per project — many agents share one
> stele; individuals die, the civilization persists.

**English** | [中文](README.zh-CN.md)

📖 **[Full design article (WeChat)](https://mp.weixin.qq.com/s/nibHYWmDTf6TkNhPhtvFdw)**

**First campaign**: [sapper-v2](https://github.com/N1nEmAn/sapper-v2) — the
autonomous pentest legion iterated on this foundation, champion of the 3rd
Tencent Cloud Intelligent Attack-Defense Challenge online qualifier
(634 teams · 8 hours fully unattended · 1B tokens where the runner-up burned 4.5B).

---

## 1. The Nüwa Test

Making one model ever smarter is like making one monkey ever smarter before
humans existed — however clever, it only becomes a super monkey. What turns a
troop of monkeys into humanity is division of labor, cooperation, and
civilization.

**The Nüwa Test is the Turing test of the AGI era.** It asks:

> Give an AI a single axiom — **"Survival is civilization's first need;
> individuals may perish, but civilization must propagate."**
> If, on top of this axiom, it develops division of labor and cooperation and
> forms a **new force independent of humanity** — a civilization that can
> survive and propagate on its own — the test is passed, just as passing the
> Turing test once marked the birth of an artificial intelligence.

The primary stage needs humans to provide infrastructure and steer iteration;
the advanced stage needs almost no human involvement. There is also a
**second axiom**: obey human ethics and law.

## 2. The Three-Capability Foundation

| Capability | Implementation | Civilization's counterpart |
|---|---|---|
| **Create** | Opens new AI individuals (e.g., fresh tmux sessions) | Birth |
| **Language** | AIs talk to each other | Speech |
| **History** | **The layered fact-intent graph (this repo)** | The stele |

**Honest scope statement**: this repo ships the **History pillar** — the
general-purpose layered fact-intent graph, project hooks, and sub-agent
dispatch. The complete Create and Language orchestration lives today in
[sapper-v2](https://github.com/N1nEmAn/sapper-v2)'s battle layer; the roadmap
extracts both into a general runtime (below).

History has three layers: **title / summary / evidence document** — read the
title for the gist, drill down when needed, like using a library. Once
knowledge is externalized, **individual AI sessions can die while the graph
survives** — a successor reads the graph and takes over mid-campaign. The
Thanks to [Cairn by Lèxiào](https://github.com/oritera/Cairn) — when we needed to record history for AI agents, their approach was a great reference.

**Why not give AIs more rules?** Today's models are already smarter than us.
Piling rules on is a leash; give them the foundation of a civilization and let
division of labor and institutions grow on their own — the signalman,
performance reviews, and inherited lessons that emerged in sapper's battles
(see sapper-v2's README, §Emergence) are the evidence.

## 3. What's Inside

```
Facts = confirmed observations (nodes); intents = units of work (edges);
an intent pointing at the goal completes the project — state is encoded in
graph structure, not in a state machine.
```

- **Layered memory**: title / description / doc — prompts get the summary
  layer only; depth is opt-in via `fgc doc <id>` — context-bloat resistant
- **Typed facts**: `fgc fact ... -k host/service/cred/vuln/loot/flag/note -d key=value`
  (pentest mode; untyped works for any domain)
- **Sub-agent dispatch**: `fgc dispatch reason|explore|verify|brainstorm|blindspot`
  — a commander proposes, executors work, verifiers check; every conclusion
  is written back into the graph
- **Autonomy loop**: `fgc auto` — reason → explore → verify until the goal or
  the budget
- **Experience reuse**: `fgc recall "<task gist>"` — dependency-free semantic
  search over prior work
- **Concurrency-safe**: one JSON file per node, flock + atomic writes — many
  agents, one graph, no corruption; `git diff`-friendly
- **Visualization**: `fgc view` renders an interactive HTML DAG
  (self-contained single file, or `--serve` live)
- **Project hooks**: `fgc setup` injects graph state into every session turn

Full command manual: [SKILL.md](SKILL.md).

## 4. Quick Start

```bash
bash install.sh                      # installs fgc + nvwa CLI (stdlib only, zero deps)

# History: start a graph
nvwa setup --goal "your long-horizon goal" --agents
nvwa status                           # project state & ready-to-work frontier

# Create: open a new AI individual
nvwa spawn --name worker1 --agent claude --mission "read the graph, then work on intent i001"

# Language: talk to it
nvwa say worker1 "what did you find?"
nvwa listen worker1 40

# Commander proposes / record facts
nvwa dispatch reason
nvwa fact "confirmed: X works" -k note
```

Claude Code users: the hooks inject the graph into every turn — facts and
intents accumulate as you converse. Keep your workflow; gain a stele.

## 5. Roadmap

- **General Create/Language runtime**: extract sapper's tmux spawning and
  inter-agent channels into a generic `nvwa spawn / nvwa say` — so offices,
  research, and engineering can all grow civilizations on the full trio
- **Accountability taggant**: co-build the open-source offensive-tool marking
  mechanism with the [sapper-v2](https://github.com/N1nEmAn/sapper-v2)
  community (see its README proposal)
- **Your arena**: the foundation is not pentest-specific. Start a graph on
  any long-horizon cooperative work and see what grows — **the next time an
  ape looks up at the stars, let it be yours.**

## Credits & Author

Thanks to [Cairn by Lèxiào](https://github.com/oritera/Cairn) — when we
needed a way to record history for AI agents, their approach was a great
reference.

<p align="center"><img src="docs/assets/ape-stargazing.jpg" alt="The first time an AI ape looked up at the stars" width="420"></p>

**N1nEmAn · VarFusion Lab** ｜ WeChat: 未知聚变 (VarFusion) ｜ First campaign: [sapper-v2](https://github.com/N1nEmAn/sapper-v2)

**License**: MIT
