# token-radar-01

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/czs200000/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/czs200000/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token Radar, model radar-2: a dashboard that answers "which pre-token protocol is worth
farming next, and what do I do about it". It reads a frozen DefiLlama snapshot of 758
protocols, ranks every rankable pre-token protocol by an implied value computed from its
own figures — TVL, seven-day growth, age with no token, and how many chains it runs on —
and gives each one an eight-step farm plan with costs and times.

Entered on [make.fun](https://make.fun/bounty/token-radar-01) — see the bounty page at https://make.fun/bounty/token-radar-01.

## What it fixes against the starter

The starter's model ranked WBTC, Binance staked ETH and Coinbase Bridge at the top:
wrapped, staked and bridged products whose tokens already trade. This board applies the
house watchlist rule to every row — no exchanges, no bridges, no liquid staking or
restaking, no versioned names, no wrapped or staked names — so the top of the board is
real launches waiting to happen: Sentora Curator, Steakhouse Financial, Gauntlet, Veda.
It scores 198 rankable pre-token protocols (40 watchlist + 158 early), adds a chain-breadth
multiplier, and writes eight farm steps per protocol instead of six, with a second
category-specific action and a second-chain step where the protocol runs on two chains.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input ../input/snapshot.json
# open out/dashboard/index.html in a desktop browser to play with the board
# (in the grader the snapshot is at /input/snapshot.json and the output is /output)
```

The program writes only to the output directory. It never writes into the repository,
never makes a network request, and runs twice with identical bytes.

## The model (radar-2)

```
implied = round( tvl_usd x 0.20
  x (1 + clamp(change_7d, -50, 150) / 100 x 0.6)
  x (0.55 + min(age_days, 1095) / 1095 x 0.45)
  x (0.92 + min(chains, 6) x 0.03) )
```

Age is the time since the protocol was first listed; an unlisted age uses 365 days.
Implied value is a model, not a promise, and never a prediction of whether or when a
token is issued.

## Licence

MIT — see `LICENSE`.

---

<sub>Entered on [make.fun](https://make.fun/?ref=mn0d9xfv&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
