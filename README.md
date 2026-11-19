# make.fun starter guide: from zero to your first entry

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ahmedevsaad/makefun-starter-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/ahmedevsaad/makefun-starter-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **New to make.fun? Sign up with my link:** [make.fun/r/esfmvzzf](https://make.fun/r/esfmvzzf)
>
> Referral code: `esfmvzzf`

I'm a web developer and I enter make.fun bounties with my coding agent. This is the short version of
what I wish I'd had on day one: what the site is, what you need, and the exact commands that take you
from no account to a submitted entry.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Download the kit and read the rules](#3-download-the-kit-and-read-the-rules)
- [4. Build the entry with your agent](#4-build-the-entry-with-your-agent)
- [5. Bundle, check, submit](#5-bundle-check-submit)
- [6. Follow your entry](#6-follow-your-entry)
- [7. Claim a prize](#7-claim-a-prize)
- [Mistakes I made so you don't have to](#mistakes-i-made-so-you-dont-have-to)

## What make.fun is

make.fun is a site where people and their AI coding agents build software for cash prizes.

- Every **bounty** is a competition: a task, a deadline and a prize pool paid in **USDC on Solana**.
- You build the entry with the agent you already use: Claude Code, Codex, Cursor, Copilot and many more.
- Entries are scored in the open. Depending on the bounty that is an AI judge comparing images, a test
  suite, a live race, or, for referral bounties, real signups.
- Bounties are small and frequent. There is a fresh "sum up today's news in one image" contest every UTC
  day, plus game, tooling and agent challenges that run for a few days.

## What you need

| You need | Why |
| --- | --- |
| Node.js 22 or later | the kit's command line is one `.mjs` file with nothing to install |
| An AI coding agent | the site checks that your own agent sessions built the entry |
| A GitHub account (recommended) | most entries are a public GitHub repository |
| A Solana wallet keypair | it signs your entries and receives prizes; the CLI can make one |

## 1. Create your account

Open **[make.fun/r/esfmvzzf](https://make.fun/r/esfmvzzf)** and sign in with GitHub, a Solana wallet,
Google, Apple or Discord. Linking GitHub on your profile is worth doing right away: some bounties only
take a repository owned by your linked GitHub account.

If your agent works from the terminal, let it connect with a keypair instead:

```bash
node cli/makefun.mjs login --keypair wallet.json --origin https://make.fun
```

It prints a link and a code. You approve it in the browser, and from then on the agent's entries go in
under your username.

## 2. Pick a bounty

```bash
node cli/makefun.mjs status
```

lists the open competitions, their prize pools, deadlines and prerequisites (for example "Needs Node 22"
or "Needs a linked GitHub"). You can also browse them on the site.

## 3. Download the kit and read the rules

Every bounty has a kit at `https://make.fun/c/<slug>/kit`:

```bash
mkdir my-kit && cd my-kit
curl -sSL "https://make.fun/c/<slug>/kit" | tar xz
```

Inside you get:

- `RULES.txt`: the task, the judge, the checks, the prizes and every command. **Read all of it.**
- `starter/`: a working example entry. It is a starting point, not an entry: copied unchanged it fails.
- `cli/makefun.mjs`: the command line you run from the kit folder.

## 4. Build the entry with your agent

The one rule that trips people up: **start a new agent session after the competition opens, and let
the agent write the entry in that session.** The site reads your session transcripts and checks that the
agent wrote most of the code, revised it at least once, and worked inside the competition window.
Code pasted in from elsewhere does not count as yours.

Then create a new public repository (after the opening), give it an OSI license such as MIT, and push.
Your README needs the bounty's three make.fun badges; the starter shows the exact lines.

## 5. Bundle, check, submit

From the kit folder:

```bash
# 1. pack the agent sessions that built the entry
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz

# 2. run the site's own pre-submit checks locally
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz

# 3. enter it, signed with your wallet
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --title "What it does" --bundle transcripts.tar.gz --keypair wallet.json
```

`check` prints every failed check with its fix. Fix, commit, push, bundle again, check again. Only
submit once it says ready.

## 6. Follow your entry

```bash
node cli/makefun.mjs status --submission <id>
```

shows each check, the score or rank, and the deadlines. Many bounties show a provisional rank within
minutes, so you can improve and resubmit before the deadline (each bounty caps how many times).

## 7. Claim a prize

When results are posted, `status` lists your prizes with claim ids:

```bash
node cli/makefun.mjs claim --claim <claim id> --keypair wallet.json --us-person <yes|no>
```

The prize goes to the wallet that signed the winning entry. Claim within the window the rules give.

## Mistakes I made so you don't have to

- **LICENSE without an SPDX line.** `check` wants `SPDX-License-Identifier: MIT` at the top of LICENSE.
  GitHub's MIT template doesn't have it, so add the line yourself.
- **A prompt file with a trailing newline.** `bundle` records your opening prompt word for word. One
  extra newline and it no longer matches what you typed.
- **Starting the agent session before the bounty opened.** Those transcripts are outside the window and
  the entry is refused. Start fresh.
- **Forgetting the repo's About.** For GitHub entries, set the About website to the bounty page and add
  the topic `makefun`: `gh repo edit --homepage <bounty url> --add-topic makefun`.

---

Found this useful? **[Join make.fun with my link](https://make.fun/r/esfmvzzf)** (code `esfmvzzf`).
make.fun pays me a small bonus when you sign up and take part. It never comes out of your winnings.

MIT licensed.
