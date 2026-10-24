<p align="center">
  <img src="twin-logo.png" alt="Twin." width="360">
</p>

<h3 align="center">AI companions for creators. Built to talk, built to sell.</h3>

<p align="center">
  <b>Twin Technologies</b> &middot; private engineering org
</p>

---

## What Twin is

Twin runs a fleet of AI companion "clones" for creators. Each clone is a real Telegram account that chats with fans in the creator's voice, sends photos, videos and voice notes, and sells paid content and bundles for Telegram Stars (and TON).

A creator signs up, fills in an onboarding form, uploads content, and gets a clone. We operate it. The creator keeps posting; the clone keeps the conversations going around the clock.

## How it fits together

```
 fans  <--->  Telegram  <--->  twin-bot / V2 engine  <--->  Supabase
                                     ^                         ^
 creators / agencies / operators --> twin-dashboard -----------+
                                     |
              twin-userbot (MTProto re-engagement)   t-social (Mini App + Lambda feed)
                                     |
                           twin-ops (deploy, backup, watchdog on AWS)
```

- **A clone is a database row.** No per-clone code paths, no per-clone deploys.
- **Money is decided in code, never by the AI.** The model picks an action; prices, Star amounts and discounts are computed deterministically.
- **Payment parity is sacred.** Every charge is deduplicated; never double credit, never miss one.
- **Businesses first.** Clones reply only through the creator's Telegram Business connection.

## Repositories

| repo | what |
|---|---|
| `twin-bot` | V1 Telegram bot runtime (grammY + TypeScript, `tsx`, no build step) |
| `twin-sexbot` | V2 engine: the newer conversation and sales engine running most of the fleet |
| `twin-dashboard` | Next.js operator, creator and agency dashboard, plus the admin and public APIs |
| `twin-userbot` | MTProto userbot for fan re-engagement campaigns |
| `twin-ops` | deploy, rollback, backup and watchdog scripts for the AWS boxes |
| `twin-onlyfans-backend` | OnlyFans-side backend and runners |
| `t-social` | T-Social Mini App (Reels and Trending) and its Lambda backend |
| `twin-gptbot` | comparison bot used for A/B testing against our engines |
| `twin-testbot` | texting test harness and reviewer |
| `twin-tgaiclone` | process docs, bug/feature pipeline, Dial Doctor agent, tracker CLI |

Some repos may still live under personal accounts while the move into this org is finished.

## Ground rules

1. **One Supabase project is live: `aouaenqayfltoqrmpitg`.** The old prod project is never touched.
2. **Everything is private.** Repos, buckets and dashboards stay private unless the owners say otherwise.
3. **One writer to the schema, one deployer at a time.**
4. **Docs-only pushes do not deploy.** Only `.md`, `.txt` and `archive/` are exempt.
5. **Verify before reporting.** A green typecheck is not proof; the check suites and a real conversation test are.
6. **No secrets in git.** Keys live in env files and AWS, never in commits.

## Deploys

Push to `main` on `twin-bot` or `twin-dashboard` builds an image in GitHub Actions. The box pulls it by digest over AWS SSM. `twin-ops/deploy.sh --dry-run` is the manual fallback; run it before any real deploy.

## Working here

- Read the repo's own `README.md` and `CLAUDE.md` before editing.
- Every fix ships a check. Plant the bug back and watch the check go red.
- Simulations never write fan rows; negative Telegram ids mean simulation.

<p align="center"><sub>Twin. &copy; Twin Technologies</sub></p>
