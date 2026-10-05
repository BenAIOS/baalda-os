# Baalda OS

Turn a [Baalda](https://baalda.com) vault into a second brain that Claude helps run. Baalda is a team second-brain app: plain Markdown files on your disk, edited together in real time, and read and written by your AI like a teammate. This plugin gives Claude four skills for setting that vault up, auditing it, keeping it current, and answering questions about Baalda itself.

## Skills

| Skill | Command | What it does |
|-------|---------|--------------|
| Setup | `/setup` | Builds the second-brain structure inside a Baalda vault (folders, system files, per-folder routing indexes, starter context), then interviews you so everything is personalized. Two modes: Solopreneurs/Professionals (default) or Business/Teams. |
| Optimizer | `/optimizer` | Audits the vault against 10 frameworks: CLAUDE.md quality, wiki structure, compression, context rot, memory, progressive disclosure, hygiene, cross-file synthesis, architecture and discoverability, plus Claude 5 rule rewriting. Every finding comes with a concrete fix you can apply now or save to a plan. Saves one HTML report. |
| Operator | `/operator` | Builds a personalized Operator prompt that keeps the vault current on a recurring cadence, then schedules it. It reads your `Context/` and `CLAUDE.md` first and only asks for what is missing: cadence, connectors, who gets escalation DMs, budgets and signature. |
| Baalda Guide | `/baalda-guide` | Answers questions about Baalda in plain language: features, file formats, sync, offline use, sharing, permissions, version history, AI and MCP, pricing, platforms and self-hosting. |

Each skill runs only when you call it by its command.

## How it treats your vault

- Setup, Optimizer and Operator keep every note's `doc_id` intact. Moves, renames and deletes go through the Baalda app or the Baalda MCP tools (`move_note`, `move_folder`, `delete_note`), so notes keep their history, backlinks and sharing.
- The skills never read, write or index `<vault>/.context/`, where Baalda keeps its own index and sync data.
- Before any bulk change, the skills suggest taking a vault checkpoint (Vault settings, Versioning) so you can roll back.

## Data and network use

This plugin contains only skill instructions and HTML templates. It ships no MCP server, hooks, scripts or executables, and it has no telemetry. It does not send your data to any server run by the plugin's author.

What the skills read, write and fetch:

- **Your vault.** The skills read and write Markdown files in the Baalda vault you run them from, using local file tools or the Baalda MCP connector if you have connected it. Setup writes the details you give it (your name, role, team, business, projects) into notes in your vault.
- **Links and files you provide.** During Setup you can paste links or point at files and folders. Claude reads those to personalize the vault.
- **Baalda documentation.** Baalda Guide fetches public docs from `https://raw.githubusercontent.com/naveedharri/baalda/main/` and pages on `https://baalda.com`. These are read-only requests that carry no vault content.
- **Google Fonts.** The Optimizer's HTML report loads fonts from `fonts.googleapis.com` and `fonts.gstatic.com` when you open it in a browser.
- **Your own connectors.** Operator detects which connectors you already have in Claude (for example a transcript tool like Fireflies, or a chat tool like Slack) and runs one read-only check on each. Nothing is sent during that check. If you enable a chat connector, the scheduled Operator can send escalation DMs to the one person you name, within the DM budget you set.
- **Scheduling.** Operator saves the rendered prompt in your vault and registers it as a recurring routine through Claude's schedule feature, so the prompt runs on the cadence you choose.

## Requirements

- A Baalda vault (desktop app or a synced vault). Get Baalda at [baalda.com](https://baalda.com).
- Optional: the Baalda MCP connector (Vault settings, MCP) so the skills can move and rename notes safely.
- Optional for Operator: the connectors you want it to use.

## Support

Open an issue at [github.com/naveedharri/baalda-os/issues](https://github.com/naveedharri/baalda-os/issues).

## License

MIT. See [LICENSE](LICENSE).
