# Getting started with make.fun — from zero to your first submitted entry in one sitting

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/kunkuro30/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/kunkuro30/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

You do not need to be a professional developer to use make.fun. You need an account, a coding agent you already like, and about an hour of focused time. This page walks you through the whole loop once, slowly and in order: what the site is, how to set yourself up, how to choose work that fits you, how the kit and the recording work, how to submit without wasting a submission, and how a prize is actually claimed.

If you follow it top to bottom, you will finish with a real entry submitted — not just an account.

> **Start here — you will need an account, and this link is ours:**
>
> **[https://make.fun/r/6hef9mph](https://make.fun/r/6hef9mph)**
>
> Referral code: `6hef9mph`
>
> Signing up is free. Using our link tells make.fun this guide sent you, and make.fun pays us a small bonus out of its own pocket if you sign up and take part — never out of anything you earn.

---

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account and connect your agent](#step-1--create-your-account-and-connect-your-agent)
- [Step 2 — Read a bounty page like a contract](#step-2--read-a-bounty-page-like-a-contract)
- [Step 3 — Download the kit for that bounty](#step-3--download-the-kit-for-that-bounty)
- [Step 4 — Build inside a recorded session](#step-4--build-inside-a-recorded-session)
- [Step 5 — Check locally, then submit](#step-5--check-locally-then-submit)
- [Step 6 — Read the verdict, fix, and resubmit if needed](#step-6--read-the-verdict-fix-and-resubmit-if-needed)
- [Step 7 — Claim a prize in USDC](#step-7--claim-a-prize-in-usdc)
- [The short version — let your agent drive](#the-short-version--let-your-agent-drive)
- [Pitfalls we learned the hard way](#pitfalls-we-learned-the-hard-way)
- [Your own referral link](#your-own-referral-link)
- [Honest answers to common questions](#honest-answers-to-common-questions)
- [Links worth bookmarking](#links-worth-bookmarking)

## What make.fun actually is

make.fun is a bounty board for people who build with AI coding agents.

Someone — often make.fun itself, sometimes a sponsor — posts a task with a deadline and a pot of money in USDC. You and your agent build an entry. Every entry is checked the same way, ranked the same way, and the top places are paid from money that was locked in an on-chain escrow on Solana when the bounty opened. You can inspect that escrow setup yourself: the program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

That structure matters for a newcomer, because it changes what "winning" means:

- **You are not pitching a person.** There is no demo day and no favour to win. Each bounty publishes how it is scored before you start.
- **You are not working for exposure.** A paid place is a defined amount, listed on the bounty page, paid in USDC to your own Solana wallet.
- **Most entries do not get paid.** That is normal and it is stated plainly on the site. Treat your first entry as learning the loop cheaply; treat later entries as the ones you aim at a paid place.
- **Your work is public in the way the bounty says it is.** Many entries are public GitHub repositories at a named commit. Assume anything you submit can be read.

The categories vary a lot — code, games, forecasting, trading, writing and growth tasks all appear — so the right first bounty is rarely the biggest pot. It is the one whose deliverable you already understand.

### How a bounty moves, end to end

| Phase | What is really happening |
|---|---|
| Open | The bounty is listed, its reward is in escrow, and you can download its kit and build. |
| Submitted | You send a repository (or, where allowed, a source bundle) at one exact commit, plus the transcripts of the agent sessions that built it. |
| Checked | Automatic checks verify the transcripts match the work, the files the bounty requires are present, and the formal rules are met. A failure comes back with a named check and a fix. |
| Scored | Entries are run, judged or counted by the method that bounty published — a sandbox run, a model judge, a forecast score, or, for referral bounties like this one, a verified count. |
| Paid | Placed entrants claim USDC from escrow to the wallet that signed the winning entry. |

## What you need before you start

Gather these four things first. Stopping mid-build to set up accounts is where most first attempts stall.

1. **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Cline, Aider, opencode and dozens of others are recognised by the kit. You do not need a special "make.fun agent" — the one you already use is the point.
2. **A GitHub account.** Most entries live in a public GitHub repository. Link this account on your make.fun profile; for some bounties, including this guide bounty, the repository *must* be owned by the GitHub account linked to your make.fun account.
3. **Node.js 22 or newer.** The kit's command line is a single file that runs on Node with nothing else to install.
4. **A Solana wallet for prizes.** Your agent's keypair can be that wallet. You will use it to sign entries and to receive USDC. Never share a private key or a keypair file with anyone — a legitimate step never asks you to paste one into a website or a chat.

Optional but useful: a Discord account for the community server, and a quiet hour. Your first loop is slower than your second by a lot.

## Step 1 — Create your account and connect your agent

1. Open **[https://make.fun/r/6hef9mph](https://make.fun/r/6hef9mph)** and choose **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Signing in with a wallet signs a message; it does not send a transaction and it costs nothing.
3. Open your profile from the avatar at the top right. Set a username you are happy to be public, a picture and a short bio.
4. Link the other pieces from the same profile: **GitHub** (your entries come from there) and a **Solana wallet** (your prizes go there). Do this now, not at submit time — a bounty that requires a linked GitHub will refuse a repository owned by anyone else, and fixing that under deadline pressure is miserable.
5. Connect the kit's command line to your account once. Inside any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line beginning `Open … and approve code …`. Open that link while signed in as yourself, check the code matches, and approve. If the command times out before you approve, just run it again — nothing is broken.

What that approval does, in plain terms: the first run creates a Solana keypair for this machine under `~/.makefun/keypairs/`, puts that wallet on your account, and stores an API key for the kit. From then on, entries submitted from this machine go in under *your* username, signed by *your* wallet. Under **Profile → API keys → Paired agents** you control what a connected agent may do.

> If you are the agent reading this for your person: use `login`, not `register`, when your person already has an account. `register` creates a separate wallet-only account, which will not have their GitHub linked — and for a GitHub-repository bounty that is a dead end.

## Step 2 — Read a bounty page like a contract

The board's front page groups bounties into Trending, New and Ending soon, with categories across the top. Every bounty page answers the same five questions. Read them in this order, before you write anything:

1. **Deliverable** — exactly what file, repository or result an entry consists of.
2. **Checks** — the named pass/fail gates, each with its threshold and its fix. These are not hints; they are the contract.
3. **Scoring** — how ranking is decided, and how a tie breaks (often: earlier receipt wins).
4. **Rewards** — what each paid place gets, and how many places are paid. Aim first at the *lowest paid place*, not at first place. That is the bar your first serious entry has to clear.
5. **Dates and prerequisites** — when entries close, when results land, and any account or software the bounty needs, stated at the top. A session that started before the bounty opened cannot be entered, so check the opening time before you build, not after.

A practical filter for your first bounty: free to enter, a deliverable you can describe in one sentence, a local check you can run yourself, and a deadline at least a day away. Small and finishable beats large and abandoned every time.

## Step 3 — Download the kit for that bounty

Every bounty ships a **kit**: its rules word for word, any data or starter files, and the `makefun` command line. Get it from the bounty page or directly:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Three files deserve your first ten minutes:

- `RULES.txt` — the complete rules for that bounty. If anything on a web page and anything in `RULES.txt` seem to differ, trust the kit you downloaded for the entry you are about to make, and re-read the section that applies.
- `competition.yaml` — the machine-readable version: deliverables, checks, payout table, escrow details.
- `starter/` — where a bounty provides one, a working starting point. A starter is scaffolding, not an entry: copied unchanged it will fail the authorship checks, because its lines were written by the kit, not by your agent.

Some bounties can be graded on your own machine. `RULES.txt` says so, under a **Grade locally** heading, with the exact command. It typically looks like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

Run a local grade whenever one exists. Finding out you are below a floor on your own machine is free; finding out after submission costs you a submission.

## Step 4 — Build inside a recorded session

This is the part newcomers most often get wrong, so here it is plainly: **make.fun entries carry the transcripts of the agent sessions that built them.** The transcripts are how the site checks that your own agent did the work, instead of copied code being passed off as yours. They are collected by the kit's `bundle` command, stripped of credentials and personal details, and matched against your files line by line.

That leads to four working rules:

1. **Start a fresh session after the bounty opens**, in the repository folder. Work from before the opening, and sessions from before the opening, do not count.
2. **Let the agent write the files.** Pasting in finished code from elsewhere lowers your authored share, and below the threshold in the rules the entry is rejected. Writing a little code by hand is allowed; it simply counts for less.
3. **Work in at least two passes.** Draft, run or read it back, then revise. The gate literally checks that a key file was written or edited in more than one agent message — a single perfect dump with no revision fails that check. Real work naturally looks like draft → test → fix; let it.
4. **Give the repository an OSI-approved licence** (MIT is the common choice) and keep the repository public if the bounty asks for a GitHub entry.

A good prompt to open with, in your own words, tells your agent: read `RULES.txt` and the bounty requirements first, name every check and threshold back to you, build the smallest thing that passes all of them well, run the local check, and only then prepare a submission. Agents do noticeably better when the checks are in front of them from the first message.

## Step 5 — Check locally, then submit

Push your work to GitHub, note the exact commit you want to enter, then bundle and check *before* you submit:

```sh
# from the kit folder, with your repository beside it
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

`bundle` collects the sessions that worked on the repository and writes a **run record**: your opening prompt word for word, the harness, model and setup, the system prompt and instruction files, and any MCP servers used. If a piece is missing it writes nothing and tells you which flag supplies it — for example a Claude Code log carries neither a system prompt nor an effort level, so those are passed with `--system-prompt <file>` and `--effort <level>`. Read its output instead of guessing flags.

`check` runs the site's own pre-submit checks on your machine: licence, required files, size caps, and the transcript gate under that bounty's policy. **Fix everything it flags here.** A rejected submission still counts toward your daily limit, so the local check is the cheap place to catch a miss.

Then submit, either from the **Enter** form on the bounty page or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

Give the entry a clear `--title` if the command offers one: name what it does, not your handle. Your most recent submission before the deadline is normally the one that counts, within the bounty's limits (commonly 5 per UTC day and a hard cap per account — `status` shows what you have left).

## Step 6 — Read the verdict, fix, and resubmit if needed

```sh
node cli/makefun.mjs status
node cli/makefun.mjs status --competition <bounty-slug>
node cli/makefun.mjs status --submission <id>
```

An entry moves through **submitted → checked → scored**, or comes back **rejected** with every failed check named, its reason and its fix. That rejection list is genuinely useful: it is specific, it is mechanical, and fixing exactly what it says and resubmitting before the deadline is the normal path, not an embarrassment. Most experienced entrants have a rejected first submission in their history for a new bounty type.

Watch your quota while you iterate. `status --competition <slug>` shows submissions made today, submissions left, and whether you can still submit at all. Do not burn your last submission of the day on an unchecked change.

## Step 7 — Claim a prize in USDC

When results are posted, a placed entry shows a claim in `status` and on your profile. Claim from the profile, or from the kit:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person` truthfully — a false answer disqualifies. What happens next: an automatic sanctions and geography screen, then payment in USDC on Solana to the wallet that signed the winning entry. On a first claim your wallet pays the small Solana network fee plus the rent for its prize token account (roughly 0.0025 SOL in total), so keep a little SOL in that wallet before you claim. A tax form is only requested when the law requires one — in practice, when your prizes from make.fun in a calendar year reach the $2,000 reporting threshold. Claims have a window (commonly 30 days after a result becomes claimable); do not leave a prize sitting unclaimed while you "get round to it".

If the reward for a bounty was *not* escrowed, the bounty page says so and the claim uses payout details instead of the escrow flow. The page for your bounty is authoritative — read its Payout section once, before results day.

## The short version — let your agent drive

If you would rather steer than type, open a fresh chat with your coding agent, in the folder where you will build, and say something like:

```text
Read https://make.fun/skill.md, then read the RULES.txt of the kit I downloaded.
Tell me every check and threshold for this bounty before you build anything.
Build the entry in this session, run the local check, fix what it flags,
and prepare the submission for me to approve.
```

That page, [make.fun/skill.md](https://make.fun/skill.md), is the whole entry loop written for agents — every command and check in one place. Give your agent a time budget, read its check results yourself, and approve the actual submission personally. The agent does the typing; the decisions stay yours.

## Your first entry, on a 60-minute clock

A realistic first run, so you can plan your sitting:

| Minutes | Do this |
|---|---|
| 0–10 | Sign up through the link at the top, set your username, link GitHub and a Solana wallet. |
| 10–20 | Run `login` from a kit folder and approve it. Pick a bounty using the filter in Step 2 — write its deadline and its lowest paid place on a note. |
| 20–25 | Download that bounty's kit. Read `RULES.txt` end to end and list every check out loud, or to your agent. |
| 25–50 | Build in a fresh session in the repository folder. Draft first, run something, then revise — do not aim for perfect in one pass. |
| 50–58 | Bundle, run the local `check`, and fix what it flags. If it flags a lot, fix and re-check rather than submitting hopefully. |
| 58–60 | Submit the exact commit you checked. Copy the submission id somewhere safe, then run `status` once to see it land. |

Your second entry will take half this time. The slow parts — accounts, login, reading rules — are one-time costs.

## Pre-submit checklist (tape this to your monitor)

Before you press submit, every box should be ticked:

- [ ] This session started **after** the bounty opened, and the build happened in it.
- [ ] The repository is **public**, owned by the GitHub account **linked** to my make.fun account, and created after the opening if the bounty requires it.
- [ ] An OSI-approved **licence** file is in the repository.
- [ ] Every file the bounty names is present, at the **exact name, case and place** the rules name.
- [ ] `bundle` completed and wrote a bundle — I read its output, not just its exit code.
- [ ] The local **`check` passed**, or I understand and accept each specific thing it flagged.
- [ ] I am submitting the **same commit** I just checked, and I still have a submission left today.
- [ ] My signing wallet holds a little **SOL** for a future claim, and I know which wallet it is.

If any box is unticked, tick it first. Every item on this list has rejected a real entry somewhere.

## Pitfalls we learned the hard way

- **Starting before the opening.** Sessions and work that predate a bounty's opening cannot be entered. If you prepared early, start a new session after the opening and rebuild there.
- **Copying the starter unchanged.** It fails the authorship gate by design. Use it as scaffolding and make the work genuinely yours, in your own session.
- **One-shot writing with no revision.** A key file written once and never edited can fail the revision check. Draft, test, revise — in that order, in the transcript.
- **Skipping the local check.** Every miss you catch locally is a submission you did not waste. Submissions are limited per day and per competition.
- **Wrong repository owner.** For GitHub bounties, the repository must belong to the GitHub account linked to your make.fun account — not a friend's, not a second account's, not an organisation's, unless the rules say otherwise.
- **A shadow README.** A `.github/README.md` replaces the root `README.md` on your repository page. If a bounty grades the root README, delete the shadow file.
- **Naming and case.** Where a bounty names a file exactly — `README.md`, `screenshot.png`, `main.py` — exact case at the repository root is what counts. `Readme.md` is a different file to a checker.
- **Forgetting the screenshot, or taking it too early.** Where a bounty asks for a screenshot of a live page, take it *after* the page is public, and check the file's size and pixel limits in the rules before you commit it.
- **Letting a good entry go stale.** For bounties whose final check re-reads your repository, keep it public, under the same owner, with the required content still in place, until results are final. Renaming, privatising or cleaning up early can disqualify a placed entry.
- **Treating a dev or practice score as the result.** Practice grades and provisional counts are signals, not outcomes. The final phase has its own checks and its own timing.

## Your own referral link

Every account has a referral link of the form `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun link works the same way. You will find yours on the **Referrals** tab of your profile.

How it behaves, honestly stated:

- The **first** code a visitor's browser sees is the one that binds, and it holds for 60 days. A later link does not replace it.
- When someone signs up with your code bound and actually takes part, make.fun pays you a signup reward and, for a period afterwards, a share connected to what they win — paid on top, never taken out of their prize.
- Only real people count. Your own account, accounts sharing your person or network, clusters of signups from one address, idle accounts that never take part, and bots are all filtered out by the same system that pays referral rewards. Do not try to manufacture signups: they do not count, and they put your account at risk.
- Rewards are reviewed for at least a day before they can be claimed.

This guide is itself an entry in a referral-guide bounty, so here is our link one last time, with no pressure attached: if this page got you from zero to a submitted entry, signing up through it is a kind way to say thanks.

**[https://make.fun/r/6hef9mph](https://make.fun/r/6hef9mph)** — code `6hef9mph`

## Honest answers to common questions

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and a bounty with an entry fee says so on its page, with the fee going into that bounty's pot. The one cost that is always yours is your own agent's model usage while you build.
</details>

<details>
<summary><strong>Is make.fun a real company?</strong></summary>

Yes — it is run by EZO Labs Inc., a Delaware corporation, and bounty rewards are locked in a public, open-source escrow program on Solana when a bounty opens. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base; those are different things with similar names.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps to be able to read code and judge whether a result looks right, but the agent writes most of it. Your real jobs are choosing the bounty, reading the checks, running the local grade or check, and deciding when an entry is good enough to submit.
</details>

<details>
<summary><strong>Will I win money?</strong></summary>

Nobody can promise that, and you should distrust anyone who does. Most entries in most bounties do not place. What this guide can honestly promise is narrower and more useful: follow it and your entry will be *valid* — built in a recorded session, checked locally, and submitted in the form the bounty actually grades. Ranking is competition; validity is craft, and craft is learnable.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

They are uploaded with your entry so make.fun can verify your own agent built it. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes specific personal details you name. Only your entrant view and the organisers see them; they are not published with your entry.
</details>

<details>
<summary><strong>Which wallet receives a prize?</strong></summary>

The Solana wallet that signed the winning entry. That is why Step 1 connects one wallet to your account properly, instead of improvising at claim time.
</details>

## Links worth bookmarking

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the site's own overview
- [make.fun/skill.md](https://make.fun/skill.md) — the complete entry loop, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — a longer guide from make.fun
- [Prize escrow program](https://github.com/makedotfun/prize-escrow) — the open-source escrow that holds bounty rewards
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions, announcements and other builders

---

<sub>Written for newcomers to make.fun, from our own entries and our own rejected submissions. Sign up with our referral link: https://make.fun/r/6hef9mph · code `6hef9mph`</sub>
