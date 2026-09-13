# Service Hub workflow

Your organisation's development workflow, served from Service Hub.

At the start of every session this fetches the skills your organisation has
switched on and writes them where Claude Code will find them. What you get
depends on what an administrator has enabled — brainstorming before code, a
failing test first, a debugging method, a definition of done.

Adapted from [Superpowers](https://github.com/obra/superpowers) by Jesse
Vincent, MIT licensed.

## Install

Ask an administrator for a developer token: **Admin → Development workflow →
Developer tokens → New token**. The secret is shown once.

Set both values where your shell will see them:

```bash
export SH_SKILLS_TOKEN=whs_...
export SH_SKILLS_SECRET=sk_...
```

Then add the plugin:

```
/plugin marketplace add Embrace-Technologies-ApS/servicehub-workflow
/plugin install servicehub-workflow
```

Start a new session. The skills are fetched and written on the way in.

## What it does on your machine

Writes `SKILL.md` files into the plugin's own `skills/` directory, cleared and
rewritten each session. Nothing is written anywhere else, and nothing is read
from your repository.

The folder is cleared rather than merged, deliberately: a skill your
organisation switches off has to actually stop applying, and the only way a file
disappears is if something removes it.

## If it does not work

The hook says so in the session rather than failing quietly — a developer who is
told their token is wrong fixes it, whereas one who silently gets no skills has
no idea anything is missing.

| | |
|---|---|
| Not configured | `SH_SKILLS_TOKEN` or `SH_SKILLS_SECRET` is unset |
| HTTP 403 | The token is unknown, revoked, or belongs to an inactive organisation. The message is the same for all three on purpose, so this cannot be used to test whether a token exists. Ask for a new one. |
| No skills returned | Everything is switched off for your organisation |

## Configuration

`SH_SKILLS_URL` overrides the Service Hub address, for a development instance.
Defaults to production.
