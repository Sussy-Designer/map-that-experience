# map-that-experience

A Claude Code skill, `/map-it`, that maps a MYOB Business or Payments experience onto a Miro board.

It reads MYOB's official help, optionally pulls what is already documented about customer problems in Confluence, and lays the workflow out phase by phase with a numbered, empty slot for a screenshot at every step. You drop your own screenshots into the slots afterwards.

## Two ways to use it

Start with `/map-it`. It asks which path you want and which Miro board to use.

1. **Test a problem or assumption.** Give it a problem customers are having, or an assumption such as "online payments save customers time". It maps the assumption against the current workflow and reports:
   - a verdict: Aligns, Partly aligns, Does not align, or Not enough evidence;
   - evidence for and against, with sources;
   - a fit rating for every step (Addressed, Partly, Gap, No evidence);
   - opportunities, each tied to a step and its evidence.
2. **Overview of a current experience.** Name a job, such as "I want to send an invoice", and it maps the current experience as a happy path. Add "all features" to include optional steps.

If your request already makes the path clear, it skips the question and says which path it is taking.

## What you get on the board

- A title written as the customer's own need, in the first person.
- A first frame, "Does it align?" (path 1) or "What we already know" (path 2).
- One frame per phase. Each step is a grey slot for a screenshot, with a note beneath it that uses the exact UI labels from the help and links to the help article it came from.
- A final frame with the happy path, prerequisites, caveats and every source.

Screenshots are optional and never needed to start.

## Requirements

- [Claude Code](https://claude.com/claude-code).
- A Miro connector the skill can write to. It uses Miro through Runlayer by default and falls back to the claude.ai Miro connector.
- Optional: an Atlassian connector with access to your Confluence, for the internal evidence step. Without it the skill still runs and says its verdict rests on help alone.
- Internet access to the public MYOB help site.

## Install

Copy the skill into your Claude Code skills folder.

For one project:

```bash
cp -r .claude/skills/map-it <your-project>/.claude/skills/
```

For every project:

```bash
cp -r .claude/skills/map-it ~/.claude/skills/
```

Start a new Claude Code session and run `/map-it`.

## Good to know

- **Help is not the live product.** Steps come from help articles and have not been verified in the product. Many help pages mix MYOB Business with AccountRight content, and the skill flags pages that are old or mixed.
- **Internal content.** When it uses Confluence, the board contains paraphrased internal findings. It never puts customer names, transcripts or verbatim quotes on a board, and it labels drafts and pages in personal spaces. Check who can see your board before sharing it.
- **It adds, it does not replace.** The skill checks the board for free space and places new sections there. It never deletes or overwrites your existing content.
- **Uploading screenshots.** Some Runlayer set-ups block image uploads with a security scan. When that happens the skill leaves the slots in place and tells you which file belongs in which slot, so you can drop them in by hand.

## Repository layout

```text
.claude/skills/map-it/SKILL.md   the skill: paths, workflow, board layout and rules
README.md                        this file
```

Your screenshots and working files go in a local `walkthroughs/` folder, which is ignored by git.
