# hadees-cli

## What is this project?

**hadees-cli** (also installed as `hadees`) is a Node.js / TypeScript command-line tool that brings authentic Islamic hadith entries into your terminal, with daily reminders, search, categories, favorites, and a local hadith cache that can sync from a remote source.

## What does it do?

- **Displays a hadith in your terminal** — a daily entry, a random one, or a specific one by id.
- **Searches** the hadith corpus by text and lists **categories** of entries.
- **Tracks favorites** so you can save, list, and remove entries you want to revisit.
- **Runs on shell startup** via a `startup` command you can hook into `.bashrc`, `.zshrc`, or your PowerShell `$PROFILE` to see a hadith every time you open a terminal.
- **Maintains a local cache** of English hadith data and can **scrape / sync** the full cache from a remote source, falling back to seed hadiths when offline.
- **Supports machine-readable output** with `-j/--json` and compact output with `-p/--plain` on most content commands.

## Requirements

- Node.js `>=18`
- npm

## Installation

```bash
# one-off run
npx hadees-cli startup

# global install
npm install -g hadees-cli
```

Installed binaries:
- `hadees-cli`
- `hadees`

## Usage

```bash
# default command (same as "daily")
hadees-cli

# show today's entry
hadees-cli daily

# random entry
hadees-cli random

# search text
hadees-cli search "patience"

# list categories
hadees-cli category --list

# show entries for a category
hadees-cli category --category daily

# show specific entry by id
hadees-cli show morning-1

# favorites
hadees-cli favorites --add morning-1
hadees-cli favorites --list
hadees-cli favorites --remove morning-1

# show startup hadith now
hadees-cli startup

# show one random hadith on demand (without startup hooks)
hadees-cli hadith-now

# scrape full english hadith cache
hadees-cli scrape-hadith
```

Most content commands support:
- `-j, --json` for JSON output
- `-p, --plain` for compact output

## Auto-show Hadith On Terminal Open

The npm package does not edit your shell profile automatically.
Configure it once in your shell startup file.

### Bash (Linux/macOS)

Add to `~/.bashrc`:

```bash
hadees-cli startup 2>/dev/null || true
```

Reload:

```bash
source ~/.bashrc
```

### Zsh (Linux/macOS)

Add to `~/.zshrc`:

```bash
hadees-cli startup 2>/dev/null || true
```

Reload:

```bash
source ~/.zshrc
```

### PowerShell (Windows)

Open profile:

```powershell
notepad $PROFILE
```

Add:

```powershell
hadees-cli startup 2>$null
```

Restart PowerShell.

## Cache and Config

- `startup` and `hadith-now` read from local hadith cache.
- If cache is missing/stale, it tries to sync from remote source.
- If sync fails (offline/network issue), it falls back to seed hadiths.

Environment variable:
- `HADEES_CLI_CONFIG_DIR` - custom directory for config and hadith cache.

## License

MIT
