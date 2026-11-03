# Contributing

This plugin uses the [Agent Plugins 1.0](https://agent-plugins.org/) format: `plugin.json` and `mcp.json` at the root. Codex-only settings, such as the display name and logo, are under `extensions.com.openai` in `plugin.json`.

## Local setup

1. Clone this repository.
2. Get the `codex` CLI. Either install it with `npm install -g @openai/codex`, or use the one that ships with the ChatGPT desktop app at `%LOCALAPPDATA%\OpenAI\Codex\bin\<build>\codex.exe` on Windows. Open a new terminal afterwards so `codex` is on your `PATH`.
3. Add the repository root as a local marketplace, using its absolute path. Its `.agents/plugins/marketplace.json` points to this folder:

   ```bash
   codex plugin marketplace add /path/to/play-agent-plugins
   codex plugin marketplace list
   ```

   The list shows `leapwork` with the repository as its root.
4. Install the plugin. Run `codex plugin add leapwork-play@leapwork`, or click **+** next to **leapwork-play** in the app's **Plugins** directory. The command prints the installed plugin root under `~/.codex/plugins/cache/leapwork/leapwork-play/`.
5. Sign in to the plugin's MCP server: `codex mcp login play`. Then run `codex mcp list` and check that `play` (`https://mcp.leapwork.ai/mcp`) is `enabled` with auth `OAuth`.
6. Turn off any other Leapwork Play MCP servers in `~/.codex/config.toml` (for example dev, QA or localhost ones) by setting `enabled = false` under their `[mcp_servers.<name>]` entries. They expose the same tool names and descriptions as `play`, so the agent picks one of them instead of the plugin's.
7. Restart the ChatGPT desktop app and start a **new** Codex session, since sessions that were already open keep their old tools. Run `/plugins` to check that Leapwork Play is enabled, then ask `@Leapwork Play create a test case named Login smoke`.

To try a change, reinstall, since Codex runs the cached copy and not your working tree:

```bash
codex plugin remove leapwork-play@leapwork
codex plugin add leapwork-play@leapwork
```

## Troubleshooting

- **"Failed to install plugin"**: check that the plugin's `source` in the repository root's `.agents/plugins/marketplace.json` is `{ "source": "local", "path": "./play-codex-plugin" }`. A `url` source makes Codex clone that repository, which fails when it is private or does not exist yet.
- **The agent calls another Leapwork server**: see step 6. The session log in `~/.codex/sessions/` shows which server each call went to, under `"invocation":{"server":...}`.
- **`play` shows `Not logged in`**: run `codex mcp login play` again.

## Notes

- `README.md` is the plugin's page for users, so keep it written for them.
- Keep the marketplace source local and relative to the repository root (`./play-codex-plugin`). It works both from a local folder and when users add the marketplace from GitHub, which is how OpenAI's own marketplaces list their plugins.
- Paths under `extensions.com.openai` start with `./` and stay inside the repository.
- To publish to the public plugin directory that ChatGPT and Codex share, use OpenAI's [plugin submission flow](https://developers.openai.com/plugins/deploy/submission).
