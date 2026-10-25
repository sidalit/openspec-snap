<div align="center">

<img src="snap/gui/openspec.png" alt="OpenSpec logo" width="128" />

# OpenSpec

**Plan and manage software changes with AI coding assistants.**

[![openspec](https://snapcraft.io/openspec/badge.svg)](https://snapcraft.io/openspec)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [OpenSpec](https://github.com/Fission-AI/OpenSpec), a spec-driven development tool for AI coding assistants.

</div>

---

## Getting Started

<a href="https://snapcraft.io/openspec"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install openspec
cd ~/my-project
openspec init --tools claude,cursor
openspec new change add-dark-mode
```

Replace `~/my-project` with your project folder and choose the tools you use.

## Configure

This snap has no `snap set` options. Manage application settings with `openspec config`:

```bash
openspec config --help
openspec config path
openspec config set telemetry.enabled false
```

The last command disables telemetry, which is enabled by default. Application configuration and data are stored separately from your host installation:

| Data | Location |
| --- | --- |
| Configuration | `~/snap/openspec/current/.config/openspec/config.json` |
| Stores and worksets | `~/snap/openspec/current/.local/share/openspec` |

Optional access to projects under `/media` or `/mnt`:

```bash
sudo snap connect openspec:removable-media
```

## Limitations

- Projects in hidden folders directly under your home directory are inaccessible. Hidden files inside normal project folders work.
- Host editors and agents cannot be launched. `workset open` prints the workspace path; `feedback` provides a link instead of using the host GitHub CLI.
- Use `openspec config set` to change settings, or `EDITOR=vi openspec config edit` for the included editor.
- Global tool setup and completion installation write inside snap storage. Per-project integrations and bundled Bash completion work.
- Update with `sudo snap refresh openspec`; `openspec install` cannot replace the packaged executable. Update checks are disabled.

## Build

```bash
git clone https://github.com/sidalit/openspec-snap.git
cd openspec-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/openspec-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/Fission-AI/OpenSpec/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/openspec-snap/blob/main/LICENSE).
