# kavisha-claude-skills

Custom Claude Code / Cursor skills, versioned here as source of truth.

## Skills

| Skill | Purpose |
|-------|---------|
| `daily-tweet` | Reads the current conversation and generates a ready-to-post tweet or short thread in Kavisha's building-in-public voice. Invoke: `/daily-tweet`. |
| `handle-edit-failures` | When a file edit fails once, stops retrying and gives the exact content + location to apply manually. Prevents compounding failures. |

## Usage

Each skill lives in its own folder: `skill-name/SKILL.md`.

To install into a project:
```bash
# 1. Copy from this repo into the project
mkdir -p "/path/to/project/.agents/skills/skill-name"
cp "skill-name/SKILL.md" "/path/to/project/.agents/skills/skill-name/SKILL.md"

# 2. Create symlink for Claude Code
cd "/path/to/project"
mkdir -p .claude/skills
ln -s "$(pwd)/.agents/skills/skill-name" .claude/skills/skill-name
```

Cursor reads from `.agents/skills/` automatically. Claude Code reads from `.claude/skills/` — the symlink bridges the two.

## Updating a Skill

1. Edit the SKILL.md in this repo
2. Commit and push
3. Copy the updated file into any projects that use it
