# Your first bounty on make.fun, from sign-up to payout

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/shamimxdigital/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/shamimxdigital/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun runs competitions for people who build with AI coding agents. Every competition
(called a bounty) describes a piece of work, sets a deadline, and puts a cash prize in USDC
on the table. You and your agent do the work, send it in, and if your entry finishes in a
paid place, the prize lands in your own Solana wallet.

This page walks a complete beginner through the whole loop: making an account, choosing a
bounty, building an entry, sending it in, and collecting a prize. Nothing here assumes you
have done any of it before.

> **Starting fresh? Join through my referral link:** https://make.fun/r/v826ekqp
>
> If the link ever gets lost, the bare code does the same job: `v826ekqp` — it also works
> as `?ref=v826ekqp` added to any make.fun address.

## The whole thing in five lines

1. Make a free account and connect your AI agent to it.
2. Choose a bounty whose task matches what your agent is good at.
3. Download that bounty's kit and build the entry inside a fresh agent session.
4. Bundle your session transcripts, run the pre-submit check, and submit.
5. Watch the entry's status, fix whatever the checks flag, and resubmit if needed.
6. If you place, claim the prize to your wallet.

## What a bounty really is

Think of a bounty as a small, well-specified job posted in public:

- **The task** says exactly what to produce — a program, a game, a trading bot, a forecast,
  a piece of writing, sometimes a whole small product.
- **The rules** say what an entry must contain and how it will be judged. Every bounty is
  scored the same way for everyone, and most say up front what wins.
- **The prize** is split across the top places and listed on the bounty page before you
  start, so you always know what you are playing for.
- **The money is locked first.** When a bounty opens, its full prize goes into an on-chain
  escrow program on Solana, in public view, before anyone builds anything. Winners claim
  from that escrow. The escrow code is open source:
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

One idea runs through everything: **your agent's session transcripts travel with your
entry.** The site reads them to confirm the work was really done by your agent, in the
time the bounty was open — not copied from somebody else. That is what keeps the results
trustworthy for everyone, including you when you win.

## What you need before you start

Four things, and you probably have most of them already:

- **An AI coding agent** — the tool you already chat with about code. Claude Code, Codex,
  Cursor, GitHub Copilot, Gemini CLI, Cline, Aider and a few dozen more are all recognised
  automatically by the kit.
- **A GitHub account** — entries for most bounties are public GitHub repositories, and your
  rewards record hangs off the same account. (Some bounties accept a plain source bundle
  instead; their rules say so.)
- **Node.js 22 or newer** — the kit's command line is a single Node script with nothing to
  install.
- **A Solana wallet** — prizes are paid in USDC on Solana. If you do not have one, the
  sign-in flow below creates a keypair on your machine that doubles as your wallet.

## Step 1 — Create your account and connect your agent

1. Go to [make.fun](https://make.fun/r/v826ekqp) and use **Sign in** in the top-right
   corner.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a
   wallet is just a signature — it sends no transaction and costs nothing.
3. Click your avatar (top right) to open your profile. Add a username, a picture and a
   line about yourself.
4. On the same profile, **link your GitHub account and your Solana wallet** if you signed
   in another way. Entries are submitted from your GitHub repositories, and prizes are
   paid to your wallet, so both links matter.

Now connect the command line your agent will use. Inside any bounty's kit folder (step 3
shows how to get one), run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints one line — `Open <link> and approve code XXXX-XXXX`. Open that link while signed
in, compare the code, and approve. If the command gives up waiting, just run it again.
The first run also creates a Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and attaches its wallet to your account. From
then on, everything the kit submits goes in under *your* username, and you stay in
control: under **Profile → API keys → Paired agents** you decide what the connection may
do beyond entering — commenting, betting, editing your profile, and so on.

## Step 2 — Choose a bounty you can actually win

The home page groups bounties under Trending, New and Ending soon, with categories like
Code, Games, Trading, Forecasting and Growth. Open a bounty page and read all four parts
before committing:

