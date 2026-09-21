# setup-paper-material

English | [简体中文](README.md)

A project-scoped Codex skill for organizing paper illustrations, literature notes, and research conclusions, with traceable sources, progress tracking, and registration of approved materials.

**Enabled only through explicit user invocation.** You choose which projects need paper material management. Once enabled, agents working in that project continue to follow its generated rules. Both Git and non-Git projects are supported.

## Installation and usage

Download or clone this repository into a folder named `setup-paper-material` inside your personal skills directory. Keep `SKILL.md`, `agents/`, and `assets/` together. The personal skills directory is `$CODEX_HOME/skills`, or `.codex/skills` under your user home directory when `CODEX_HOME` is unset. Cloning a private repository requires access to it.

Explicitly invoke the skill in the project you want to manage:

```text
$setup-paper-material Initialize paper material management for this project.
```

Invocation authorizes initialization without another enablement confirmation. If materials already exist, the skill preserves them and fills in missing items; conflicting rules require clarification. You can explicitly override the default directory names.

For subsequent work, specify an organization or registration task:

```text
$setup-paper-material Organize the detection probability curve materials, record their sources, and update progress.
```

```text
$setup-paper-material Check in the detection probability curve v1 we just approved.
```

## What it creates in your project

```text
paper_material/
├── AGENTS.md
├── README.md
├── TODO.md
├── docs/
│   └── check_in/
│       └── README.md
└── illustrations/
    └── check_in/
        └── README.md
```

It also adds a rule pointer to the project's root `AGENTS.md`, preserving other instructions. Illustration topic directories are created as needed.

| Location | Purpose |
| --- | --- |
| `paper_material/AGENTS.md` | Persistent project rules for paper materials |
| `paper_material/README.md` | Index of sources, results, applicable conditions, material paths, and status |
| `paper_material/TODO.md` | In-progress, completed, and pending paper preparation work only |
| `docs/` | Literature notes, analysis, and conclusions, optionally grouped by topic |
| `illustrations/<topic>/` | Illustrations, editable sources, scripts, and exports for one topic |
| Both `check_in/` directories | Approved versions with registration authorization and source indexes |

## Approval and check in

Material status distinguishes: **in progress → awaiting approval → approved, awaiting registration → registered**.

- “This figure is good” can approve a version, but does not automatically authorize registration. Registration requires an explicit **check in** request or clear registration authorization.
- When the object or intent of feedback is unclear, the agent asks at the end of the turn after completing other authorized work. The material remains unregistered until clarified.
- Registration copies approved documents, or selected figures, editable sources, and necessary small scripts/configuration files, while preserving working sources. Large datasets, model weights, and experimental results are referenced by path and version.
- The registration index records sources, versions, descriptions, approval and authorization evidence, and dates. Figures also include confirmed visual details.
- Revisions require fresh approval and registration authorization. Historical registered versions are retained, with the currently adopted version identified for preferred use in the paper.

Here, check in means registering paper materials; it is unrelated to Git commit or push.

## Scope and repository files

The skill manages materials. Plotting, analysis, literature work, and writing follow the specific user request. It does not manage overall project development or clean up, delete, or migrate existing directories during initialization. Original experiment files remain in place.

- [SKILL.md](SKILL.md): initialization, maintenance, and completion checks.
- [Project rule template](assets/paper-material-AGENTS.md): ongoing material management rules written into the project.
- [Invocation policy](agents/openai.yaml): explicit invocation configured with `allow_implicit_invocation: false`.

This guide is available in English and Chinese. The skill instructions and project rule template are currently written in Chinese.

## License

This skill is distributed under the [MIT License](LICENSE). Paper materials retain the licensing terms determined by their sources and rights holders.
