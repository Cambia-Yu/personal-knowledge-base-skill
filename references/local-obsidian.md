# Local Obsidian Target

Do not store a user's real Obsidian path in the distributable skill package.

Use one of these private local configuration locations:

- Environment variable: `PKB_OBSIDIAN_VAULT`
- Local private config:
  - macOS/Linux: `$HOME/.codex/pkb.local.json`
  - Windows: `%USERPROFILE%\.codex\pkb.local.json`

Example `pkb.local.json`:

```json
{
  "obsidianVault": "/Users/you/Documents/YourVault"
}
```

Before writing synchronized notes, verify the configured vault:

```sh
vault="${PKB_OBSIDIAN_VAULT:-$(jq -r '.obsidianVault // empty' "$HOME/.codex/pkb.local.json")}"
test -d "$vault/.obsidian"
```

If the check fails, stop and ask the user for the correct vault path. Do not write to any scanned or recently opened vault as a fallback.
