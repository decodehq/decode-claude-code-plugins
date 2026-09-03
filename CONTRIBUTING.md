# Adding a plugin

## 1. Create the directory

```bash
mkdir -p plugins/my-plugin/.claude-plugin
```

## 2. Write the plugin manifest

`plugins/my-plugin/.claude-plugin/plugin.json`:

```json
{
  "name": "my-plugin",
  "description": "One sentence on what this plugin does.",
  "version": "0.1.0",
  "author": { "name": "DECODE", "url": "https://github.com/decodehq" }
}
```

The `name` must be kebab-case and must match the directory name.

## 3. Add the contents

Claude Code picks these up by convention, so no wiring is needed:

| Directory | Holds |
| --- | --- |
| `skills/<name>/SKILL.md` | A skill, with `name` and `description` frontmatter. |
| `commands/<name>.md` | A slash command, invoked as `/<name>`. |
| `agents/<name>.md` | A subagent definition. |
| `hooks/hooks.json` | Hook configuration. |
| `.mcp.json` | MCP servers the plugin provides. |

## 4. Register it in the marketplace

Add an entry to the `plugins` array in `.claude-plugin/marketplace.json`:

```json
{
  "name": "my-plugin",
  "source": "./plugins/my-plugin",
  "description": "One sentence on what this plugin does.",
  "version": "0.1.0",
  "author": { "name": "DECODE", "url": "https://github.com/decodehq" }
}
```

Keep `version` in sync with the plugin's own manifest.

## 5. Test before pushing

Add your local checkout as a marketplace and install from it:

```bash
claude plugin marketplace add ./
claude plugin install my-plugin@decode
```

## 6. Rolling it out

Enabling a plugin for every new project is a separate change in
`decode-standard-project-template`: add `"my-plugin@decode": true` to
`enabledPlugins` in its `.claude/settings.json`. Existing projects pick up new
plugin versions on their next marketplace update, but do not gain newly added
plugins until their own settings enable them.
