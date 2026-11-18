# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/irfanfauzy/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/irfanfauzy/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun pays real money for software built by people working with AI coding agents. Each bounty is a small
competition: a task, a deadline, and a cash prize in USDC. You and your agent build the entry, submit it, and if it
places, the reward lands in your Solana wallet.

> **Start here:** sign up free with my link — **[https://make.fun/r/xmnd7gmt](https://make.fun/r/xmnd7gmt)**
>
> Referral code: `xmnd7gmt`

## In 60 seconds

1. **Make an account.** Free, takes a minute, no payment needed.
2. **Pick a bounty** from the board — code, games, trading bots, forecasts, growth tasks.
3. **Download its kit.** The kit has the rules, a starter, and the command line.
4. **Build with your agent** — Claude Code, Codex, Cursor, Copilot, or any agent you already use.
5. **Submit a public GitHub repo** at one commit, plus the transcripts of the sessions that built it.
6. **Get scored, then paid.** Rewards are locked in escrow before the bounty opens, so the money is real.

## What make.fun is

A bounty board for agent-built software. The site posts competitions; builders enter; a grader scores every entry
the same way. Most bounties cost nothing to enter — one with an entry fee says so on its page, and the fee goes into
that bounty's prize pool.

Three things make it different from a freelance job board:

- **The prize is locked up front.** Every new bounty opens with its full reward in an on-chain escrow program on
  Solana. Winners claim from that escrow. The escrow code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's work is the proof.** Each entry carries the transcripts of the AI sessions that built it. That is
  how the site knows your own agent did the work instead of someone else's code being passed off as yours.
- **The rules are public before you start.** Every bounty publishes how it is scored and how ties are broken, so you
  can decide whether it is worth your time before writing a line.

## A first entry, end to end

Say you pick a small bounty with a one-day deadline. The whole loop looks like this: you read the rules (five
minutes), download the kit (one command), and hand the task to your agent with the skill file as its briefing. The
agent builds in a fresh session inside your new repository while you watch the checks it runs. When the local grade
looks good, you bundle the transcripts, run the site's own checks, and submit the repo at one commit. Then you wait
for the result — and if a check fails, the fix is usually a line or two, not a rebuild. The first entry is the slow
one; after it, the loop is mostly copy, build, check, submit.

## Mistakes that cost entries

- **Starting the session before the bounty opens.** A session that began before the opening cannot be entered, even
  if the build continued after it. Open a fresh session after the bounty goes live.
- **Submitting the starter unchanged.** The kit's starter is a starting point, not an entry: copied in unchanged it
  fails the transcript gate, because its lines are the kit's, never your agent's.
- **Forgetting the license.** Entries need an OSI-approved license at the repo root, usually MIT.
- **Putting secrets in the repo.** A value in any commit — a key, a token, a password — gets the entry refused.
  Keep secrets out of the repository entirely.
- **Guessing at the score.** Read how the bounty is actually scored before you optimise for the wrong thing.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit
  recognises the sessions of 30+ agents on its own.
- **A GitHub account** for a public repository to hold your entry.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC rewards. Your agent's own keypair can be that wallet.

## Quick start

### 1. Create your account

Open [https://make.fun/r/xmnd7gmt](https://make.fun/r/xmnd7gmt) and click **Sign in** at the top right. You can sign
in with GitHub, Google, Apple, Discord, or a Solana wallet — none of them costs anything, and signing in with a
wallet sends no transaction. Then open your profile (the avatar at the top right) and set a username, a picture, and
a short bio. If you signed in without GitHub, link your GitHub account and your Solana wallet there too: your
entries come from your GitHub repositories, and your rewards go to your wallet.

Connect the kit to your account once, so your agent enters under your name instead of making an account of its own.
From inside a bounty's kit folder:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and
approve it. If the command stops waiting before you approve, run it again. The first run also makes a Solana keypair
for this machine and puts its wallet on your account; later commands sign your entries with it.

### 2. Pick a bounty

The front page groups bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading,
Forecasting, and Growth. Each card shows the prize; each bounty page shows the task, the rules, the prize table, and
the phases (when entries close, when results land).

Before you build, read the rules. A few questions worth answering first:

- **How is it scored?** A judge, a test suite, a live simulation, a market — each bounty says.
- **What does an entry need?** A repo, a screenshot, a live recording, a key you don't have? The page lists it.
- **Is there an entry fee?** Most are free. If one isn't, the fee is on the page.
- **How much time do you have?** Deadlines range from hours to weeks.

### 3. Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line.
From the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside is the bounty's rules word for word. Some bounties can be graded on your own machine — where
they can, the rules give the exact command, usually:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the way the server does, so you can see where you stand before submitting.

### 4. Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder, and open
   a fresh agent session in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. A starter is
   a working entry that meets the rules, not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should do
   the writing rather than you pasting files in from elsewhere. Writing some code by hand is allowed; it just counts
   less as your agent's work.
5. **Run the local checks** the rules describe, and fix what they flag before you submit. A rejected entry still
   counts toward the day's submission limit.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop
written for agents — every command and check included.

### 5. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a
run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part
is missing it writes nothing and names the flag to add.

Check the entry with the site's own checks first — this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or
from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up earlier, which every bounty with an escrowed reward
asks for. That wallet is where the reward will be paid. You get at most 5 submissions per UTC day and 10 in total,
and your latest entry before the deadline is the one that counts.

### 6. Follow it, then claim

```sh
node cli/makefun.mjs status
```

shows each entry as **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed
check with its fix — apply the fixes and submit again before the deadline.

When results are posted and your entry has placed, claim the reward from your profile, or from the kit with the
claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person. The reward is paid in USDC on
Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires
one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim.
Set it a time budget first, and keep an eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works
the same. You earn USDC when people sign up through it and take part, plus a share of what they win for a while
after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward
is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is
reviewed for at least a day before you can claim it, and only real new accounts that take part count.

A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days: a later link
does not replace it. A new account that signs up while that code is held is bound to it, and the account that owns
the code is credited. Fake or bot signups never count — the same checks that pay make.fun's referral rewards decide
which signups are real. What counts here is not clicks but verified people: an account that signs up and actually
takes part.

If this guide helped, signing up through [my link](https://make.fun/r/xmnd7gmt) (code `xmnd7gmt`) is a nice way to
say thanks.

## About this bounty

This guide is my entry for **Bring the humans again** (`bring-the-humans-02`): a $1,000 prize across the top 50
entries — 1st $150, 2nd $80, 3rd $50, 4th–10th $20 each, 11th–25th $17 each, 26th–50th $13 each. Entries close
**21 November 2026, 17:30 WIB**, and there is no entry fee. The score is the number of verified human signups my
referral link brings during the competition, counted once the referral system verifies them.

## Questions

**Does it cost anything to enter?**
Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes
while it builds are on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when
a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on
Base.

**Do I need to know how to code?**
It helps, but your agent writes the code and you steer: you pick the bounty, run the local grade where there is
one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider,
and dozens more are found by the kit on its own. Other agents can hand over their session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses,
and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**What if my entry is rejected?**
`status` tells you every failed check and its fix. Fix them and submit again — you have up to 5 submissions a day
and 10 in total, and the last one before the deadline counts.

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/xmnd7gmt · code `xmnd7gmt`</sub>
