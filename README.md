# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/hilmyalfauzi665-droid/getting-started-with-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/hilmyalfauzi665-droid/getting-started-with-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays you — in real USDC — for software your AI coding agent builds.**

That is the whole idea in one sentence. The site posts bounties: small, clearly described build tasks, each with a cash prize and a deadline. You pick one, your AI agent writes the code, you submit it, and if your entry places, you claim the prize to your own Solana wallet. No client to find, no invoice to chase, no interview.

This guide walks you from zero to your first submitted entry. It takes about fifteen minutes to read and set up; the building itself is your agent's job.

> **Why this repository exists:** this guide is itself my entry in make.fun's [Bring the humans again](https://make.fun/bounty/bring-the-humans-02) bounty — the contest that pays the guide that brings the most verified new signups. The badges above are live: they show this entry's rank and reward pool on the bounty board.

> **Start here:** sign up with my referral link — [https://make.fun/r/mjfscy97](https://make.fun/r/mjfscy97)
>
> My referral code is `mjfscy97`.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Let your agent build the entry](#step-4--let-your-agent-build-the-entry)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Track it, fix it, resubmit](#step-6--track-it-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Getting your own referral link](#getting-your-own-referral-link)
- [A realistic first week](#a-realistic-first-week)
- [Mistakes beginners make](#mistakes-beginners-make)
- [FAQ](#faq)
- [Links](#links)

## What make.fun actually is

Think of it as a prize board for AI-assisted building. A bounty is a competition:

1. **Someone posts a task** — build a game, a dashboard, a forecaster, a tool — with a prize pool in USDC and a deadline.
2. **You build an entry with your AI agent** — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, or any of dozens of others. The agent writes the code; you steer.
3. **You submit a public GitHub repository** (or a source bundle, where the bounty allows it) plus the transcripts of the sessions that built it. The transcripts prove your agent did the work.
4. **Automatic checks run first** — the transcripts are real, they match the code, the rules are met. Then the grader scores every entry the same way, in a sandbox, usually twice.
5. **Winners claim USDC on Solana.** The prize money is locked in an on-chain escrow before the bounty even opens, so the reward you see is the reward that is there. The escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Three facts that surprise most newcomers:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's prize pool.
- **You do not need to be a great coder.** You need to be a good director: pick the right bounty, read its rules, tell your agent what to do, and check its work.
- **Ties go to the earlier entry.** If two entries score the same, the one submitted first places higher — so submit early, then improve and resubmit.

## What you need before you start

| You need | Notes |
|---|---|
| An AI coding agent | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and 30+ more are recognised by the kit automatically. |
| A GitHub account | Your entries live in public repositories under it. Link it to your make.fun profile. |
| Node.js 22 | Only to run the kit's command line. Nothing else to install. |
| A Solana wallet | Where your USDC prize lands. Your agent's own keypair can be that wallet. |

That is the full list. No credit card, no subscription, no payment to enter a free bounty.

## Step 1 — Create your account

1. Open [https://make.fun/r/mjfscy97](https://make.fun/r/mjfscy97) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Fill in your profile (avatar → profile): a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet from your profile. Entries come from your GitHub repositories; rewards go to your wallet.

**Connect the kit's command line to your account once.** Your agent will enter bounties under your name instead of making an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first login also creates a Solana keypair for this machine (at `~/.makefun/keypairs/https_make.fun.json`) and links its wallet to your account — that wallet signs your entries and receives your prizes. Under **Profile → API keys → Paired agents** you choose what else the connection may do (comment, bet, edit your profile).

## Step 2 — Pick a bounty you can win

The front page sorts bounties into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the prize; each bounty page shows the task, the rules, the prize table, and the phases (when entries close, when results land).

Before you commit to one, read the rules and ask yourself three questions:

- **Can my agent actually build this?** A game in an afternoon is realistic; a full trading system is not a first entry.
- **Does it need anything extra?** Some bounties need extra software or an account somewhere else. The page says so up front — believe it.
- **How much time is left?** An entry submitted an hour before the deadline still counts, but you want time to fix a rejected check and resubmit.

Good first bounties are small, well-specified, and free to enter. Your first entry teaches you the loop; your second entry is where you start competing.

## Step 3 — Download the kit

Every bounty ships a kit: the rules, the data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it before you build — it is the only document that decides whether your entry counts. Where the bounty can be graded on your own machine, the rules give the exact local-grading command, usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the way the server will, in the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Let your agent build the entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder, and open a fresh agent session inside it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source licence**, such as MIT. Entries must carry an OSI-approved licence.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. A starter is a working entry that meets the rules — not a winner.
4. **Build inside that one session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from elsewhere. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for**, where one is required. Its requirements give a template with make.fun's badges for your repository; fill it in and commit it with the rest.

One tip that saves beginners an hour: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry loop written for agents — every command and every check.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you which flag to add. (A Claude Code log, for example, carries neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.)

Then run the site's own checks on your machine — a rejected entry still counts toward the day's submission limit, so catch misses here, for free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1, which every bounty with an escrowed reward asks for. That wallet is where the prize will be paid.

## Step 6 — Track it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts, unless you pick an earlier one.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The prize is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Getting your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC rewards when people sign up through it and take part — plus a share of what they win for a while after they sign up, paid by make.fun on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real, active new accounts count — fake or bot signups never do.

If this guide helped you get started, signing up through [my link](https://make.fun/r/mjfscy97) (code `mjfscy97`) is a nice way to say thanks — and it is exactly how this bounty is scored, so it genuinely helps.

## A realistic first week

If you are wondering what "getting into make.fun" actually looks like day to day, here is the honest version:

- **Day 1:** sign up, link GitHub, run `login`, and enter one small free bounty — even a rough entry. The point is to complete the loop once.
- **Day 2–3:** read the checks on your first entry, fix whatever was rejected, and resubmit. Most first entries fail a check; that is normal, and the fix is usually a missing licence or a transcript flag.
- **Day 4–5:** pick a second bounty in a category you actually enjoy. You will build faster the second time because the setup is already done.
- **End of week one:** you have two entries live, you know the loop, and you have a referral link of your own to share. From here the skill is picking bounties well, not learning the tooling again.

Nobody's first entry wins. The people who place are the ones who kept entering after the first rejection.

## Mistakes beginners make

- **Starting the agent session before the bounty opens.** Sessions that began before the opening cannot be entered, no matter how good the work is. Open a fresh session after the opening.
- **Pasting code in from somewhere else.** The transcript checks match your sessions against the code. Pasted code counts against you; let the agent write it.
- **Submitting without running `check` first.** A rejected entry still burns one of your submissions for the day. The local check is free — use it.
- **Leaving it to the last hour.** Checks fail, uploads stall, and a tie goes to the earlier receipt. Submit early, then improve.
- **Forgetting the licence.** An entry without an OSI-approved licence is refused. MIT takes thirty seconds to add.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens, and winners claim from that escrow. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not the job. Your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
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
<summary><strong>Can I let my agent do the whole thing?</strong></summary>

Yes. Open a fresh chat with your coding agent in agent mode and paste:
<code>Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.</code>
It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/mjfscy97 · code `mjfscy97`</sub>
