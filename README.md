# Quack Documentation

Official documentation for [Quack](https://quack.build) - the multi-agentic IDE powered by Claude Code.

## Structure

```
quack-docs/
├── 01-getting-started/     # Introduction, installation, first steps
├── 02-core-concepts/       # Agents, droids, skills
├── 03-advanced-techniques/ # Power user features
├── 04-best-practices/      # Workflows and patterns
├── images/                 # Documentation images
└── _meta.json              # Navigation structure
```

## Usage

This repository is used as a Git submodule in:
- **quack-app** - The Tauri desktop application
- **quackagency-website** - The quack.build website

### Adding as Submodule

```bash
git submodule add git@github.com:AleKDev/quack-docs.git docs/guide
git submodule update --init --recursive
```

### Updating Content

1. Make changes in this repo
2. Commit and push
3. In consuming repos, run:
   ```bash
   git submodule update --remote
   git add docs/guide
   git commit -m "Update documentation"
   ```

## License

MIT - Part of the Quack project by C&C Apple Premium Partner.
