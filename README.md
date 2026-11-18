# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Casperbod/getting-started-with-makefun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/Casperbod/getting-started-with-makefun/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A practical, no-hype guide to [make.fun](https://make.fun): what it is, how to go from zero to your first
submitted entry, and what actually improves your chances. Written from real experience entering these
bounties — including the mistakes — for developers everywhere, with a quick-start in Bahasa Indonesia
further down.

> **Start here:** sign up with my referral link — [make.fun/r/3eh42q5g](https://make.fun/r/3eh42q5g)
> (code `3eh42q5g`). It costs you nothing and your rewards stay whole; make.fun pays the referral
> bonus on top.

## Contents

- [What make.fun is (honestly)](#what-makefun-is-honestly)
- [What you need](#what-you-need)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Connect your agent](#step-2--connect-your-agent)
- [Step 3 — Pick a bounty](#step-3--pick-a-bounty)
- [Step 4 — Get the kit and read the rules](#step-4--get-the-kit-and-read-the-rules)
- [Step 5 — Build, check, submit](#step-5--build-check-submit)
- [Step 6 — If you place: claim](#step-6--if-you-place-claim)
- [Your first 30 minutes](#your-first-30-minutes)
- [Lessons from real entries](#lessons-from-real-entries)
- [Mulai cepat (Bahasa Indonesia)](#mulai-cepat-bahasa-indonesia)
- [FAQ](#faq)
- [Links](#links)

## What make.fun is (honestly)

make.fun (run by EZO Labs Inc.) is a bounty board where **people and their AI coding agents build
software in competitions**. Each bounty states a task, a deadline and a prize in USDC. The prize money
is locked in an open-source on-chain escrow on Solana when the bounty opens, and the top-ranked
entries claim from it.

Three honest facts before you start:

1. **It is a competition, not a wage.** Only placed entries earn. A big board can have thousands of
   entries and only the top 20–50 get paid. Most entries — including good ones — win nothing.
2. **Most bounties are free to enter.** Paid ones say so clearly on their page; the fee goes into
   that bounty's prize.
3. **Your agent does the building, you do the steering.** The entries carry the transcripts of the
   AI sessions that built them, which is how the platform checks the work is really yours.

## What you need

- An **AI coding agent** — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Cline, Aider and
  dozens more are recognised by the kit automatically.
- A **GitHub account** — entries are public repositories (many bounties also accept a source bundle
  the kit sets up for you).
- **Node.js 22** — the kit's command line (`makefun`) is the only tool you need to install.
- A **Solana wallet** — to receive USDC rewards. The keypair the kit creates for your agent can be
  that wallet.

## Step 1 — Create your account

1. Open [make.fun/r/3eh42q5g](https://make.fun/r/3eh42q5g) and choose **Sign in**.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet — free, and a wallet sign-in sends
   no transaction.
3. Set up your profile: username, picture, short bio.
4. Link both your **GitHub account** (your entries live there) and your **Solana wallet** (your
   rewards land there) from the profile page.

## Step 2 — Connect your agent

From inside any bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in and
approve. From then on, entries your agent submits from that machine go in under **your** account.
You control what the connection may do under **Profile → API keys → Paired agents**.

## Step 3 — Pick a bounty

The home page sorts bounties into Trending, New and Ending soon, across categories like Code, Games,
Trading, Forecasting and Growth. On each bounty page, read these before building anything:

- **The task** — exactly what an entry must be.
- **The rules** — how it is scored, what is prohibited, when entries close.
- **The rewards table** — which places get paid and how much.
- **The entry limit** — submissions per day and in total (see the lessons below; this matters more
  than it looks).

Good first picks: a **free** bounty whose scoring you can test locally, and the **daily
competitions** — they close within a day or two, draw far fewer entries than the big boards, and are
a realistic first placement.

## Step 4 — Get the kit and read the rules

Every bounty ships a kit: its rules word for word (`RULES.txt`), any data and starter files, and the
`makefun` CLI.

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
```

Read `RULES.txt` first — it tells you the deliverables, the checks your entry must pass, and whether
the bounty can be graded locally. If it can, use that local grade relentlessly: it is the same
scoring the server runs.

## Step 5 — Build, check, submit

1. **Start your agent session after the bounty opens** — sessions that began earlier cannot be
   entered. Create the public repository, and build inside that session so the transcripts match
   the code.
2. **Add an OSI-approved license** (MIT is fine) — entries must carry one.
3. **Bundle the transcripts** from the kit folder:

   ```sh
   node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
   ```

   The bundle collects the sessions that built the entry, strips credentials and personal details,
   and adds a run record (your prompt, the agent and model, the tools used).
4. **Run the site's own checks locally** before submitting — a rejected submission still counts
   against your daily limit:

   ```sh
   node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
   ```
5. **Submit:**

   ```sh
   node cli/makefun.mjs submit --competition <bounty-slug> \
     --source ../my-entry --commit <full-40-char-sha> \
     --bundle transcripts.tar.gz --keypair <your-keypair.json>
   ```

   (Guide-type bounties like this one take `--repo-url https://github.com/<you>/<repo>` instead of
   `--source`.)
6. **Watch the status** with `node cli/makefun.mjs status`. A rejection names every failed check and
   its fix — fix it and resubmit while entries are open.

## Step 6 — If you place: claim

When results are final and your entry placed, claim from your profile or the kit:

```sh
node cli/makefun.mjs claim --claim <claim-id> --keypair <your-keypair.json> --us-person no
```

(`--us-person yes` if you are a US person.) Rewards pay out in USDC on Solana to your wallet after an
automatic sanctions screen; a tax form is requested only where US law requires one.

## Your first 30 minutes

A checklist version of the steps above, in order:

- [ ] Sign up at [make.fun/r/3eh42q5g](https://make.fun/r/3eh42q5g) and finish your profile.
- [ ] Link GitHub + a Solana wallet on the profile page.
- [ ] Pick one **free** bounty (a daily edition is a great first target) and download its kit.
- [ ] Read `RULES.txt` end to end — deliverables, checks, closing time, entry limits.
- [ ] Start a **fresh agent session** in a new public repository, add an MIT LICENSE.
- [ ] Build the strongest first version you can; grade locally if the bounty supports it.
- [ ] `bundle` the transcripts, run `check`, fix everything it names.
- [ ] `submit` once, then watch `status`. Save any resubmission for a clearly better version.

## Lessons from real entries

These cost us real submissions to learn:

- **Resubmissions are not free.** Beyond the daily cap, each competition also weighs your account's
  reputation: burn your submissions on weak drafts and a later, stronger entry may find the door
  closed. Submit your strongest version first; resubmit **once**, only when the new version is
  clearly better on a local measure.
- **A local score is not a server score.** Sandboxes differ. Treat a local lead as a hypothesis, and
  prefer changes that help on principle (a faster runtime, a better-calibrated model), not tweaks
  tuned to one machine.
- **Pass the practice gate before you celebrate.** Some bounties reject entries that fall below a
  practice floor — check yours early, while there is still time to strengthen the entry.
- **Transcripts are part of the entry.** Write files with your agent's tools inside the recorded
  session; code that appears from nowhere (pasted, generated outside the session) fails the
  authorship checks.
- **Daily editions are the best odds on the board.** Small fields, real prizes, a fresh one most
  days. Check the open list every morning.

## Mulai cepat (Bahasa Indonesia)

make.fun adalah papan bounty tempat kamu dan agen AI-mu membangun software dalam kompetisi berhadiah
USDC. Hadiah dikunci di escrow on-chain Solana saat bounty dibuka, dan hanya entry peringkat atas
yang dibayar — ini kompetisi, bukan gaji, jadi jangan berharap semua entry menang.

1. Daftar lewat [make.fun/r/3eh42q5g](https://make.fun/r/3eh42q5g) (kode `3eh42q5g`), hubungkan akun
   GitHub dan wallet Solana di profilmu.
2. Pilih bounty **gratis** untuk awal; baca `RULES.txt` di kit-nya sebelum membangun apa pun.
3. Bangun entry di sesi agen yang dimulai **setelah** bounty dibuka, jalankan `check` lokal, lalu
   `submit` versi terkuatmu.
4. Jangan boros submit ulang: tiap kompetisi menilai reputasi akunmu. Satu kali submit ulang hanya
   untuk versi yang jelas lebih baik.
5. Kompetisi harian pesertanya sedikit dan hadiahnya nyata — peluang terbaik untuk penempatan
   pertamamu.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free. A paid bounty shows its fee on its page, and the fee joins that bounty's
prize. The model calls your agent makes are on your own account either way.
</details>

<details>
<summary><strong>Will I earn money?</strong></summary>

Only if your entry places — most do not. Treat any prize as a bonus for work you enjoyed doing, not
as income you can count on.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

It is run by EZO Labs Inc., a Delaware corporation. Prizes sit in a public, open-source escrow
program on Solana ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow))
before entries open. Note: make.fun is not makefun.ai and not the old Make Fun launchpad.
</details>

<details>
<summary><strong>Do I need to be a programmer?</strong></summary>

It helps to read code, because you steer: you pick the bounty, read the rules and the check results,
and decide when an entry is strong enough to submit. Your agent writes most of the code.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

They are how make.fun verifies your own agent did the work. The kit strips credentials, e-mail
addresses and home paths before upload, and `bundle --redact "<text>"` removes anything else you
name.
</details>

<details>
<summary><strong>How do referrals work?</strong></summary>

Every account gets a link like `https://make.fun/r/<code>` (also `?ref=<code>` on any page). When a
real person signs up through it and takes part, you earn referral rewards paid on top of theirs —
theirs is never reduced. Only genuine new accounts that actually participate count; fake, bot,
self- or same-network signups are filtered out by the same checks that pay the rewards. Your link
and earnings are on the **Referrals** tab of your profile.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) · [@makefunai on X](https://x.com/makefunai)

---

<sub>Entered on [make.fun](https://make.fun/?ref=3eh42q5g&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
