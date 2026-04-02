# skill-from-conversation

An [opencode](https://opencode.ai) skill that extracts learnings and workflows from a conversation and converts them into a reusable skill file.

## What It Does

When you've just completed a multi-step task in opencode (debugging an issue, setting up a project, writing a feature, etc.), this skill analyzes the conversation and distills the steps into a structured, reusable `SKILL.md` that can be loaded in future sessions.

Skills are opencode's way of injecting domain-specific instructions and workflows into a conversation. They live as `SKILL.md` files under `~/.config/opencode/skills/<skill-name>/`.

## Installation

Copy the `SKILL.md` file into your opencode skills directory:

```bash
mkdir -p ~/.config/opencode/skills/skill-from-conversation
cp SKILL.md ~/.config/opencode/skills/skill-from-conversation/
```

## How to Use

1. **Have a conversation** where you complete a multi-step task (e.g. setting up auth, deploying an app, configuring a linter).
2. **Ask opencode to create a skill** — for example:
   - *"Create a skill from this conversation"*
   - *"Save this process as a skill called setup-prisma"*
   - *"Can you make this reusable?"*
3. **Review the output** — the skill will be previewed before saving so you can confirm or modify it.
4. **Use it next time** — the new skill will be available in future opencode sessions.

## What to Expect

The skill will:

1. **Analyze** your conversation to identify the core goal, key actions, tools used, and decisions made.
2. **Generalize** specifics into reusable patterns (file paths become placeholders, specific values become parameters).
3. **Generate** a proper `SKILL.md` with YAML frontmatter, "When To Use" section, and step-by-step instructions.
4. **Preview** the skill content and ask for your confirmation before saving.
5. **Save** it to `~/.config/opencode/skills/<skill-name>/SKILL.md`.

One-off errors, retries, and context-specific details are intentionally excluded — only the repeatable workflow is captured.

## Example

This very skill was created using itself. Here is the conversation that produced it:

> **User**: *"can you extract the skill that creates skill from a conversation and create git repo and publish it to my github"*

The conversation involved:

1. Reading the skill files from `~/.config/opencode/skills/skill-from-conversation/`
2. Discovering `gh` CLI was unavailable, falling back to plain `git`
3. Getting the GitHub username
4. Creating a local repo with `SKILL.md` and `README.md`
5. Initializing git, committing, and pushing to GitHub
6. Editing the README with detailed docs

Running the skill on that conversation produced:

```markdown
---
name: publish-opencode-skill
description: Extracts an opencode skill from the local skills directory, creates a standalone git repo with README, and publishes it to GitHub
---
metadata:
  author: user
  version: "1.0.0"
  argument-hint: <skill-name>
---

# Publish an OpenCode Skill to GitHub

## When To Use

- You want to share an opencode skill as a standalone GitHub repository
- User asks to "publish", "extract", or "export" a skill

## Steps

1. **Locate the Skill**
   - Read `~/.config/opencode/skills/<skill-name>/SKILL.md`
   - Check for any scripts or additional files in the skill directory

2. **Ask for GitHub Username**
   - Prompt for the user's GitHub username if not known
   - Remind user to create an empty repo at https://github.com/new (no README, no license)

3. **Create Local Repo**
   - `mkdir -p <skill-name>`
   - Copy `SKILL.md` into the directory
   - Write a `README.md` with: description, installation instructions, usage, example, and license

4. **Init and Commit**
   - `git init`
   - `git add -A`
   - `git commit -m "Initial commit: <skill-name>"`

5. **Push to GitHub**
   - `git remote add origin git@github.com:<username>/<skill-name>.git`
   - `git push -u origin main`

6. **Report**
   - Confirm the repo URL
   - Summarize what was published
```

## Skill Name Rules

- Lowercase letters and hyphens only
- 1–64 characters
- Must be unique within your skills directory

## License

MIT
