# David Goggins Running Analytics

Three self-contained web pages that analyze David Goggins' ultrarunning record. Open any `.html` file in a browser; there is nothing to install and no server.

## Files

| File | What it does |
|---|---|
| `goggins-run-analytics-v2.html` | Dashboard of his verified timed races: miles per year, pace vs. distance, Badwater 135 across 2006/2007/2013, Moab 240 at age 45 vs. 50, full race log. |
| `goggins-race-sim.html` | Race simulator. Replays any of his 17 races and runs him against Eliud Kipchoge, a pro runner, a "decently healthy" runner and a "normal person". |
| `goggins-leg-biomechanics.html` | Spring-mass model of his legs at each race's real pace: contact and flight time, peak force, leg stiffness, footstrikes per leg, plus an animation. |
| `goggins-running-analytics.html` | Earlier version: a personal run log with sample data. Not about Goggins' real results. |

## Real data vs. model

**Real (published results):** race name, year, distance, finish time and place for 17 finishes.

**Model (my assumptions, not measurements):** everything for the other runners in the simulator, and every biomechanics number. Treat them as illustrative.

## Race data

Sources: ultrarunning.com, DUV ultra statistics (statistik.d-u-v.org), davidgoggins.com, and race-history summary sites.

| Year | Race | Miles | Time | Place |
|---|---|---|---|---|
| 2005 | San Diego One Day | 100 | 18:56:00 | n/a |
| 2006 | Badwater 135 | 135 | 30:18:54 | 5th |
| 2007 | Western States 100 | 100 | 20:52:50 | 26th |
| 2007 | Badwater 135 | 135 | 25:49:40 | 3rd |
| 2013 | Badwater 135 | 135 | 32:44:10 | 18th |
| 2013 | Hellgate 100K | 62.1 | 12:47:28 | 8th |
| 2015 | Hellgate 100K | 62.1 | 11:56:02 | 5th |
| 2016 | Strolling Jim 40 | 40 | 4:54:15 | 1st |
| 2016 | Zane Grey 50 | 50 | 11:23:29 | 13th |
| 2016 | Music City Trail 50K | 31.1 | 4:30:43 | 1st |
| 2016 | Infinitus 88K | 54.7 | 12:01:00 | 1st |
| 2016 | JFK 50 | 50 | 7:30:36 | 34th |
| 2019 | Leadville Trail 100 | 100 | 22:55:44 | 35th |
| 2020 | Moab 240 | 238 | 62:21:29 | 2nd |
| 2020 | JFK 50 | 50 | 7:08:26 | 25th |
| 2025 | Bigfoot 200 | 206 | 66:04:18 | 23rd |
| 2025 | Moab 240 | 238 | 84:57:23 | 21st |

### Known gaps

- He has completed 60+ ultras; this list is only the timed finishes I could verify.
- DNFs are excluded. Badwater 2008 is a DNF in every source; sources disagree on whether a second DNF was in 2012 or 2014.
- Triathlons, cycling and non-race feats (such as the 2013 pull-up record) are excluded.
- Exact months are unverified for 2005 and 2016 races, so the log shows years only.
- Moab 2025 is 84:57:23 on ultrarunning.com and 84:57:24 on another site. Distance is listed as 238 mi (DUV) or 240.

## Simulator model

- Each runner is defined by a flat marathon time: Kipchoge 2:01:09, pro 2:10:00, healthy 4:30:00, normal 6:30:00 (all editable).
- Finish time follows a Riegel-style curve: time scales with distance^1.06 up to 26.2 miles, then distance^k beyond (k = 1.25 by default; elite 100-mile marks sit close to that).
- A terrain multiplier per course is applied (1.0 for road or loop courses up to 1.5 for mountain and desert trail). **These multipliers are my rough estimates.**
- Rest or sleep time is added once moving time passes 20 hours (25% of the excess by default).
- Goggins' lane uses his actual time, with the same fatigue curve shaping his pacing.
- Kipchoge has never raced an ultra, so his results are extrapolation. The "normal person" lane assumes they can finish; most untrained people could not, or would miss cutoffs.

## Biomechanics model

Sine-wave spring-mass running model (Morin et al., 2005):

- Peak vertical force = m · g · (π/2) · (flight time / contact time + 1)
- Contact time = 0.40 − 0.035 · speed (seconds), capped at one step; my assumed fit
- Step time = 60 / cadence (default 160 steps/min)
- Leg length = 0.53 × height
- Leg stiffness = peak force / leg compression; vertical stiffness = peak force / center-of-mass drop
- Speed uses estimated moving time: 70% of elapsed time at 200+ miles, 92% at 100 to 135, 97% at 50 to 100, 100% under 50

Body size defaults to 1.85 m and 91 kg (Wikipedia's figures; other sites say 6 ft 2 in and about 190 lb). A preset shows 135 kg (297 lb), his reported weight before joining the SEALs.

Not modelled: fatigue-driven gait changes, downhill braking, terrain, shoes, joint-level (ankle, knee, hip) loads. Reported leg injuries (shin stress fractures, a fractured kneecap) come from press and biography accounts; no imaging or gait-lab data is public, so the pages make no claims about which leg or bone.

## Disclaimer

Educational and entertainment project. Not medical, coaching or training advice.
