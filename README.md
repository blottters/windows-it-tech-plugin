# Windows IT Tech Plugin

A Claude Cowork plugin that turns Claude into a senior Windows 11 IT help desk technician. Includes a 3,500+ line troubleshooting knowledge base (38 sections), live diagnosis capabilities, and automated health monitoring.

## What It Does

When you describe any Windows problem — blue screens, frozen apps, PowerShell broken, Wi-Fi dropping, printer not working, driver issues, update failures, slow boot, audio gone, or literally anything else — this plugin activates and Claude becomes your IT tech.

Claude will:
- Route your problem to the right chapter(s) from the knowledge base
- Run diagnostic commands directly on your machine (with Windows-MCP)
- Explain what's broken and why
- Fix it with specific, tested commands
- Verify the fix worked

## Components

| Type | Name | Purpose |
|------|------|---------|
| Skill | `windows-it-tech` | Core troubleshooting skill with 18 chapter reference files covering all Windows 11 domains |
| Skill | `windows-health-scan` | Tiered system health scanner — 20 checks across 3 tiers (Quick / Standard / Deep) |

## Required MCP Connectors

This plugin works best with these MCP servers connected in your Cowork session:

### Windows-MCP (required for live diagnosis)
Provides PowerShell execution, process inspection, registry access, filesystem operations, screenshots, and desktop notifications. Without this, Claude can only give you instructions — with it, Claude runs the commands directly.

**Tools used:** `mcp__Windows-MCP__PowerShell`, `mcp__Windows-MCP__Process`, `mcp__Windows-MCP__Registry`, `mcp__Windows-MCP__FileSystem`, `mcp__Windows-MCP__Screenshot`, `mcp__Windows-MCP__App`, `mcp__Windows-MCP__Clipboard`, `mcp__Windows-MCP__Notification`, `mcp__Windows-MCP__Shortcut`, `mcp__Windows-MCP__Snapshot`, `mcp__Windows-MCP__Click`, `mcp__Windows-MCP__Type`, `mcp__Windows-MCP__Scrape`, `mcp__Windows-MCP__Wait`

### Desktop Commander (optional, for health monitoring)
Provides process management, file search, and directory operations. Used by the automated health check scheduled task for logging and file operations.

**Tools used:** `mcp__Desktop_Commander__start_process`, `mcp__Desktop_Commander__list_directory`, `mcp__Desktop_Commander__read_file`, `mcp__Desktop_Commander__write_file`

## Knowledge Base Coverage

| Chapter | Topics |
|---------|--------|
| Ch01 | PowerShell fundamentals, profiles, remoting, JEA |
| Ch02 | WSL2, Docker Desktop, Hyper-V |
| Ch03 | App installation, Winget, MSIX, Store repair |
| Ch04 | System repair (SFC, DISM), services management |
| Ch05 | Networking (Wi-Fi, DNS, VPN, firewall) |
| Ch06 | BSOD analysis, Sysinternals, Event Viewer |
| Ch07 | Environment variables, registry editing |
| Ch08 | Recovery, system restore, reset |
| Ch09 | Quick reference commands |
| Ch10 | Hardware, audio, display troubleshooting |
| Ch11 | User profiles, BitLocker, Group Policy |
| Ch12 | Printing, disk management, RDP |
| Ch13 | Windows Update troubleshooting |
| Ch14 | Performance tracing (WPR/WPA) |
| Ch15 | Task Scheduler |
| Ch16 | Windows Update error code reference |
| Ch17 | Intune/MDM enrollment and policy |
| Ch18 | CBS logs, DISM internals, TSS diagnostic toolkit |

## Usage

### Troubleshooting
Just describe your Windows problem. The `windows-it-tech` skill auto-triggers on any Windows-related keywords including: cmd, PowerShell, .exe, BSOD, Device Manager, Event Viewer, regedit, services.msc, blue screen, frozen, Wi-Fi, printer, driver, update, boot, audio, Bluetooth, Docker, WSL, Task Scheduler, BitLocker, Group Policy, registry, or any Windows tool name.

### Health Scanning
Say "health check", "system scan", "run diagnostics", or "how's my PC" and the `windows-health-scan` skill activates. Claude asks which tier you want:

**Tier 1 — Quick Scan** (~30 sec, 6 checks)
Memory/CPU, disk space, critical services, pending reboot, uptime, Defender status.

**Tier 2 — Standard Scan** (~2 min, 12 checks)
Quick + Windows Update, event log errors, WSL/Docker, startup bloat, driver problems, disk SMART health.

**Tier 3 — Deep Scan** (~5 min, 20 checks)
Standard + temp bloat, firewall status, failed scheduled tasks, network connectivity, pagefile health, reliability score, certificate expiry, GPU TDR crashes.

Results are logged to `%USERPROFILE%\Documents\Claude\Health-Logs\` and a Windows notification is sent with the summary.

## Plugin Structure

```
windows-it-tech-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── windows-it-tech/
│   │   ├── SKILL.md
│   │   └── references/ (18 chapters + INDEX + Appendices)
│   └── windows-health-scan/
│       ├── SKILL.md
│       └── references/health-checks.md (all 20 checks)
├── windows-it-tech.plugin
└── README.md
```

## Related

- [Windows-11-Bible](https://github.com/blottters/Windows-11-Bible) — Full repo with monolith file, RISEN+ReAct system prompt, and health check docs

## License

MIT
