# openclaw-agent Skill

Manage OpenClaw agents with Git version control.

## Commands

```bash
# Track an existing agent
openclaw-agent track <name>

# Clone from GitHub
openclaw-agent clone <owner/repo>

# Import to OpenClaw
openclaw-agent import <name>

# Commit changes
openclaw-agent commit <name> <message>

# Push to remote
openclaw-agent push <name>

# Pull from remote
openclaw-agent pull <name>

# Sync (pull + import)
openclaw-agent sync <name>

# Publish to GitHub
openclaw-agent publish <name>

# List managed agents
openclaw-agent list

# Untrack agent
openclaw-agent untrack <name>
```

## Directory Structure

```
~/.openclaw-agents/repos/<agent>/
├── config.json              # Agent metadata
└── workspace-<agent>/
    ├── AGENTS.md            # Agent persona
    ├── IDENTITY.md          # Agent identity
    ├── SOUL.md              # Agent soul
    └── skills/              # Agent skills
```

## Config.json Fields

Only these fields are synced:
- `id`
- `name`
- `skills` (skill names)
- `identity`
- `subagents`
- `tools`

## Skills in config.json

Skills are stored as names, not paths:
```json
{
  "skills": ["cli-anything", "github"]
}
```

When tracking, skills are resolved from:
1. `~/.openclaw/skills/<name>`
2. `workspace/skills/<name>`
3. `skills.load.extraDirs` in openclaw.json

## Sync Flow

```
track → Git repo → push → GitHub
                         ↓
                   clone/pull
                         ↓
import → workspace + openclaw.json (skills only)
```