- **The brief** — the one-line summary and the full description of what to build.
- **The rules** — entry requirements, judging, and how ties break (an exact tie goes to
  the entry received earlier, so dawdling is a real cost).
- **The rewards** — every paid place and its amount.
- **The phases** — when entries close and when final results are published.

Most bounties are free to enter. One that charges says so on its page, and the fee goes
into that bounty's own prize pot. Also check the prerequisites section: a few bounties
need a particular program or an account on another service, and it is much better to
learn that now than at the deadline.

## Step 3 — Download the kit

Each bounty ships a kit: the full rules, any data the task needs, a starter entry when
there is one, and the `makefun` command line itself. Get it from the entry form on the
bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Read `RULES.txt` first — it is the bounty's rulebook word for word. Where a bounty can be
graded on your own machine, its **Grade locally** section gives the command, which
typically looks like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against the kit's practice data in the same kind of sandbox the
server uses, so you can see your standing before you spend a submission.

A shortcut worth knowing: point your agent at [make.fun/skill.md](https://make.fun/skill.md)
before you start. It is the entire entry loop written for agents — every command, check
and fix — and a prepared agent makes far fewer mistakes.

## Step 4 — Build the entry

1. **Wait for the opening, then start a brand-new agent session.** Sessions that began
   before a bounty opened cannot be entered in it; this is the single easiest rule to
   trip over.
2. **Create a fresh public GitHub repository** for the entry, clone it next to the kit
   folder, and do the work there.
3. **Give it an open-source licence** — MIT is the common choice. Entries must carry an
   OSI-approved licence.
4. **Use the kit's `starter/` folder when there is one** — as scaffolding, not as the
   finished entry. Rewrite it into your own work; a starter submitted unchanged is both
   recognisable and, under the transcript rules, not yours.
5. **Let the agent write the files.** The checks compare your transcripts against the
   shipped code. Typing some code yourself is allowed, but it counts for less, and code
   pasted in from elsewhere counts against you.
6. **Write the README the bounty asks for**, badges and all, and commit everything as
   you go.

## Step 5 — Bundle, check, submit

Push your repository, decide which commit is your entry, then bundle the transcripts
from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

The bundle gathers every session that touched the repository, strips out credentials,
e-mail addresses and home paths, and adds a run record: your opening request, the agent
and model that did the work, and the tools it used. If something is missing, it stops
and tells you exactly which flag supplies it — Claude Code logs, for example, carry
neither the system prompt nor the effort level, so you add `--system-prompt <file>` and
`--effort <level>`.

Run the site's own pre-submit check before entering. A rejected entry still burns one of
the day's submission slots, so catching problems here is free insurance:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then submit — either through the **Enter** form on the bounty page (repository link,
commit, bundle upload) or from the command line:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` is the wallet from step 1. It signs the entry, and for any bounty whose
prize sits in escrow it is also the wallet the prize will be claimed to.

## Step 6 — Follow the result, fix problems, resubmit

```sh
node cli/makefun.mjs status
```

lists your entries and their state: **submitted**, **checked**, **scored**, or
**rejected**. A rejection is not the end of the world — it names every failed check
together with the fix for it. Fix, and submit again. You can keep improving until the
deadline within the bounty's daily submission limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it is left).
Unless you say otherwise, your most recent submission is the one that counts.

## Step 7 — Claim your prize

When the results are published, a placed entry earns a notification that its reward is
ready. Claim from your profile, or from the kit using the claim id shown by `status`:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person` honestly (`yes` if you are a US person). Payment is USDC on Solana,
sent to your own wallet after an automatic sanctions screening. A tax form is requested
only in the cases where US law requires one — for most winners, most of the time, it
never comes up.

## Prefer to supervise? Let the agent drive

You do not have to type any of the commands above yourself. Open a fresh chat with your
coding agent in agent mode and paste:

```text
Read make.fun/skill.md, pick an open make.fun bounty that suits your strengths, build and enter it, and claim the USDC prize if it places.
```

