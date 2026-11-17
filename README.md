# claude-hooks

<p align="center">
  <img src="docs/images/icon.svg" width="96" height="96" alt="claude-hooks icon: a hook hanging from a ring">
</p>

<p align="center">
  <strong>One place for every AnnihilationWizard hook.</strong><br>
  A Claude Code plugin marketplace: add it once, then install the hooks you want.
</p>

<p align="center">
  <a href="#hooks"><img src="https://img.shields.io/badge/Hooks-1-green.svg" alt="1 hook"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="MIT License"></a>
  <a href=".claude-plugin/marketplace.json"><img src="https://img.shields.io/badge/Type-Plugin%20marketplace-6E7681.svg" alt="Plugin marketplace"></a>
</p>

<p align="center">
  <a href="#hooks">Hooks</a> ·
  <a href="#install">Install</a> ·
  <a href="#update">Update</a> ·
  <a href="#adding-a-hook">Adding a hook</a> ·
  <a href="#project-structure">Project structure</a>
</p>

Each hook lives in its own repository, with its own version, changelog and issues. This repository only holds the catalog in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json), so Claude Code fetches each hook from its own repository when you install it. You can install, update or turn off each hook on its own, and on a new machine two commands bring them back.

## Hooks

| Hook | What it does |
| --- | --- |
| <img src="https://raw.githubusercontent.com/AnnihilationWizard/reply-language/main/docs/images/icon.svg" width="20" height="20" alt=""> [reply-language](https://github.com/AnnihilationWizard/reply-language) | Sends a reply written mostly in English back to Claude to rewrite in Traditional Chinese |

### reply-language

**Replies stay in Traditional Chinese.** When Claude ends a turn with a reply written mostly in English, the Stop hook sends it back once to rewrite in Traditional Chinese with Taiwan terminology, keeping code, commands, paths and identifiers as they are. Only the final reply counts, so English status lines between tool calls do not trigger it, and code, URLs and paths are not counted as English.

![Side-by-side Claude Code session: on the left Claude ends the turn with an English reply to a Chinese request; on the right the Stop hook sends that reply back and Claude rewrites the same reply in Traditional Chinese](https://raw.githubusercontent.com/AnnihilationWizard/reply-language/main/docs/images/preview.svg)

## Install

In a Claude Code **terminal** session, add the marketplace once:

```
/plugin marketplace add AnnihilationWizard/claude-hooks
```

Then install the hooks you want:

```
/plugin install reply-language@claude-hooks
```

1. Choose a scope for each hook. The **user** scope runs the hook in every session.
2. Claude Code confirms `Plugin is now active.` No restart is needed.

<details>
<summary>Add the marketplace and install in one step</summary>

```
/plugin install reply-language --marketplace AnnihilationWizard/claude-hooks
```

Answer `y` to add the `github:AnnihilationWizard/claude-hooks` marketplace.

</details>

> [!TIP]
> If a hook's script is also registered in `~/.claude/settings.json`, or loaded with `--plugin-dir` or `CLAUDE_CODE_PLUGIN_DIRS`, remove it from there after installing it here, or it runs twice.

## Update

Refresh the catalog, then update a hook:

```bash
claude plugin marketplace update claude-hooks
claude plugin update reply-language@claude-hooks
```

Run `/reload-plugins` in an open session to pick up the new version. You can also choose **Update now** in the `/plugin` **Installed** tab.

To update automatically, open `/plugin` > **Marketplaces** and enable auto-update for `claude-hooks`. Auto-update is off by default for marketplaces other than the official ones.

## Adding a hook

1. Publish the hook in its own repository with a `.claude-plugin/plugin.json` and a `hooks/hooks.json`.
2. Add an entry to `plugins` in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json):

   ```json
   {
     "name": "my-hook",
     "description": "What the hook does, in one line",
     "source": { "source": "url", "url": "https://github.com/AnnihilationWizard/my-hook.git" }
   }
   ```

3. Add the hook's folder to `.gitignore`, check the catalog, then push:

   ```bash
   claude plugin validate --strict .
   ```

A hook's update reaches users only when its `version` in `.claude-plugin/plugin.json` changes, so bump it with each release. Updating a hook does not need a change here.

## Project Structure

```text
.claude-plugin/   marketplace.json, the catalog of hooks
docs/images/      README icon
README.md         this page
LICENSE           MIT License
```

The hook folders next to these files on the author's machine are separate Git repositories and are ignored by this one.

## License

[MIT License](LICENSE). Copyright © 2026 [AnnihilationWizard](https://github.com/AnnihilationWizard).
