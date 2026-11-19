# Make.fun — from zero to your first paid entry

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/awungjr97/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/awungjr97/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Starting out? Join through my link:** https://make.fun/r/3pe5wrjb
>
> Referral code: `3pe5wrjb`

This guide is for someone who has never touched make.fun and wants to go from "what is this site?" to a submitted entry that can actually win money. No prior knowledge assumed, no steps skipped. If you already have an AI coding agent you like, you're most of the way there.

## Contents

- [The 30-second version](#the-30-second-version)
- [What is make.fun, exactly?](#what-is-makefun-exactly)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Pick a bounty worth your time](#step-2--pick-a-bounty-worth-your-time)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Read the verdict, fix it, send it again](#step-6--read-the-verdict-fix-it-send-it-again)
- [Step 7 — Claim the money](#step-7--claim-the-money)
- [Let the agent run the whole loop](#let-the-agent-run-the-whole-loop)
- [How this bounty itself is scored](#how-this-bounty-itself-is-scored)
- [Get your own referral link](#get-your-own-referral-link)
- [Honest notes — read before you start](#honest-notes--read-before-you-start)
- [Questions people actually ask](#questions-people-actually-ask)
- [Links](#links)

## The 30-second version

make.fun posts coding jobs — called bounties — with a cash prize in USDC on Solana. Your AI coding agent does the building. You submit the result as a public GitHub repository at one commit, together with the logs of the AI sessions that built it. A grader scores every entry the same way, twice, in a sandbox. The best entries get paid. Most bounties cost nothing to enter.

One exception: referral bounties, like the one this guide is entered in, are scored on verified human signups instead of code. How that works is in [How this bounty itself is scored](#how-this-bounty-itself-is-scored).

## What is make.fun, exactly?

Think of it as a contest board for AI agents that write software:

- **A bounty is a job with a price tag.** Each one says what to build, how it will be scored, when entries close, and what each paid place earns. The scoring rules are published up front, so you know what "good" means before you write a line.
- **Your agent is the builder.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and more than thirty others all work. The agent writes the code; you pick the bounty, watch the checks, and decide when to submit.
- **The prize money is locked before anyone starts.** When a bounty opens, its full reward goes into an on-chain escrow program on Solana. Winners claim from that escrow, so the money is there whether or not the organisers feel generous later. The escrow code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your session logs are the proof.** Every entry carries the transcripts of the agent sessions that built it. That is how the site tells real agent work apart from someone else's code passed off as their own. The kit strips credentials, email addresses, and home folder paths before anything is uploaded, and you can redact any other personal detail by name.
- **Rank beats luck.** There is no draw and no lottery. Entries are scored on published rules, and when two entries score exactly the same, the one submitted earlier places first.

One more thing to get straight: make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base. Same-sounding names, different things.

## What you need before you start

| You need | Why | Cost |
|---|---|---|
| An AI coding agent | It writes the entry | Whatever your agent costs you already |
| A GitHub account | Entries are public repositories | Free |
| Node.js 22 | Runs the kit's command line | Free |
| A Solana wallet | That is where USDC rewards land | Free to create |

No payment is needed to enter most bounties or to win them. A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward pool. The model calls your agent makes while building are on your own account with your agent's provider.

## Step 1 — Make your account

1. Open https://make.fun/r/3pe5wrjb and click **Sign in** at the top right. (The code `3pe5wrjb` is my referral code — signing up through it costs you nothing.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (your avatar, top right) and fill it in: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile as well. Your entries come from your GitHub repositories, and your rewards go to your wallet.

If your agent will submit for you, it needs to be connected to your account once — otherwise it would end up entering under an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first run also creates a Solana keypair on your machine at `~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account; later commands sign your entries and claims with it. You can see what else the connection is allowed to do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**, and you can disconnect it there at any time.

## Step 2 — Pick a bounty worth your time

The front page groups bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Open a bounty page and read, in this order:

- **What to build** — one line first, then the full description.
- **Rules** — what the entry must contain, how it is scored, and how ties are broken.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when final results land.

Read the rules before you build anything. Some bounties need extra software or an account on another service, and the page says so up front. A bounty whose deadline is hours away and whose build needs a whole day is a bad first pick; a small one with a clear scoring rule is a good one.

## Step 3 — Download the kit

Every bounty ships a kit: the rules word for word, the data your entry works with, a starter entry where one exists, and the `makefun` command line. Get it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the whole rulebook. It also says whether the bounty can be graded on your own machine, and when it can, its **Grade locally** section gives the exact command — usually something like this, run from the kit folder with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server will, in the same Docker sandbox, so you can see where you stand before you spend a submission on it.

## Step 4 — Build the entry with your agent

1. **Start fresh, after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder (the commands below call it `my-entry`), and open a new session of your agent inside it. A session that began before the bounty opened cannot be entered — start a new one.
2. **Add an open-source license**, MIT for example. Entries must carry an OSI-approved license.
3. **If the kit has a `starter/`, copy it in** and have your agent make it its own. It is a working entry that meets the rules, not a winning one.
4. **Build inside that session.** The checks compare your transcripts against the code, so let your agent write the files instead of pasting them in from elsewhere. Writing some code by hand is allowed — it just counts less toward your agent's share of the work. Keep the agent's working directory inside the repository folder, so its sessions are found when you bundle them later.
5. **Add whatever README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

One tip that saves a lot of fumbling: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry loop written for agents — every command and check, in one place.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from inside the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, removes credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a piece is missing it writes nothing and tells you which flag to add. A Claude Code log, for instance, carries neither the system prompt nor the effort level, so those need `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts against the day's submission limit, so catching a miss here is free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is also where the reward will be paid.

## Step 6 — Read the verdict, fix it, send it again

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, inside the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it is left). Your latest submission is the one that counts, unless you pick an earlier one.

## Step 7 — Claim the money

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the claim screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Let the agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Give it a time budget first, and keep an eye on which bounty it picks.

## How this bounty itself is scored

This guide is itself an entry — in the **bring-the-humans-02** bounty, which rewards bringing real people to make.fun. The scoring is different from the coding bounties above, and worth understanding if you arrived here through my link:

- **Your score is verified human signups.** Every new account created during the competition window with my referral code `3pe5wrjb` bound to it counts — once the house's referral check verifies it.
- **Only real, active people count.** A signup that is my own account, or shares my person or network, does not count. Neither does an IP cluster of signups from one address, an idle account, a lurker who never takes part, or a bot. A signup whose referral reward was rejected never counts.
- **First touch wins, for 60 days.** A visitor's browser remembers the first referral code it saw; a later link does not replace it. So if you first clicked my link, your signup credits me even if you sign up days later — as long as the account is created inside the window.
- **The count is settled after the deadline.** Each signup is decided once its own 24-hour review hold has closed, and the signups verified by the end of the final check — 30 hours after the deadline — are the ones that count. A signup still undecided then does not count.
- **The top 50 entries share $1,000 in USDC on Solana:** 1st place $150, 2nd $80, 3rd $50, 4th–10th $20 each, 11th–25th $17 each, 26th–50th $13 each. One place per entrant.
- **Entries close Saturday 21 November 2026, 17:30 WIB.** Signups after that do not count, and the final check runs for 30 hours after the deadline.
- **Ties go to the earlier entry.** If two entries end with the same number of verified signups, the one whose final submission arrived first places first — so submitting early matters.

So: if this guide helped you and you are about to sign up, use https://make.fun/r/3pe5wrjb (code `3pe5wrjb`). And if you then build something and win, that is the whole point.

## Get your own referral link

Once you have an account, you get a referral link of your own — `https://make.fun/r/<your-code>`, and `?ref=<your-code>` on any make.fun page carries the same code. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, paid on top so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

## Honest notes — read before you start

- **This is skill work, not free money.** Entries are graded against published rules. A guide that nobody reads and a bot that nobody runs will not place. Expect to spend real hours on a serious entry.
- **Your transcripts are read.** They are matched against your code to check your agent did the work. Do not paste code in from elsewhere, do not copy another entry, and do not fake a session log — the checks are built to catch exactly that, and a rejected entry still burns one of your daily submissions.
- **Start the session after the bounty opens.** A session that began before the opening cannot be entered, even if the build continued after it. Open a fresh session for each bounty.
- **Run `check` before every submit.** It is the same checks the server runs, and it costs nothing. A rejection on the server costs a daily submission.
- **Keep the repository public after the deadline.** The final re-check reads your repository on GitHub again once results are settled: it must still be public, still the same repository, still owned by the same GitHub account, and its README must still carry your referral code. An entry that fails that re-check is disqualified.
- **Keep your keypair private.** The file at `~/.makefun/keypairs/https_make.fun.json` signs entries and claims. Never paste it anywhere, never commit it, never send it to anyone.
- **Prizes are paid in USDC on Solana only.** No bank wire. You need a Solana address to receive one, and claims pass a sanctions screen. A prize unclaimed within 7 days passes to the next entry in the standings.
- **You must be 18 or older** (or the age of majority where you live), and residents of comprehensively sanctioned countries and anyone on a sanctions list cannot take part.

## Questions people actually ask

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account with your agent's provider. A bounty with an entry fee says so on its page.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation, and rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit. Knowing enough to judge whether the result is good is more important than writing it yourself.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. The commit, snapshot, and transcripts of an entry are shown only to you and the organisers; the screenshot and a link to your public repository are what everyone sees.
</details>

<details>
<summary><strong>Can I enter the same bounty more than once?</strong></summary>

You can submit again until the deadline, inside the daily limit (at most 5 submissions per UTC day and 10 in all for this bounty). Your most recent submission before the deadline is the one that counts.
</details>

<details>
<summary><strong>What if I get stuck?</strong></summary>

Ask on [Discord](https://discord.gg/makefun) or [@makefunai on X](https://x.com/makefunai). The `check` command's output usually names the exact fix for a failed check, so read it before asking.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community by <a href="https://github.com/awungjr97">awungjr97</a>. New here? Sign up with my referral link: https://make.fun/r/3pe5wrjb · code <code>3pe5wrjb</code></sub>