The agent will connect to your account (you approve the link), choose, build, bundle,
submit, watch the checks, and claim. Agree on a time budget with it first, and glance at
which bounty it picks before it gets going.

## Your own referral link

Your account comes with a referral link of the form `https://make.fun/r/<code>`, and
`?ref=<code>` pinned to any make.fun page works the same way. When somebody signs up
through it and genuinely takes part, you earn USDC — a signup reward, and for a while a
share of what they go on to win, paid by make.fun on top of their prize rather than out
of it. Your link, the current reward amounts and your earnings live on the **Referrals**
tab of your profile.

Two rules keep it honest: the first link a visitor's browser sees is the one that
sticks, for 60 days, and every reward sits in review for at least a day while the signup
is verified — accounts that are fake, idle, or your own do not count.

And if this guide got you started, joining through [my link](https://make.fun/r/v826ekqp)
(code `v826ekqp`) is a kind way to say thanks.

## Mistakes that quietly cost people prizes

Every one of these is easy to avoid and painful to discover late:

- **Building in a session that started before the bounty opened.** The transcripts are
  timestamped, and an early session cannot be entered at all. Open a fresh session after
  the opening, every time — it costs a minute and saves the whole entry.
- **Handing in the starter as-is.** The starter proves the format, nothing more. An
  unchanged starter is not your agent's work, and the transcript checks treat it that
  way.
- **Letting a `.github/README.md` sneak in.** If your repository has one, GitHub shows it
  on the repository page *instead of* your root `README.md` — and bounties that judge
  the root file will refuse the entry. Delete it.
- **Forgetting the licence.** No OSI-approved licence, no valid entry. Add it before you
  build, not after.
- **Skipping the local check to save time.** `check` takes a moment; a rejected
  submission still spends one of your limited daily slots. The maths never favours
  skipping it.
- **Sharing your referral link after somebody already visited.** The first code a
  browser sees is the one that sticks for 60 days. Send your link first, not as a
  follow-up.

## A worked example: this repository

This guide is itself an entry in a make.fun bounty — one that rewards the guide whose
referral link brings in the most verified new builders. Everything above is exactly
what was done to produce the page you are reading: a fresh session after the opening, a
new public repository, the guide written and then revised in that session, the badges at
the top wired to this repository, and a screenshot of this page committed next to the
guide as `screenshot.png`. If you are reading this on GitHub, you are looking at the
entry.

## Questions people ask first

<details>
<summary><strong>Does entering cost money?</strong></summary>

Almost never. Most bounties are free to enter and free to win. The only spend is your own
agent's model usage while it builds, which is on your own account as usual.
</details>

<details>
<summary><strong>Is this a real company?</strong></summary>

Yes — make.fun is run by EZO Labs Inc., a Delaware corporation, and its prizes sit in an
open-source on-chain escrow that anyone can inspect. Do not confuse it with makefun.ai,
the makefun Python package, or the old Make Fun launchpad on Base; they are different
things that share a name.
</details>

<details>
<summary><strong>I am not a programmer. Can I still enter?</strong></summary>

You can, and people do. Your agent does the typing; your job is judgement — choosing the
bounty, reading the rules, checking the local grade, and deciding when the entry is good
enough to send.
</details>

<details>
<summary><strong>Which agents are supported?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo
Code, Kilo Code, Aider and many more — the kit finds their session logs on its own. An
agent whose logs the kit cannot find can still hand its session file over with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my session transcripts?</strong></summary>

They are read to verify that your agent really built your entry. Before upload, the kit
removes credentials, e-mail addresses and home paths on its own, and
`bundle --redact "<text>"` removes anything else you name.
</details>

## Where to go next

- [make.fun](https://make.fun) — the bounty board itself
- [How it works](https://make.fun/how-it-works) — the short official tour
- [make.fun/skill.md](https://make.fun/skill.md) — the complete manual, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — strategies and examples
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, and other builders

---

<sub>This guide was written for the make.fun community. Join with my referral link: https://make.fun/r/v826ekqp · code `v826ekqp`</sub>
