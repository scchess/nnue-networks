# Human-like NNUE Networks

This repository contains networks that I've developed with the goal to create various human-like styles. 

This is inspired by the Maia chess project and I wanted to make versions for [Stockfish NNUE](https://github.com/CSSLab/maia-chess). The con of the Maia bots is that it had endgame and tactical problems. Most engines are either too strong tactically or positionally. This aims to provide a more authentic sparring experience for players.

## Play At Lichess

You can play against these bots at Lichess through these links:
* [nnuehuman1200](https://lichess.org/@/nnuehuman1200)
* [nnuehuman1500](https://lichess.org/@/nnuehuman1500)
* [nnuehuman2400](https://lichess.org/@/nnuehuman2400)

## Play on your computer

If you want a local version on your computer, fork my [cfish repository](https://github.com/kennyfrc/Cfish) and follow the instructions there. I've made 3 branches named `elo1200`, `elo1600`, and `elo2300`. I know the elos there and at lichess are inconsistent. Will fix those on a later date.

## Just the nets

See [releases](https://github.com/kennyfrc/nnue-networks/releases).


## Fixed NPS testing results

An interesting observation from my fixed NPS testing is that if you pool together 1200, 1500, and 2300 in a 50k nps tournament (used `tc=40/60`), the estimated elos perfectly arrange themselves into 1200 and 1500. Only the 2300 net is different, but if you search on full nodes (see next test), then the elos start to look better. I've only tested on 180 games, so probably with more datapoints, the gaps will look right. Also added Shredder pegged at 1500 elo to provide a baseline. Book used is noomen 30.

```
Rank Name                          Elo     +/-   Games   Score    Draw
   1 cfish-2300                    338      69     180   87.5%   10.6%
   2 shredder-1500                  49      49     180   56.9%    8.3%
   3 cfish-1600                    -47      49     180   43.3%    7.8%
   4 cfish-1200                   -342      75     180   12.2%    5.6%
```

## Normal testing conditions

Without the nps limit, it's surprisingly weaker than [simpleEval](https://lichess.org/@/simpleEval), which is also stockfish but with just material counting (estimated at 2200 elo). Book used is noomen 30.

```
Rank Name                          Elo     +/-   Games   Score    Draw
   1 cfish-2300                    618     204     180   97.2%    1.1%
   2 stockfish-simpleEval          125      54     180   67.2%    2.2%
   3 cfish-1600                   -166      57     180   27.8%    1.1%
   4 cfish-1200                   -430     103     180    7.8%    0.0%
```

## Improvement Areas

The ratings bins aren't perfect. What can be done to further improve the experience:
* For the 1600 network, use a rating bin between 1200-1600.
* For the 2400 network, use a rating bin between 1600 to 2300 and replace the kingbase data.

That said, I would say that the experiment is a success so far for the 1200 version. Currently, the 1600 bot captures some bad habits from the <= 1200 elo bins and the 2400 is too strong. The above two changes should help fix that.

## Special Thanks

Special thanks to dkappe for helping pioneer the supervised learning trend for both Leela and Stockfish NNUE. Here's his [repository](https://github.com/dkappe/leela-chess-weights/wiki/) and [patreon](https://www.patreon.com/badgyal/posts). I also used his Kingbase 2300 data played to terminal to supplement my Caissabase data. Thanks as well to [Maia's project team](https://github.com/CSSLab/maia-chess) for renewing interest on AI that simulates human behavior.