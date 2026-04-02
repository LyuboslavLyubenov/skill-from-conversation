---
name: skill-from-conversation
description: Gathers learnings from the current conversation and converts them into a reusable skill
---
metadata:
  author: user
  version: "1.0.0"
  argument-hint: <new-skill-name>
---

# Skill from Conversation

Gathers learnings from the current conversation and converts them into a reusable skill file.

## When To Use

- You've completed a multi-step task you want to save as a reusable workflow
- User explicitly requests creating a skill from the conversation
- User asks "how did we accomplish X?" or "can you save this process?"

## Steps

1. **Analyze the Conversation**
   - Review the steps taken in this conversation
   - Identify the core goal/purpose
   - Extract key actions, tools used, and decisions made
   - Ignore one-off decisions, errors, and retries
   - Note any tools/commands used repeatedly

2. **Generalize Steps**
   - Convert specific values into placeholders/parameters
   - Remove context-specific details
   - Focus on the repeatable pattern

3. **Determine Metadata**
   - Choose a valid skill name (lowercase, hyphens only, 1-64 chars)
   - Write a clear description (max 1024 chars)
   - Identify useful parameters if needed
   - Set argument-hint if skill takes arguments

4. **Generate SKILL.md**
   - Create proper YAML frontmatter with name and description
   - Write clear "When To Use" section
   - Document step-by-step instructions
   - Include examples or templates if relevant

5. **Preview and Confirm**
   - Show the generated skill content
   - Ask user to confirm or modify
   - Get final skill name from user

6. **Write File**
   - Create directory: `~/.config/opencode/skills/<skill-name>/`
   - Save to `~/.config/opencode/skills/<skill-name>/SKILL.md`

7. **Report**
   - Confirm skill name and file location
   - Summarize what the skill does
   - List any parameters defined

## Output Format

After creating the skill, report:
- Skill name
- File location
- Brief summary of what the skill does
- Any parameters or arguments it accepts
