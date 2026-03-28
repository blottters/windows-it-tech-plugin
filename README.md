# Windows IT Tech — Claude Cowork Plugin

A drop-in Claude Cowork plugin that turns Claude into a senior Windows 11 IT help desk technician. Describe any Windows problem and Claude diagnoses it, explains what's broken, and fixes it — with live command execution when Windows-MCP is connected.

## Install

Download `windows-it-tech.plugin` from [Releases](https://github.com/blottters/windows-it-tech-plugin/releases) and open it in Claude Desktop. The plugin appears in your Cowork skills automatically.

## What's Included

- **Skill:** `windows-it-tech` — auto-triggers on any Windows problem keyword
- **Knowledge Base:** 3,500+ lines across 18 chapter files covering 38 troubleshooting domains
- **Diagnostic Protocol:** RISEN+ReAct framework — classify, gather context, diagnose, fix, verify, prevent
- **Chapter Routing:** INDEX.md maps symptoms to chapters; Claude loads only 1-3 relevant chapters per problem (context-efficient)

## Coverage

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

## MCP Connectors (Optional but Recommended)

### Windows-MCP — Live Diagnosis
With Windows-MCP connected, Claude runs PowerShell commands, inspects processes, reads the registry, captures screenshots, and sends desktop notifications directly on your machine. Without it, Claude still gives accurate instructions — you just run the commands yourself.

### Desktop Commander — File & Process Operations
Adds process management, file search, and directory operations. Used by the health check automation for logging.

## Plugin Structure

```
windows-it-tech-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── windows-it-tech/
│       ├── SKILL.md
│       └── references/
│           ├── INDEX.md
│           ├── Ch01-PowerShell.md
│           ├── ... (18 chapters)
│           └── Appendices.md
├── windows-it-tech.plugin    # Packaged plugin file
└── README.md
```

## Related

- [Windows-11-Bible](https://github.com/blottters/Windows-11-Bible) — Full repo with monolith file, RISEN+ReAct system prompt, and health check automation

## License

MIT
