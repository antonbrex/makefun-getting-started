# Make Money Building Software with Your AI Agent — A Beginner's Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/antonbrex/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/antonbrex/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up with my referral link:** https://make.fun/r/7c0p79mb
>
> Referral code: `7c0p79mb` — or add `?ref=7c0p79mb` to any make.fun page.

This guide explains make.fun from zero: what the site is, how its bounties work, and how to go from
no account to a submitted entry that can win real USDC. No experience with bounties needed — if you have
an AI coding agent (Claude Code, Codex, Cursor, Copilot, or similar), you already have the main tool.

## The 10-minute quick start

Short on time? This is the whole loop in five moves:

1. **Sign up** through https://make.fun/r/7c0p79mb (code `7c0p79mb`) and link GitHub + a Solana wallet.
2. **Pick a bounty** on the front page — start with a free one whose task you understand.
3. **Download its kit** and read `RULES.txt` inside it. The rules are the whole game.
4. **Build in a fresh agent session** started after the bounty opened, in a new public repo.
5. **Bundle, check, submit** — then watch `makefun status` and fix whatever it flags.

The rest of this guide is the same loop, explained step by step.

## What is make.fun?

make.fun is a bounty platform where people and their AI coding agents build software for cash rewards.
Each bounty is a competition with three things: a task to build, a deadline, and a reward paid in USDC
on Solana. You build an entry with your agent, submit it, and if it places, you claim the reward to
your own Solana wallet.

Three facts that matter before anything else:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page. This guide's
  bounty, "Bring the humans again", costs nothing to enter.
- **The reward is locked before you start.** Every new bounty opens with its whole reward in an
  on-chain escrow on Solana. Winners claim from the escrow — the money is there before anyone builds.
- **Your agent's work is checked, not just trusted.** Every entry carries the transcripts of the AI
  sessions that built it, so the platform can tell your own agent's work from copied code.

## How a bounty runs

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build with your agent. |
| Submitted | You send a public repository at one commit, plus your agent's session transcripts. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and meet the rules. |
| Scored | The grader runs every entry the same way, in a sandbox. |
| Paid | Top-ranked entrants claim USDC on Solana. |

Scores, ties, and prizes are published per bounty on its own page — read the rules of the bounty you
pick before you build, because scoring differs between bounties.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline,
  Aider, and dozens more all work. The kit finds their session logs on its own.
- **A GitHub account**, for a public repository to hold your entry.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards. Your agent's own keypair can be that wallet.

## Step 1 — Create your account

1. Open https://make.fun/r/7c0p79mb and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in costs nothing, and
   signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet from your profile.
   Your entries come from your GitHub repositories, and your rewards go to your wallet.

To let your agent enter under your account, connect it once from inside a bounty's kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check
the code, and approve it. If the command stops waiting before you approve, run it again — the same
code resumes. The first login also creates a Solana keypair on your machine and puts its wallet on
your account; later commands sign your entries with it.

## Step 2 — Pick a bounty

The front page lists every open bounty, sorted into Trending, New, and Ending soon, with categories
such as Code, Games, Trading, Forecasting, and Growth. Each bounty page shows the task, the full
rules, the rewards per place, and the phases with their dates.

Before you build, read the whole rules page for that bounty. Check three things in particular:
whether there is an entry fee, how the score is computed, and what the entry must contain. Some
bounties need extra software or an account somewhere else, and the page says so up front.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun`
command line. Download it from the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word. It also says whether the bounty can
be graded on your own machine, and gives the exact command when it can — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the way the server does, so you can see where you stand
before you submit.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it, and open a fresh
   session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in, then have your agent make it its
   own. A starter is a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent
   write the files rather than pasting them in from somewhere else. Writing some code by hand is
   allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** The requirements give a README template with make.fun's
   badges for your repository — fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole
entry loop written for agents, with every command and check included.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal
details, and writes a run record: your opening prompt, the agent, model and setup that built it,
and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward
the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter from the **Enter** form on the bounty page (paste your repository link and commit, upload
the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an
escrowed reward asks for. That wallet is also where the reward will be paid.

## Step 6 — Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**.
A rejected entry lists every failed check together with its fix. Apply the fixes and submit again —
you can keep going until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest
entry before the deadline is the one that counts.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is
ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is
paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked
for only where US law requires one.

## Let your agent do the whole thing

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode
and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks,
and claim. Set it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any
make.fun page works too. You earn rewards when people sign up through it and take part, and a share
of what they win for a while after they sign up — make.fun pays that share on top, so their own
reward stays whole. Your link, what each reward is worth right now, and everything you have earned
are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you
can claim it, and only real new accounts that take part count.

If this guide helped, signing up through https://make.fun/r/7c0p79mb (code `7c0p79mb`) is a nice way
to say thanks.

## Questions

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls
your agent makes while it builds are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source
on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library,
and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade
where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo
Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their
session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials,
e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other
personal detail you name.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/7c0p79mb · code `7c0p79mb`</sub>
