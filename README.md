# GH Agentic Workflows - tanulópéldák

Ez a mappa három példán keresztül mutatja be a GitHub Agentic Workflows (`gh aw`)
alapjait. Ezek nem hagyományos Actions YAML-fájlok: a `.md` fájl elején lévő
YAML frontmatter állítja be a futást és a jogosultságokat, az alatta lévő
Markdown pedig az agent feladata. A `gh aw compile` mindegyikből futtatható
`.lock.yml` workflow-t készít.

A mappa jelenleg nem Git-repó; másold ezeket a fájlokat egy GitHub-repó
gyökerébe, vagy inicializálj belőle repót, mielőtt a lentebbi `gh aw`
parancsokat futtatod.

> **Figyelem:** a GitHub Agentic Workflows nyilvános előzetes verzió. A futások
> AI-használatot számlázhatnak, a beállított safe outputok pedig GitHub-tartalmat
> hozhatnak létre vagy módosíthatnak. Először olvasd át a forrásokat és a
> generált lock fájlokat; éles repóban csak a saját igényeidre szabva kapcsold
> be őket. A heti jelentés futásonként egy issue-t hoz létre.

## A három példa

| Fájl | Mit tanít? | Mikor indul? | Engedélyezett eredmény |
| --- | --- | --- | --- |
| `01-repo-tour.md` | Egyszerű prompt, frontmatter, minimális olvasási jogosultság | Kézzel (`workflow_dispatch`) | Legfeljebb egy összefoglaló issue |
| `02-opt-in-issue-triage.md` | GitHub-esemény, toolset, címke-allowlist, safe outputs | Amikor egy issue megkapja az `ai-triage` címkét | Legfeljebb egy komment és egy engedélyezett címke |
| `03-weekly-repo-report.md` | Ütemezés, több GitHub toolset, korlátozott írás | Hetente hétfőn | Legfeljebb egy heti jelentés issue |

A triage-példához hozd létre az `ai-triage` repócímkét, és csak olyan issue-n
próbáld ki, amelyen engedélyezed az automatizálást. A javasolt címkéket
(`bug`, `question`, `documentation`, `enhancement`) a triage-workflow nem hozza
létre automatikusan; add hozzá őket a repóhoz, vagy módosítsd az allowlistet.

## Beállítás és futtatás

Szükséges egy GitHub-repó, amelyben engedélyezett az Actions, egy hitelesített
`gh` CLI, az Agentic Workflows kiterjesztés és egy támogatott AI-engine.
Copilotnál szervezeti repóban használható a szervezet által engedélyezett
`copilot-requests: write` számlázás; személyes repónál állítsd be a szükséges
`COPILOT_GITHUB_TOKEN` repository secretet. Más engine-ekhez az adott
szolgáltató kulcsát kell secretként felvenni.

```sh
gh auth login --scopes repo,workflow
gh extension install github/gh-aw
gh aw validate
gh aw compile
```

Ellenőrizd a `.github/workflows/*.lock.yml` fájlokat is; ezekből futtatja a
GitHub Actions a workflow-kat. Forrás vagy frontmatter módosítása után futtasd
`gh aw compile`-t újra, majd commitold együtt a `.md` és a hozzá tartozó
`.lock.yml` fájlt.

A `01-repo-tour` kézzel indítható a repó Actions lapjáról vagy ezzel:

```sh
gh aw run 01-repo-tour
```

A többi példa eseményre, illetve ütemezésre indul. Állapot és naplók:

```sh
gh aw status
gh aw logs 01-repo-tour
```

## Mit érdemes megfigyelni?

1. A frontmatterben az `on` mondja meg, mikor indul a workflow.
2. A `permissions` a lehető legszűkebb hozzáférést adja az agentnek. Az agent
   nem kap közvetlen írási jogot.
3. A `tools.github.toolsets` határozza meg, mely GitHub-adatokhoz használhat
   eszközöket.
4. A `safe-outputs` külön, korlátozott műveletként engedélyez publikálást.
   A `max` és az `allowed` szűkíti, hogy mi történhet.
5. A Markdown törzs írja le az agent feladatát; ez önmagában nem bővíti a
   jogosultságait.
6. A `.lock.yml` a lefordított Actions workflow. Nézd meg, hogyan lett a
   frontmatterből futtatható, több jobos workflow.

További olvasnivaló:

- [GitHub Agentic Workflows - Quickstart](https://github.github.com/gh-aw/setup/quick-start/)
- [GitHub Agentic Workflows - dokumentáció](https://github.github.com/gh-aw/)
- [GitHub dokumentáció: Agentic Workflows létrehozása](https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows)
