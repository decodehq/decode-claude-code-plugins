# decode-claude-code-plugins

DECODE's Claude Code plugin marketplace. One repo holding the shared skills,
commands, and agents that DECODE projects install into Claude Code.

Plugins in this marketplace are enabled automatically by
[`decode-standard-project-template`](https://github.com/decodehq/decode-standard-project-template),
so every new DECODE project gets them without manual setup.

## Layout

```
.claude-plugin/marketplace.json   # the marketplace manifest
plugins/
└── decode-standards/             # one directory per plugin
    ├── .claude-plugin/plugin.json
    ├── skills/
    └── commands/
```

## Using it

Projects generated from the standard template already have this marketplace
registered in `.claude/settings.json`, so there is nothing to do.

To add it to an existing project by hand:

```bash
claude plugin marketplace add decodehq/decode-claude-code-plugins
```

Then enable a plugin:

```bash
claude plugin install decode-standards@decode
```

The marketplace is named `decode`, so plugins are referenced as
`<plugin-name>@decode`.

## Available plugins

| Plugin | Description |
| --- | --- |
| `decode-standards` | DECODE engineering standards and conventions. Currently a stub. |

## Adding a plugin

See [CONTRIBUTING.md](CONTRIBUTING.md).
