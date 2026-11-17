# claude-hooks

A Claude Code plugin marketplace for AnnihilationWizard's hooks. Add it once, then install the hooks you want.

Each hook lives in its own repository, with its own version, changelog and issues. This repository only holds the catalog in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json), so Claude Code fetches each hook from its own repository when you install it.

## Hooks

| Hook | What it does |
| --- | --- |
| [reply-language](https://github.com/AnnihilationWizard/reply-language) | Sends a reply written mostly in English back to Claude to rewrite in Traditional Chinese (Taiwan) |

## Install

In a Claude Code terminal session, add the marketplace once, then install each hook with the **user** scope:

```
/plugin marketplace add AnnihilationWizard/claude-hooks
/plugin install reply-language@claude-hooks
```

On a new machine, these two commands bring the hooks back.

## Update

```bash
claude plugin marketplace update claude-hooks
claude plugin update reply-language@claude-hooks
```

Run `/reload-plugins` in an open session to pick up the new version. A hook's update reaches users only when its `version` in `.claude-plugin/plugin.json` changes.

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

## Project Structure

```text
.claude-plugin/   marketplace.json, the catalog of hooks
README.md         this page
LICENSE           MIT License
```

The hook folders next to these files on the author's machine are separate Git repositories and are ignored by this one.

## License

[MIT License](LICENSE).
