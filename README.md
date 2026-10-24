# OpenSpec snap

[![openspec](https://snapcraft.io/openspec/badge.svg)](https://snapcraft.io/openspec)

Snap packaging for [OpenSpec](https://github.com/Fission-AI/OpenSpec), a spec-driven development tool for AI coding assistants.

Unofficial build, not affiliated with or endorsed by Fission AI or the OpenSpec project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/openspec"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install openspec                   # or a local build: ./openspec_<version>_*.snap --dangerous
sudo snap connect openspec:removable-media   # optional: /media, /mnt
cd ~/my-project
openspec init --tools claude,cursor
openspec new change add-dark-mode
openspec validate add-dark-mode
openspec archive add-dark-mode
```

## Known limitations

### Configuration and data

The snap keeps its configuration and data in its own folder instead of `~/.config/openspec` and `~/.local/share/openspec`:

| What | Location |
|---|---|
| Config | `~/snap/openspec/current/.config/openspec/config.json` |
| Data (stores, worksets) | `~/snap/openspec/current/.local/share/openspec` |

`openspec config path` prints the exact path.

### Projects in hidden folders

The snap cannot read or write hidden files or folders directly in your home directory, such as `~/.notes`. Projects in normal folders work, including their hidden files such as `.claude/` or `.cursor/`.

### Programs installed on your system

The snap cannot run programs installed on your system:

- `openspec workset open` cannot start your editor or agent (VS Code, Cursor, Claude Code, Codex). It prints the path of the workspace file instead, which you can open yourself.
- `openspec config edit` only works with `vi`, the editor included in the snap's base: `EDITOR=vi openspec config edit`. Use `openspec config set` otherwise.
- `openspec feedback` cannot use the GitHub CLI. It prints a link to open the issue in your browser instead.

### Global tool folders

Tools that OpenSpec sets up outside the project, such as MiniMax Code skills in `~/.minimax/skills`, are written to the snap's own folder and are not seen by those tools. Per-project setup is not affected.

### Shell completion

Bash completion comes with the snap. `openspec completion install` writes to the snap's own folder and has no effect.

### Telemetry

OpenSpec sends anonymous usage statistics by default. To turn them off:

```bash
openspec config set telemetry.enabled false
```

The update check is turned off in the snap.
Update with `sudo snap refresh openspec`; `openspec install` cannot replace files inside the snap.

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). OpenSpec is MIT-licensed; the embedded Bun runtime, Git and the other dependencies carry their own licenses.
