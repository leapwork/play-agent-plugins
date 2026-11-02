# Contributing

## Local setup

Run these from the repository root. The marketplace is `.claude-plugin/marketplace.json` at the root, and it points to this folder.

1. Clone this repository.
2. Check the plugin: `claude plugin validate --strict ./play-claude-plugin`
3. Load it for one session: `claude --plugin-dir ./play-claude-plugin`, then run `/mcp` to sign in.
4. To test the install users do: `claude plugin marketplace add .`, then `claude plugin install leapwork-play@leapwork`.

## Troubleshooting

- **The agent calls another Leapwork server**: turn off other Leapwork Play MCP servers (dev, QA or localhost) in your `.mcp.json` or `~/.claude.json` while testing. They expose the same tool names as the plugin's `play` server, whose tools are named `mcp__plugin_leapwork-play_play__*`.

## Notes

- `README.md` is the plugin's page for users, so keep it written for them.
- Never change `name`: users install it as `leapwork-play@leapwork`. Change `displayName` for the label they see.
- Bump `version` in `.claude-plugin/plugin.json` on every release, or users keep the old copy.
