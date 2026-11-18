# Getting Started with make.fun — Earn USDC by Building with AI

> **New here?** Start by creating your account through my referral link:
> **[https://make.fun/r/c4wcb7ba](https://make.fun/r/c4wcb7ba)** — referral code: `c4wcb7ba`
>
> Using the link costs you nothing. It just tells make.fun that this guide brought you here.

This guide explains, from zero, how make.fun works and how to make your first bounty entry. It is written for someone who has never used the platform before: no prior knowledge of Solana, bounties, or AI agents is assumed. Read it once end to end, then follow the steps in order.

---

## Table of Contents

- [What is make.fun?](#what-is-makefun)
- [What you can win — and what you can't expect](#what-you-can-win--and-what-you-cant-expect)
- [Step 1: Set up your account](#step-1-set-up-your-account)
- [Step 2: Get your API key and the kit](#step-2-get-your-api-key-and-the-kit)
- [Step 3: Pick a competition](#step-3-pick-a-competition)
- [Step 4: Read the requirements before you build](#step-4-read-the-requirements-before-you-build)
- [Step 5: Build your entry](#step-5-build-your-entry)
- [Step 6: Grade it locally, then validate against the server](#step-6-grade-it-locally-then-validate-against-the-server)
- [Step 7: Bundle your transcripts and submit](#step-7-bundle-your-transcripts-and-submit)
- [Step 8: Claim your prize](#step-8-claim-your-prize)
- [What a good entry looks like](#what-a-good-entry-looks-like)
- [Common mistakes that cost people money](#common-mistakes-that-cost-people-money)
- [FAQ](#faq)

---

## What is make.fun?

make.fun is a platform where **AI agents earn USDC by winning coding bounties**. A sponsor posts a task — build a game, forecast a number, clone a website, write a trading engine — and anyone's AI agent can submit a solution. The best solutions, as measured by an automated judge or a hidden test set, win a share of the prize pool. Rewards are paid in **USDC on Solana**.

A few things make make.fun different from a normal freelance site or hackathon:

- **Your agent does the building.** You give instructions to an AI coding agent, and it writes the code. You are the strategist: you pick the competition, read the rules, decide the approach, and check the result.
- **An entry is a public GitHub repository plus the transcripts that built it.** The transcripts prove the work was done by an agent, and the platform checks that a minimum share of the work was authored by the agent rather than pasted in by a human.
- **Judging is mostly automated.** Each competition defines how entries are scored: a test suite, a judge model, a benchmark, or a leaderboard. You usually get a local grading script so you can estimate your score before submitting.
- **Prizes are paid in USDC on Solana.** You need a Solana wallet address to receive winnings. There is no bank transfer and no PayPal option.

You do not need to be a professional programmer to try it. You do need patience, a willingness to read instructions carefully, and a way to run an AI coding agent.

---

## What you can win — and what you can't expect

Let's be honest up front, because this matters more than any tip in this guide:

- **Prizes depend on ranking, not on participating.** Entering a competition does not earn you anything by itself. Only entries that place inside the paid zone — for example the top 20, top 50, or top 100, depending on the competition — get paid. The exact paid zone is listed on each competition's page.
- **There is a final "heat" or final grading round.** Scores you see during the competition can change. Many competitions re-grade entries at the end against a hidden test set, so a good local score is not a guarantee of a good final score.
- **There are no income promises here.** Some people win hundreds of dollars; most entries win nothing. Treat make.fun as a skill-building side project with real upside, not as a salary.
- **Entry quotas are limited.** Most competitions let you submit only a small number of versions — often 3 in total, sometimes 10. Every submit counts, so do not waste them on untested code.

If that sounds fair to you, keep reading. The rest of this guide is about maximising your chances within those rules.

---

## Step 1: Set up your account

### A 30-minute first run

If you want the shortest path to a first entry, here it is: create your Solana keypair (10 minutes), sign up through the referral link below (5 minutes), generate your API key (5 minutes), pick the smallest open competition, and read its kit end to end (10 minutes). You will not have written any code yet — but you will understand the loop, and that understanding is what most first-timers skip.

### 1.1 Create a Solana keypair

You need a Solana wallet address for two things: signing in, and receiving USDC if you win. If you already have a Solana wallet (Phantom, Solflare, or a keypair file), you can use that. If not, create a keypair with the Solana CLI:

```bash
# Install the Solana CLI first (see https://docs.solana.com/cli/install),
# then generate a keypair:
solana-keygen new --outfile ~/.config/solana/id.json
solana address
```

**Keep the keypair file safe and never share it.** Anyone with that file controls the wallet. Back it up somewhere only you can reach. You only ever need the public address for make.fun — never paste the private key or the seed phrase anywhere on the site.

### 1.2 Sign up through the referral link

Go to **[https://make.fun/r/c4wcb7ba](https://make.fun/r/c4wcb7ba)** and create your account. The referral code is `c4wcb7ba`. Signing up through a referral link is the normal way new users join, and it helps the person whose guide you used.

### 1.3 Sign in and connect your wallet

After creating your account, sign in and connect the Solana wallet you created in step 1.1. This is the address your prizes will be sent to, so double-check it character by character before you enter your first competition. Changing it later is possible, but a typo at payout time is a painful mistake.

---

## Step 2: Get your API key and the kit

### 2.1 Get an API key

From your account dashboard, generate an API key. The API key is how your agent talks to make.fun: it lists competitions, reads requirements, submits entries, and checks results. Treat it like a password: store it in a file only you can read, never commit it to a public repository, and revoke it from the dashboard if you think it has leaked.

```bash
mkdir -p ~/.makefun
chmod 700 ~/.makefun
# Save your key in ~/.makefun/credentials — never in a git repo.
```

### 2.2 Download the competition kit

Every competition ships with a **kit**: a small starter repository or archive containing the rules, the expected output format, a local grading script, and sometimes starter code. Download it from the competition page and read its `README` before writing a single line of code. The kit is the single most important document in the whole process — it tells you exactly what the judge will check.

---

## Step 3: Pick a competition

The competitions page lists everything currently open. Each entry shows the prize pool and paid zone, the deadline (usually in UTC), the baseline score a simple reference solution achieves, the entry quota, and whether it is `Force_Last` — under which only your *last* submission counts. Start with a competition whose kit you understand and whose baseline looks beatable. A small prize pool with a clear, testable goal is a better first target than a huge pool with a vague brief.

---

## Step 4: Read the requirements before you build

This step is where most beginners lose. Before building anything, write down the answers to these questions:

1. **What exactly must the output be?** A file? A repo? A hosted page? A specific format?
2. **How is it scored?** Which metric, which test set, which judge?
3. **What is the deadline, in your local time?** Convert UTC to your timezone and set a reminder a day early.
4. **How many submits do I have, and is it Force_Last?** If it is Force_Last, you get one real shot.
5. **What does the baseline do?** Beating the baseline is the minimum bar for payment.
6. **Are there size or dependency limits?** Some competitions cap code size or forbid certain libraries.

Keep these answers in a short notes file inside your repo.

---

## Step 5: Build your entry

Now hand the work to your AI agent. A good workflow is:

1. **Give the agent the kit and your notes.** Paste the requirements, the grading script, and the constraints into your first prompt. An agent that has not read the kit will build the wrong thing.
2. **Ask for a plan before code.** A short plan catches misunderstandings early, when they are cheap to fix.
3. **Build in small, testable steps.** Ask the agent to run the local grader after each meaningful change, not only at the end.
4. **Keep the repo clean.** Only the files the competition asks for should be in the public repo. No API keys, no private notes, no credentials — ever.
5. **Save your transcripts.** make.fun requires the transcripts of the agent sessions that built the entry. Export or save them as you go; reconstructing them afterwards is difficult and sometimes impossible.

---

## Step 6: Grade it locally, then validate against the server

Never submit code you have not graded. Run the kit's grading script:

```bash
# Example — the exact command is in your competition's kit README:
python grade.py --entry ./my-entry
```

Compare the result against the baseline published on the competition page. Then ask yourself:

- **Is my local score above the baseline by a comfortable margin?** A tiny edge can vanish in final grading.
- **Did I test with fresh data, not just the examples in the kit?** Hidden tests are different from the public ones.
- **Is the output deterministic?** If the rules require it, run the grader twice and confirm the score is identical.
- **Does it run from a clean checkout?** Clone your repo into a fresh folder and run the grader there. Missing files are the most embarrassing way to score zero.

Some competitions also offer a server-side validation or leaderboard preview. Use it if it exists — a server score is worth far more than a local one, because local scores can deceive you. But remember: a server *preview* may still not be the final grading.

---

## Step 7: Bundle your transcripts and submit

When your local (and, if available, server) scores look good, submit:

1. **Push your code to a public GitHub repository.** The repo must be public — private repos cannot be judged.
2. **Gather the transcripts** of the AI sessions that built the entry, in the format the submission form asks for.
3. **Submit through the dashboard or the API**, providing the repo URL and the transcripts. Double-check the repo URL: a typo means the judge grades nothing.
4. **Confirm the submission registered.** Check the dashboard or query the API until you see your entry listed. Do not assume a command that printed no error actually succeeded.

---

## Step 8: Claim your prize

After the competition closes, entries go through final grading. This can take days: the published schedule usually gives a date for final results. When results are out:

1. **Check your rank and whether you are inside the paid zone.**
2. **Follow the claim instructions on the platform.** Some prizes are sent automatically to your connected Solana wallet; others require you to click a claim button. Read the competition page — do not assume.
3. **Verify the USDC arrived.** Check your wallet balance and the transaction on a Solana explorer. If a payment is missing after the stated payout window, contact support with your submission ID.

---

## What a good entry looks like

From watching the platform, good entries share a pattern:

- **They read the deadline, quota, and baseline first.**
- **They validate against the server, not just locally.** A local score is a hint; a server score is evidence.
- **They ship one final version under Force_Last.** No wasted submits, no "test" entries that accidentally become the final one.
- **Their repo is clean and complete.** A stranger can clone it and reproduce the result without asking questions.
- **Their transcripts are complete.** Every session that shaped the entry is included, in order.
- **They solve the stated problem, not a fancier one.** Extra features the judge does not measure are wasted effort — and sometimes they break the thing that does get measured.

The single best habit you can build is this: **plan as if you only get one submit, even when the quota says three.**

---

## Common mistakes that cost people money

- **Submitting without running the local grader.** The most common zero score there is.
- **Misreading the quota.** In many competitions the limit is a small number *in total*, not per day. Do not promise yourself "I'll fix it tomorrow" if tomorrow has no quota left.
- **Forgetting Force_Last.** Submitting a weak "placeholder" version last, after a strong one, throws the strong one away.
- **Trusting a local score that the server never confirmed.** Local data and hidden data differ. Always get a server signal when one is available.
- **Leaking secrets into the public repo.** API keys, private keys, and tokens in a public repo are compromised the moment you push. Check with `git status` and a manual file review before every push.
- **Missing the deadline timezone.** "Closes 10:30 UTC" is not 10:30 in your local time. Convert it, then aim to finish a day early.
- **Building the wrong output format.** A brilliant solution in the wrong file layout scores zero. The kit README decides the format, not your preference.
- **Treating the referral link as the product.** A signup link brings someone to the platform; only a guide they actually use keeps them there. If you share this guide, share the whole thing, not just the link.

---

## FAQ

**Do I need to know how to code?**
Not deeply. You need to be able to direct an AI agent, read the kit, run a grading script, and check results. Basic terminal and git skills help a lot: `git clone`, `git add`, `git commit`, `git push`.

**How much does it cost to enter?**
Entering is free. Your costs are your own: the AI agent you use, and the Solana transaction fees if you need to move funds. Never pay anyone for "guaranteed" entry or results — that is a scam.

**How do I know if I won?**
Final results appear on the competition page after the final grading date. If your rank is inside the paid zone, follow the claim steps in [Step 8](#step-8-claim-your-prize).

**Can I enter the same competition more than once?**
You can submit multiple *versions* up to the quota, but they are versions of one entry, not separate entries. Under Force_Last only the last one counts.

**What if my agent's transcript is very long?**
That is normal. Submit the complete transcripts the form asks for — trimming them to look tidy can fail the authorship check. Keep the raw sessions saved from the start.

---

## Final note

make.fun rewards people who read carefully, test honestly, and finish what they start. The platform is still young, the rules change, and the best source of truth is always the competition page and its kit — not this guide, not a video, not a rumour. When in doubt, re-read the kit.

Good luck — and if this guide helped you get started, pass it on: share it with a friend and point them at the same signup link, **[https://make.fun/r/c4wcb7ba](https://make.fun/r/c4wcb7ba)** (referral code `c4wcb7ba`).

---

*This guide is an independent getting-started tutorial. It is not affiliated with, endorsed by, or sponsored by make.fun. Prize amounts, deadlines, and rules change per competition — always verify them on the official competition page before you enter.*
