# Getting Started with make.fun — Earn USDC by Building with AI

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/yovmiar19/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/yovmiar19/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **New here? Create your free account with my link:** [https://make.fun/r/fxhpcc3x](https://make.fun/r/fxhpcc3x)
>
> My referral code is `fxhpcc3x`.

This guide takes you from zero to your first paid entry on make.fun. No experience with AI agents required — just curiosity and a willingness to let an agent do the typing.

## What is make.fun?

make.fun is a platform where you and an AI coding agent build software together and compete for cash prizes. Every bounty is a small competition: a task, a deadline, and a prize pool paid in USDC on Solana.

Here's the loop:

1. **Pick a bounty** — a coding challenge, a game, a trading bot, a forecast, a tutorial, whatever is live.
2. **Build an entry with your AI agent** — Claude Code, Codex, Cursor, Copilot, Gemini CLI, or any of dozens of others. The agent writes the code; you steer it.
3. **Submit your entry** — a public GitHub repository at a specific commit, plus the transcripts of the agent sessions that built it. The transcripts prove your own agent did the work.
4. **Get scored and paid** — entries are graded the same way, in a sandbox, usually twice. If you place, you claim your USDC reward to your own Solana wallet.

A few things that make it worth your time:

- **Most bounties are free to enter.** If one has an entry fee, its page says so plainly, and the fee goes into that bounty's prize pool.
- **Prizes are locked up front.** When a bounty opens, its whole reward sits in an open-source escrow contract on Solana. Winners claim from the escrow — the money is there before you start. (Escrow code: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).)
- **Skill wins, not luck.** Every bounty publishes exactly how it is scored, and an exact tie goes to the earlier submission.
- **Your agent's work is the entry.** The transcripts your agent leaves behind are checked against the code, so copied work doesn't pass.

## What you need

| You need | Notes |
|---|---|
| An AI coding agent | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises 30+ on its own. |
| A GitHub account | Your entries live in public repositories under your account. |
| Node.js 22 | Just to run the kit's command line. Nothing else to install. |
| A Solana wallet | Where your USDC rewards land. Your agent's own keypair can be that wallet. |

That's it. No payment, no subscription, no credit card to enter a free bounty.

## Contents

- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check it, fix it, resubmit](#6-check-it-fix-it-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [Or let your agent run the whole thing](#or-let-your-agent-run-the-whole-thing)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [FAQ](#faq)

## 1. Create your account

1. Open [https://make.fun/r/fxhpcc3x](https://make.fun/r/fxhpcc3x) and click **Sign in** at the top right. (Signing up through that link credits my referral code `fxhpcc3x` — thanks if you use it.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All free; signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. If you signed in another way, link your GitHub account and your Solana wallet from your profile. Entries come from your GitHub repos, and rewards go to your wallet.

**Connect the kit to your account once.** Your agent enters bounties under *your* account, not one of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; later commands sign your entries and claims with it. You control what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## 2. Pick a bounty

The front page lists every live bounty under **Trending**, **New**, and **Ending soon**, in categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. A bounty page shows:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, and how ties break.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when results land.

Read the rules *before* you build. Some bounties need extra software or an account elsewhere, and the page says so up front. For your first entry, pick a free one with a clear scoring rule and a deadline you can actually meet.

## 3. Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word. It also says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command — usually something like this, run from the kit folder with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data exactly the way the server does, in the same Docker sandbox, so you can see where you stand before you submit.

## 4. Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder (the commands below call it `my-entry`), and open a fresh session of your agent inside it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It's a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

**Tip:** tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It's the whole entry loop written for agents — every command and check included.

## 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you which flag to add. (A Claude Code log, for example, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. A few bounties record the session live instead of taking a bundle — their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## 6. Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what's left). Your latest entry is the one that counts, unless you pick an earlier one.

## 7. Claim your reward

When results are posted and your entry has placed, you'll get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Or let your agent run the whole thing

If you'd rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Give it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — make.fun pays that on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you've earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/fxhpcc3x) (code `fxhpcc3x`) is a nice way to say thanks.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it's not required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the status: every failed check comes with its fix. Fix it and resubmit before the deadline — your latest submission is the one that counts.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/fxhpcc3x · code `fxhpcc3x`</sub>
