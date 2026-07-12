# fable.exe Rename Design

## Decision

Rename the public plugin from **fable** to **fable.exe**, spoken “Fable EXE,” and publish the change as version 2.0.0.

Claude Code requires kebab-case identifiers for clean marketplace validation, so the brand and technical identifiers intentionally differ:

- Public brand, repository, and Pages project: `fable.exe`
- Marketplace and plugin identifier: `fable-exe`
- Skill prefix: `fable-exe-`

## Migration contract

All active public surfaces move together: plugin metadata, marketplace metadata, skill directories and frontmatter, cross-skill references, README commands, design-of-record, landing page, social card, GitHub repository metadata, Pages URL, and release notes.

The v1 evaluation prompts and result files remain byte-for-byte historical evidence. Their documentation will explicitly say they evaluated the former `fable-mode` name, now shipped as `fable-exe-mode`.

Because GitHub does not redirect project Pages URLs after a repository rename, every active reference must use `https://uhhexe.github.io/fable.exe/`. GitHub repository links may redirect, but all maintained copy will use `https://github.com/uhhexe/fable.exe` directly.

## User-facing migration

Existing users remove the old `fable@fable` installation and marketplace, add `uhhexe/fable.exe`, then install `fable-exe@fable-exe`. Fresh users only need the final two commands.

## Verification

- Claude plugin validation passes without identifier warnings.
- Six `fable-exe-*` skills are discoverable after a disposable clean install.
- Active docs contain no stale repository, Pages, install, or skill identifiers outside the migration and historical-evaluation notes.
- The landing page renders at desktop and mobile widths with no console errors or horizontal overflow.
- GitHub main, the v2.0.0 tag, and the release point to the same commit.
- The new Pages URL and social card return successfully.
