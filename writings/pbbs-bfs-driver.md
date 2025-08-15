---
layout: default
title: "PBBS BFS Driver for Dummies"
permalink: /writings/pbbs-bfs-driver/
description: Covering the subtleties in running a PBBS benchmark driver.
---
<h1>PBBS BFS Driver for Dummies</h1>
<p class="subtitle">August 2025</p>

The documentation on how to **run** it is vague, 

> Official documentation: https://cmuparlay.github.io/pbbsbench/
>
> SimpleBFS: https://github.com/cmuparlay/pbbsbench/tree/master/benchmarks/breadthFirstSearch/simpleBFS

So, here is my take:)


Let's make the driver work
---------------------------

Run **make** for simpleBFS!

Well for the **infile** -> try running testInputs: `python3 testInputs`.

WTH: `make: *** [Makefile:82: randLocalGraph_J_10_20000000] Error 137`

**Error 137**: System limits! In my case: Ran out of RAM and Swap Space. Try running `htop`; This one is a beast on my machine containing 16 gigs of RAM and 16 cores (hyperthreaded) i5 13th gen. So tone down the parameters for all 3 graphs :

```python
tests = [
	[1, "randLocalGraph_J_10_50000", "", ""],
	[1, "rMatGraph_J_12_100000", "", ""],
	[1, "3Dgrid_J_150000", "", ""]
]
```

randLocalGraph_J_10_50000 is not generated in `cmuparlay/pbbsbench/.../testData/graphData/data`
Run make locally: `make randLocalGraph_J_5_50000`
Finally:

For: `<bench> [-o <outfile>] [-r <numrounds>] <infile>` 

Do: `./BFS -r 10 <your_dir_path>/testData/graphData/data/randLocalGraph_J_5_50000`

You should see something like this for r = 10 rounds, Voila!
>Parlay time: 0.0063
>Parlay time: 0.0066
>Parlay time: 0.0067
>Parlay time: 0.0063
>Parlay time: 0.0063
>Parlay time: 0.0065
>Parlay time: 0.0067
>Parlay time: 0.0067
>Parlay time: 0.0066
>Parlay time: 0.0063
