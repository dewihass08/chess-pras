# JUDGE_PLAYBOOK — tiny-chess-01 (from RULES.txt, read end to end)

Process: read addyosmani `incremental-implementation`, then `source-driven-development`, before coding.

## Scoring
- 6 practice games: depth-2 (855), depth-3 (1073), depth-4 (1199), nodes-100k (1392), nodes-250k (1497), nodes-500k (1596); 3 white/3 black, distinct openings. Final adds nodes-1M (1667), nodes-2M (1712).
- Trial Elo = R with sum(1/(1+10^((anchor-R)/400))) = W + D/2, bisection, integer, clamped 0..2112. Rank = mean Elo; ties: plies to spare, then receipt. Contender trials replayed byte-identical: fixed node/depth, no clock, no unseeded randomness.
- 1800 s trial wall, 10,000 ms/move (aim ~3 s/move), 1 CPU, 512 MB. Game ends on mate, stalemate, insufficient material, 3rd occurrence, 100 quiet plies; at 200 plies adjudicate if material lead >= 5 else draw.

## Bar and prizes
- Practice floor 1154 Elo. House baseline sunfish 4 KB (3649 B, 50k nodes/move): 1364/1451/1279 on 6-game practice = mean 1365 (1325 on 8 games). Final staged: top 50 of 6 first-set trials become contenders, all 6 scored and replayed.
- Paid place needs mean Elo above every house baseline AND 90% paired t-interval of per-instance lead > 0; beating is a gate, not a rank. Prizes: 1st $100, 2nd $70, 3rd $50, 4-10 $20, 11-20 $14; $500 USDC on Solana, claim within 7 days.

## Gates
- main.py <= 4096 B committed, Python 3.13 stdlib only, no other repo file read/imported; packed lzma/zlib counts; whole repo <= 8192 B, no file > 4096 B; MIT license with SPDX line.
- No model calls, no network beyond env, no hidden data, no clock. Transcript gate: sessions present/wellformed/in window, >=30% reproduced lines, >=5 assistant turns, priced usage, >=2 writes, freshness anchor, run record, own work. GitHub entry needs badges+About/website and owner claim unless repo owner matches login.

Verify locally: all 3 practice instances, Elo vs baseline from same harness, two byte-identical runs, gate check 0 FAIL. Do not submit.
