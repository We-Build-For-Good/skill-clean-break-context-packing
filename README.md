# Clean Break & Context Packing Protocol

> **An open-source AI engineering protocol from [We Build for Good](https://webuildforgood.com)**  
> *Freeze working state cleanly. Orient any successor in under 30 seconds.*

---

## Overview

`clean-break-context-packing` is an operational protocol for AI coding assistants (Claude Code, Cursor, Antigravity, OpenAI Codex).

It prevents the chaos of mid-session disconnects, token limits, and abrupt session ends. It mandates a 60-second wrap-up sequence that commits checkpoints, cleans the git tree, and leaves a crystal-clear continuation line.

---

## The 4 Steps

1. **Freeze the Line**: Stop starting new work; leave files syntactically valid.
2. **Commit the Checkpoint**: Commit working code with a descriptive WIP message.
3. **Verify the Tree**: Confirm `git status` is clean.
4. **Write the 3-Line Continuation Pointer**: State the branch/commit, verified tests, and the single next file/line to edit.

---

## Installation

### For Claude Code
```bash
git clone https://github.com/webuildforgood/skill-clean-break-context-packing.git ~/.claude/skills/clean-break-context-packing
```

### For Cursor
```bash
mkdir -p .cursor/skills
git clone https://github.com/webuildforgood/skill-clean-break-context-packing.git .cursor/skills/clean-break-context-packing
```

### For Antigravity / Open Agent Skills
```bash
mkdir -p .agents/skills
git clone https://github.com/webuildforgood/skill-clean-break-context-packing.git .agents/skills/clean-break-context-packing
```

---

## License

MIT License. Developed and maintained by [We Build for Good](https://webuildforgood.com).
