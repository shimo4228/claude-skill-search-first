Language: English | [日本語](README.ja.md)

# claude-skill-search-first

An [Agent Skill](https://agentskills.io/specification) that enforces a **research-before-coding** workflow. Before writing custom code, the agent searches for existing tools, libraries, MCP servers, and patterns — then makes an informed adopt/extend/build decision.

## Install

### Claude Code

```bash
# Copy into your global skills directory
cp -r skills/search-first ~/.claude/skills/search-first
```

### SkillsMP

```bash
/skills add shimo4228/claude-skill-search-first
```

## How It Works

1. **Need Analysis** — Define what functionality is needed
2. **Parallel Search** — Search npm/PyPI, MCP servers, GitHub, and existing skills
3. **Evaluate** — Score candidates on functionality, maintenance, community, docs, license, and deps
4. **Decide** — Adopt as-is, extend/wrap, compose multiple packages, or build custom
5. **Implement** — Install the chosen solution with minimal custom code

## When It Triggers

- Starting a new feature that likely has existing solutions
- Adding a dependency or integration
- Before creating a new utility, helper, or abstraction

## Decision Matrix

| Signal | Action |
|--------|--------|
| Exact match, well-maintained, MIT/Apache | **Adopt** — install and use directly |
| Partial match, good foundation | **Extend** — install + write thin wrapper |
| Multiple weak matches | **Compose** — combine 2-3 small packages |
| Nothing suitable found | **Build** — write custom, but informed by research |

## Examples

```
Need: Check markdown files for broken links
Search: npm "markdown dead link checker"
Found: textlint-rule-no-dead-link (score: 9/10)
Action: ADOPT — npm install textlint-rule-no-dead-link
Result: Zero custom code, battle-tested solution
```

## License

MIT