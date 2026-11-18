# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A content-only collection of agent skills (Markdown `SKILL.md` files) for anti-"AI slop" frontend design. There is no build, lint, or test tooling, and no package manifest. Changes are edits to Markdown, validated by reading and by trying the skill with an agent.

## Layout

- `skills/<folder>/SKILL.md`: one skill per folder. Each has YAML frontmatter (`name`, `description`). Distribution relies on the `npx skills add` CLI scanning `skills/`.
- `skills/llms.txt`: one-line summaries of every skill. Keep in sync with skill descriptions.
- `skill.sh`: a local name-to-path registry (`source ./skill.sh <name>` prints the path). New skills must be added to its `SKILLS` map.
- `README.md`: skills table, install instructions, dial docs. `CHANGELOG.md`: version history (v1 to v2 rationale).
- `.github/copilot-instructions.md`: a short manifesto Copilot auto-loads; it points at `skills/`.
- `research/`: background writing on model "laziness" (findings, root causes, remediation) that informs rules such as anti-truncation.

## Folder name vs install name

The folder name and the install name differ, and the **frontmatter `name:`** is what `npx skills add --skill "<name>"` takes. For example, folder `taste-skill` installs as `design-taste-frontend`, `taste-skill-v1` as `design-taste-frontend-v1`, `gpt-tasteskill` as `gpt-taste`, `redesign-skill` as `redesign-existing-projects`, and `soft-skill` as `high-end-visual-design`. The README table lists every mapping. Do not rename a frontmatter `name:` casually: it breaks existing users' install commands (the v2 rewrite deliberately kept `design-taste-frontend` stable).

## Skill families

- **Implementation skills** output code: `taste-skill` (default, v2 experimental, ~1200 lines), `taste-skill-v1` (frozen legacy, preserved for users who depend on its exact behavior), `gpt-tasteskill`, `redesign-skill`, `soft-skill`, `minimalist-skill`, `brutalist-skill`, `stitch-skill` (also carries a `DESIGN.md` export format), `output-skill`, `image-to-code-skill`.
- **Image-generation-only skills** output reference images and never code: `imagegen-frontend-web`, `imagegen-frontend-mobile`, `brandkit`.

## Conventions when editing skills

- `taste-skill` (v2) is numbered by section (§0 Brief Inference, §2 Brief to Design System Map, §8 Dark Mode, §11 Redesign Protocol, §12 Block Library contract, etc.) and cross-references sections by number. Renumbering a section means fixing references elsewhere in that file and in the CHANGELOG.
- v2 bans em-dashes in its own prose and output rules. Recent commits purged them (remaining uses are intentional rule references), so do not introduce new ones in `taste-skill`.
- Its three tuning dials are `DESIGN_VARIANCE`, `MOTION_INTENSITY` and `VISUAL_DENSITY` (1-10), set at the top of the file and documented in the README "Settings" section. Keep both in sync if they change.
- After adding, renaming, or re-describing a skill, update all of: the README skills table (with install name), `skills/llms.txt`, `skill.sh`, and the CHANGELOG when behavior changes.
- Commit messages follow conventional style (`feat(skill): ...`, `docs(readme): ...`).
