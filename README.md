# Windows IT Tech Plugin

Turn Claude into a senior Windows 11 IT help desk technician. Includes a 3,500+ line troubleshooting knowledge base across 18 chapters, live system diagnosis via Windows-MCP, and tiered health scanning with automated logging.

## Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| `windows-it-tech` | Any Windows problem keyword (BSOD, PowerShell, Wi-Fi, printer, driver, update, boot, audio, registry, etc.) | Routes to the right knowledge base chapter, runs diagnostics, explains the problem, fixes it, and verifies the fix |
| `windows-health-scan` | "health check", "system scan", "run diagnostics", "how's my PC" | Tiered system health scanner with 20 checks across 3 tiers (Quick / Standard / Deep) |

## Health Scan Tiers

- **Quick** (~30s, 6 checks) — CPU/memory, disk space, critical services, pending reboot, uptime, Defender status
- **Standard** (~2min, 12 checks) — Quick + Windows Update, event log errors, WSL/Docker, startup bloat, driver problems, disk SMART
- **Deep** (~5min, 20 checks) — Standard + temp bloat, firewall, failed tasks, network, pagefile, reliability score, certs, GPU TDR

Results are logged to `%USERPROFILE%\Documents\Claude\Health-Logs\` with a Windows desktop notification summary.

## Knowledge Base Coverage

18 chapters covering every major Windows 11 troubleshooting domain:

| Chapter | Topics |
|---------|--------|
| 01 | PowerShell fundamentals, profiles, remoting, JEA |
| 02 | WSL2, Docker Desktop, Hyper-V |
| 03 | App installation, Winget, MSIX, Store repair |
| 04 | System repair (SFC, DISM), services management |
| 05 | Networking — Wi-Fi, DNS, VPN, firewall |
| 06 | BSOD analysis, Sysinternals, Event Viewer |
| 07 | Environment variables, registry editing |
| 08 | Recovery, system restore, reset |
| 09 | Quick reference commands |
| 10 | Hardware, audio, display troubleshooting |
| 11 | User profiles, BitLocker, Group Policy |
| 12 | Printing, disk management, RDP |
| 13 | Windows Update troubleshooting |
| 14 | Performance tracing (WPR/WPA) |
| 15 | Task Scheduler |
| 16 | Windows Update error code reference |
| 17 | Intune/MDM enrollment and policy |
| 18 | CBS logs, DISM internals, TSS diagnostic toolkit |

## Requirements

### Windows-MCP (required for live diagnosis)

This plugin requires the [Windows-MCP](https://github.com/nicekid1/windows-mcp) server to run diagnostic commands directly on the user's machine. Without it, Claude can only provide instructions — with Windows-MCP connected, Claude executes PowerShell commands, reads the registry, inspects processes, takes screenshots, and sends desktop notifications.

**MCP tools used:** PowerShell, Process, Registry, FileSystem, Screenshot, App, Clipboard, Notification, Shortcut, Snapshot, Click, Type, Scrape, Wait

### Desktop Commander (optional)

Used by the automated health check scheduled task for file logging operations.

## Plugin Structure

```
windows-it-tech-plugin/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── windows-it-tech/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── INDEX.md
│   │       ├── ch01-powershell.md
│   │       ├── ch02-wsl-docker.md
│   │       ├── ... (18 chapters)
│   │       └── appendices.md
│   └── windows-health-scan/
│       ├── SKILL.md
│       └── references/
│           └── health-checks.md
├── hooks/
│   └── hooks.json
└── README.md
```

## CLI Features (Claude Code only)

The CLI version includes additional features not available in Cowork:

- **SessionStart hook** — checks when the last health scan was run and nudges the user if it's been 7+ days
- **`allowed-tools` enforcement** — restricts tool permissions to only Windows-MCP tools during skill execution
- **Argument passthrough** — `/windows-it-tech:windows-health-scan quick` skips the tier selection prompt

## Installation

### Claude Code (CLI)
```bash
/plugin install windows-it-tech@claude-plugins-official
```

### Cowork
Install via Customize > Plugins, or add the skill files directly.

## Author

**LO** ([@blottters](https://github.com/blottters))

## License

MIT
