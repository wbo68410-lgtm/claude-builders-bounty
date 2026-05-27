# PR Reviewer Agent

`claude-review` reviews a GitHub pull request diff and returns a structured Markdown comment that can be pasted into the PR conversation.

## Setup

```bash
chmod +x claude-review
install -m 755 claude-review ~/.local/bin/claude-review
```

No package installation is required. The CLI uses only the Python standard library.

## Usage

```bash
claude-review --pr https://github.com/owner/repo/pull/123
```

Write the review to a file:

```bash
./claude-review --pr https://github.com/owner/repo/pull/123 --output review.md
```

Review a saved diff:

```bash
./claude-review --diff-file pr.diff
```

## Output Format

The generated Markdown includes:

- Summary of changes
- Identified risks
- Improvement suggestions
- Confidence score: `Low`, `Medium`, or `High`

## Claude Code Agent Prompt

Use `.claude/agents/pr-reviewer.md` as the Claude Code sub-agent definition. The agent should run `./claude-review --pr <url>`, inspect the Markdown output, and post or return the comment unchanged unless it finds a factual mistake.
