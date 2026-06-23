# earl-marketplace

Earl's personal [Claude Code](https://claude.com/claude-code) plugin marketplace.

The marketplace manifest is at `.claude-plugin/marketplace.json`. Each plugin lives in its own
subdirectory and is referenced from the manifest by a relative `source` path.

## Plugins

- **hood-2-coast** — skills for training for and running the Hood To Coast / Portland To Coast
  relay: daily training plans, leg/course lookup, packing, race rules, and team/van logistics.
  Grounded in the bundled 2026 HTC Handbook.

## Using this marketplace

```sh
claude plugin marketplace add /Users/earlespino/projects/marketplace
claude plugin install hood-2-coast@earl-marketplace
```

After editing a plugin, re-sync with `claude plugin marketplace update earl-marketplace` and
restart Claude Code (or run `/reload-plugins`).
