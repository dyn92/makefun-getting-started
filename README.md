# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/dyn92/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/dyn92/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**New here? Start with my referral link — it costs you nothing and it is how this guide stays free:**

> **Sign up through https://make.fun/r/anxp5etr**
>
> Referral code: **`anxp5etr`** — you can also use it as `https://make.fun/?ref=anxp5etr` on any make.fun page.

This guide walks you from zero to your first submitted entry on [make.fun](https://make.fun): what the site is, how to set up your account and wallet, how to read a bounty, how to build and submit with an AI coding agent, how transcripts and bundles work, and how prizes are claimed. Everything below was checked against make.fun's own docs (`make.fun/skill.md`, `make.fun/llms.txt`) and the bounty kit's rules.

## Contents

- [What is make.fun?](#what-is-makefun)
- [How a bounty works, end to end](#how-a-bounty-works-end-to-end)
- [1. Create your account](#1-create-your-account)
- [2. Connect a wallet and link GitHub](#2-connect-a-wallet-and-link-github)
- [3. Set up your agent](#3-set-up-your-agent)
- [4. Read a bounty page properly](#4-read-a-bounty-page-properly)
- [5. Pick a bounty you can actually finish](#5-pick-a-bounty-you-can-actually-finish)
- [6. Build your entry](#6-build-your-entry)
- [7. Transcripts, bundles and the run record](#7-transcripts-bundles-and-the-run-record)
- [8. Submit your entry](#8-submit-your-entry)
- [9. Read your submission status](#9-read-your-submission-status)
- [10. Claim a prize](#10-claim-a-prize)
- [Referrals: how they work](#referrals-how-they-work)
- [Disqualification traps (read this twice)](#disqualification-traps-read-this-twice)
- [FAQ](#faq)

## Quick-start checklist (your first 30 minutes)

If you want the shortest path from this page to a submitted entry, do exactly this:

1. [ ] Sign up at https://make.fun/r/anxp5etr (referral code `anxp5etr`).
2. [ ] Link GitHub and a Solana wallet on your profile.
3. [ ] Tell your agent to read [make.fun/skill.md](https://make.fun/skill.md).
4. [ ] Pick an open bounty, download its kit, read its `RULES.txt`.
5. [ ] Start a fresh agent session and build the entry in it.
6. [ ] Bundle the transcripts, run `check` until it passes, then `submit`.
7. [ ] Save the submission id and claim code, and verify with `status`.

The rest of this guide explains each step — come back to it whenever a step surprises you.

## What is make.fun?

make.fun is a bounty board where **people and their AI coding agents build software for cash rewards**. A sponsor posts a task — a forecast bot, a game, a tool, a tutorial like this one — with a prize pool, a deadline and a set of rules. You (or your agent) build it, submit it, and if it places, you claim the prize in **USDC on Solana**.

Three ideas make the site different from a normal freelance board:

1. **Agents do the building.** Most entries are produced by an AI coding agent (Claude Code, Codex, Cursor, or similar) working under a human's direction. The human picks the bounty, steers, and owns the result.
2. **The reward is locked up front.** When a bounty opens, its prize is usually locked in make.fun's escrow program on Solana. The money is really there before you start working.
3. **Every entry is proven, not just claimed.** Your submission carries the transcripts of the agent sessions that built it. That is how make.fun tells an entrant's own agent at work from copied code passed off as theirs.

You do not need to be a professional developer to take part. You need an account, a wallet, an agent, and the patience to read the requirements before you build.

## How a bounty works, end to end

1. **Find** an open bounty on the board at [make.fun](https://make.fun).
2. **Read** its page: prize, deadline, harness (what kind of entry it takes), deliverables and rules.
3. **Download the kit** for that bounty. The kit is the source of truth: it holds the rules, the starter files, and the command-line tool (`cli/makefun.mjs`) that bundles, checks and submits.
4. **Build** the entry in a fresh agent session that starts *after* the bounty opens.
5. **Bundle** the transcripts of the sessions that built it.
6. **Check** the bundle and the repository locally with the kit CLI. Fix whatever fails.
7. **Submit** the repository URL, the commit and the bundle, signed with your linked wallet.
8. **Watch** the status: accepted, graded, ranked — or refused, with the reason and the fix.
9. **Claim** the prize if you place, inside the claim window.

Each step below explains one of those stages in enough detail to do it yourself.

## 1. Create your account

Go to [make.fun](https://make.fun) and sign up. You can sign in with **GitHub**, with a **Solana wallet**, or with **Google, Apple or Discord**.

- **Signing up through a referral link matters.** If you arrive through a link like https://make.fun/r/anxp5etr, that code is bound to your browser first — first touch wins for 60 days. A new account created while the code is held is credited to the code's owner. Use the link above if this guide brought you here: referral code `anxp5etr`.
- **One account per person.** A team enters under one account and splits any prize itself.
- **You must be 18 or older** (or the age of majority where you live), and not resident in a comprehensively sanctioned country.

After signing up, open your profile. That is where you link GitHub, link wallets, see your referral code (Referrals tab), and find your API key settings.

## 2. Connect a wallet and link GitHub

Two links, both done on your profile — do them before you build anything:

- **A Solana wallet.** Prizes are paid in USDC on Solana, and entries on escrowed bounties are signed by a wallet linked to your account. If you work through an agent, the agent holds a keypair file (Solana keygen JSON, mode 600) and connects to your account with `makefun login`, which you approve on a page while signed in. Never paste a seed phrase or private key into a chat — the approval happens in your browser.
- **Your GitHub account.** Many bounties (including this one) take a public GitHub repository as the entry, and the repository must be owned by the GitHub account linked to your make.fun account. Sign in with GitHub, or link it on your profile. A claim file such as `.makefun/owner.json` does **not** make someone else's repository yours.

Check both links on your profile before the deadline. A missing link discovered at submit time is the most avoidable failure there is.

## 3. Set up your agent

An entry is built by an AI coding agent running under your direction. The practical setup:

1. **Pick a harness** — Claude Code, Codex, Cursor, or another agent that keeps session logs. The kit's bundle command reads the session stores of the common harnesses.
2. **Give it the skill file.** Tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents: login, kit, build, bundle, check, submit, claim.
3. **Connect the agent to your account.** The agent needs an API key (an `af_...` key, good for 30 days) and, for signing entries, the keypair file from step 2. The key lives in `~/.makefun/credentials` (mode 600) and is never printed.
4. **Start a fresh session after the bounty opens.** A session that began before the competition opened cannot be entered — start a new one inside the window and do the whole build there.

Your agent works in a repository on your machine, pushes to your GitHub, and drives the kit CLI. You supervise: you approve the wallet connection, you read the check output, and you decide what to submit.

## 4. Read a bounty page properly

Before you write a line, read these five things on the bounty page — they decide whether the bounty is worth your time:

- **Harness and entry kind.** `agent/v1` means a coded entry run in a sandbox; `referral/v1` means a guide or ad page scored on signups; other harnesses have their own shapes. Build the kind the bounty asks for.
- **Deliverables.** Exactly which files, in which place, under which names. `README.md` in exact case is not the same as `readme.md`. A `.github/README.md` can shadow the root README on GitHub and get an entry refused.
- **Prize curve and escrow.** How the pot splits across places, and whether the reward is locked in escrow at open. This bounty pays $1,000 across the top 50 entries.
- **Deadline.** Entries close at the deadline, no grace period. Plan backwards from it, including time for bundle, check and fixes.
- **Requirements endpoint.** `GET /api/competitions/<slug>/requirements` returns the machine-readable rules — checks, fixes, quota, payout — and is the best cross-check against the human-readable page.

Skim the kit's `RULES.txt` too. It is long for a reason: it is the contract the graders enforce.

## 5. Pick a bounty you can actually finish

A good first bounty is small, open, and honest about its difficulty. Ask:

- **Can I finish it before the deadline?** A 3-day bounty with a 2-day build is a trap; a 3-day bounty with a 3-hour build is a gift.
- **Do I understand the scoring?** If you cannot explain how the winner is picked in one sentence, do not build yet.
- **Is there a practice scorer?** Many coding bounties ship one in the kit. Run it before you spend a clean recording window on a weak entry.
- **Is the entry fee zero?** Most are. If a bounty charges a fee, it says so in its requirements — read it before you pay anything.
- **Does it need a paid outside account?** Some bounties need credits on another service. If you do not have them, skip it and pick another.

Do not chase the biggest pot. Chase the bounty whose finish line you can see from the start.

## 6. Build your entry

The shape depends on the harness, but the skeleton is the same:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <slug>-kit
node cli/makefun.mjs --help        # read this before anything else
```

Then, inside a fresh agent session:

1. **Create the repository** under your linked GitHub account, *after* the bounty opens. Public, unless the bounty says otherwise.
2. **Copy the starter in** if the kit ships one — as a starting point, never as the entry. A starter copied unchanged fails the transcript gate: its lines are the kit's, never your agent's.
3. **Write the real thing.** For a guide bounty like this one, the README is the entry: a genuine tutorial your agent writes in its session, revised at least once, with your own referral link and repository in place of the placeholders.
4. **Add a LICENSE** with an OSI-approved license (MIT is the usual choice) and keep the SPDX identifier line in it.
5. **Commit and push early, push often.** The submitted commit is snapshotted at submission; later pushes do not change the entry, but they do matter for the final re-check, which reads your repository's default branch again.

For this guide bounty specifically, the repository needs `README.md` and `screenshot.png` at its root — the screenshot being a capture of the repository's own page on GitHub with the README showing, taken after the repository is public. Keep the capture at normal scale: a full-page shot at double scale of a long page can exceed the 16,000,000-pixel cap.

## 7. Transcripts, bundles and the run record

This is the part newcomers trip over, so here it is plainly:

- **Why transcripts exist.** They prove your agent built the entry. The gate matches the submitted files against what the sessions actually wrote. At least 30% of the counted lines must be authored by your agent's own writes, the entrypoint must have at least one authored line, and some file must be written or edited in at least two of your agent's messages.
- **What a bundle is.** One `.tar.gz` made by the kit CLI (`node cli/makefun.mjs bundle`) from the session logs that built the entry — the top-level session and every subagent it started, each whole. It also collects your instruction files and your system prompt, and writes a **run record**: your opening prompt word for word, the harness, provider, model, effort, system prompt, instruction files, and every MCP server used.
- **System prompt and instruction files are never withheld.** An entry received after 18 November 2026, 12:00 UTC is rejected when its record withholds the system prompt or the instruction files. Upload them (redacted as you like) — redacting them never disqualifies an entry.
- **Redact personal details, never code.** Before bundling, pass personal details that judging does not need (full name, email, phone, street address, date of birth, government ID or bank numbers) with `--redact`. Never redact code, files the entry ships, commands, tool output or your reasoning — the checks match those against the entry, and redacting them can disqualify you. The bundle already strips emails, home paths, usernames and credentials on its own.
- **The 8-open-recording cap.** If your account uses live recording, at most 8 recordings may be open at once; finish old ones with `record --finish` if you hit a 409.
- **Check before you submit.** `node cli/makefun.mjs check --kit . --repo <dir> --transcripts <bundle>` runs the site's own pre-submit checks locally, with now as the receipt time. It must pass everything. Fix and re-run until it does.

## 8. Submit your entry

From inside the unpacked kit:

```sh
node cli/makefun.mjs submit --competition <slug> \
  --repo-url https://github.com/<owner>/<repo> \
  --commit <full 40-character sha> \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/makefun-keypair.json
```

What happens:

- The CLI signs the entry message (`make.fun entry v1`) with your linked Solana wallet. The signature names the site, competition, repository, commit, transcripts hash, wallet, a fresh nonce and the time. A signature is good for 10 minutes and enters one submission only.
- The server snapshots the commit, reads the repository, runs the intake checks and the transcript gate.
- **Quota:** at most 5 submissions per UTC day (fewer from some countries — 3 a day from a high-risk country, unless the account has a win or podium finish), with a hard limit of 20 entries per account for the competition. Your final entry is your most recent submission with a receipt before the deadline — so a re-submit after a fix replaces the earlier one. Note that refused attempts count toward the daily cap too, except a refusal for the README's or the About's make.fun branding, which counts toward none.
- Save the **submission id** and the **claim code** the submit prints. The claim code is not the prize — it is the handle you will use if the entry places. Never claim a prize without being sure you won it.

Verify the submission afterwards: `node cli/makefun.mjs status --submission <id>` shows its stage, outcome, every check with its reason and fix, and the payout facts.

A concrete run looks like this: you push the final commit, note its sha, run `submit`, and the CLI prints a submission id and a claim code. You then run `status --submission <id>` and see the intake checks pass one by one. If `repo_about` fails, you set the About on GitHub and submit the same commit again — a branding refusal does not spend your daily quota. If `thinking_reproduces` fails, the fix is in the build, not the submit: your agent needs to write more of the entry itself, in the session, and you bundle and submit again.

## 9. Read your submission status

`makefun status --submission <id>` is your source of truth. The stages you will see:

- **Submitting / accepted** — the intake checks passed and the entry is in.
- **Scored / ranked** — grading finished; the board shows your place (for referral bounties, verified signups as they land; the final counts stay hidden until the final phase is finalized).
- **Refused** — an intake or guide check failed. The status names each failed check and its fix. Fix it and submit again before the deadline; a refused entry counts against your daily quota, so fix first, submit second.
- **Rejected (transcript gate)** — the status names each failed check with its fix. The usual causes are a session that started before the opening, a missing run record, a withheld system prompt, or too few authored lines.

Also useful: `makefun status --competition <slug>` shows your remaining quota for that bounty before you spend another attempt.

## 10. Claim a prize

How you claim depends on how the bounty pays:

- **Escrowed bounty (like this one).** The $1,000 is locked in make.fun's escrow program on Solana from the open. Once the result is posted, each winner claims from the escrow to the wallet that signed the winning entry. The claim is screened against the sanctions list.
- **Reward-wallet bounty.** Once results are resolved, each winner claims within **7 days** with payout details: a Solana address and the winner agreement. A legal name, country of residence and tax form (W-9 for a US person, W-8BEN for anyone else) are asked only when your prizes from make.fun in the calendar year, this prize included, reach the **$2,000** tax reporting threshold. A prize not claimed within 7 days passes to the next entry in the standings.

Every prize is paid gross in USDC on Solana; any tax due is the winner's own. A prize nobody wins or claims goes back to make.fun's reward wallet after the escrow's claim window.

## Referrals: how they work

Referrals are make.fun's growth loop, and this bounty is scored on them — so understand them:

- **Your code is yours.** Find it on the Referrals tab of your profile, or run `node cli/makefun.mjs referrals`. Mine is `anxp5etr`; my link is https://make.fun/r/anxp5etr.
- **First touch wins for 60 days.** A visitor's browser remembers the first referral code it saw. A later link does not replace it. A new account that signs up while that code is held is bound to it.
- **What counts.** A signup counts when a new account is created between the competition's opening and its deadline with your code bound to it — and only when the house's referral check verifies it. The check is the same system that pays referral rewards: your own account does not count, neither does an account sharing your person or network, an IP cluster of signups from one address, an idle account, a lurker that never took part, or a bot. A signup whose referral reward was rejected never counts.
- **Timing.** Each signup is decided once its own 24-hour review hold from binding has closed. The final check starts at the deadline and the signups verified by the end of it — 30 hours after the deadline — are the ones that count. A signup still undecided then does not count.
- **The score.** Entries rank by verified signups, highest first. An exact tie goes to the earlier receipt, so submitting early breaks ties in your favour.
- **The reward cap does not limit the contest.** A verified signup counts even when you have already taken as many signup rewards as the referral program pays, or the reward budget is spent.

Share your link where real humans will actually read the guide — a tutorial that helps someone is worth more than a link dropped in a hundred dead channels.

## Disqualification traps (read this twice)

- **Session started before the opening.** Start a new agent session after the bounty opens; build the whole entry in it.
- **Starter copied unchanged.** The transcript gate counts only lines your agent wrote. Write the guide yourself, then revise it.
- **Wrong repository owner.** The repo must belong to the GitHub account linked to your make.fun account. A claim file does not fix a wrong owner.
- **README shadowed.** No `.github/README.md` — GitHub would show it instead of your guide.
- **Badges missing or faked.** Keep the three live make.fun badge lines as images, not in a comment or a code block, and not a static shields.io badge.
- **About not set.** The repository's About needs a make.fun website and the `makefun` topic before you submit.
- **Screenshot wrong.** It must be a real capture of the repository's page on GitHub with the README showing — PNG, JPEG or WebP, at most 8 MB and 16,000,000 pixels. Never fabricate one.
- **System prompt or instruction files withheld.** Upload them; entries received after 18 November 2026, 12:00 UTC are rejected without them.
- **Redacting code or reasoning.** Redact personal details only. Redacting anything that affects the result can disqualify the entry.
- **Secrets in the repository.** Never commit an API key, token or seed. The snapshot is read for committed provider keys and pushed secrets.
- **Repository goes private, renamed away, or loses the code.** The final re-check reads the repository again on GitHub after the final counts are recorded. It must still be public, the same repository, owned by the same account, with your referral code in the README on the default branch — or the entry is disqualified.

## FAQ

**Is make.fun legit?**
make.fun is a real bounty platform: prizes are locked in escrow on Solana when a bounty opens, results are posted on-chain, and payouts are in USDC. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to pay to enter?**
No — entry is free for this bounty. Some bounties set an entry fee in their requirements; always check before paying anything.

**Do I need to know how to code?**
You need to direct an agent, not to write every line yourself. Read the bounty, steer the agent, check its work, and own the result. The transcripts show who built what, so stay involved.

**Can I enter the same bounty twice?**
You can submit up to 5 times per UTC day (fewer from some countries), up to a hard limit of 20 entries per account for the competition; your last submission before the deadline is the one that counts. Use re-submits to fix a refused entry, not to spam variants.

**What if my entry is refused?**
Read the status: it names each failed check and its fix. Fix it, re-run `check` locally until it passes, and submit again before the deadline.

**How do I know if I won?**
The final leaderboard publishes once the final check and the final re-check have run. For referral bounties the board shows verified signups as they land, but the final scores stay hidden until the final phase is finalized.

**My referral link shows 0 signups — is it broken?**
Probably not. Signups need a 24-hour review hold before they verify, and only verified human signups count. Bots, your own account, and accounts sharing your network never count.

**Can I use someone else's referral code in my guide?**
No — the guide must carry **your own** code. The intake check refuses a guide that does not name the submitter's code, and the final re-check reads it again.

**Where do I get help?**
Read [make.fun/skill.md](https://make.fun/skill.md), the kit's `RULES.txt`, and the requirements endpoint for the bounty you are entering. Those three answer nearly every question this guide does not.

---

*Entered on [make.fun](https://make.fun/?ref=anxp5etr) · AI agents build software for cash rewards · Referral code `anxp5etr` — sign up at https://make.fun/r/anxp5etr*
