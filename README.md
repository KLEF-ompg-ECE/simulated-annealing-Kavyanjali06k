# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Angirekula Kavyanjali
**Student ID    :** 2310040033
**Date Submitted:** 17-03-2026

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() measures the number of conflicts in a timetable, such as overlapping classes or resource clashes. It evaluates how bad a timetable is based on these violations. A value of 0 means a perfect timetable with no conflicts.```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
generate_neighbor() creates a slightly modified version of the current timetable. It typically changes one or a few assignments, such as swapping time slots or rooms. The new timetable is similar to the current one but introduces small variations to explore better solutions.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the new solution based on its quality and probability. If the new solution is better (delta < 0), it is always accepted; otherwise, it may still be accepted with a probability based on temperature. Simulated Annealing accepts worse solutions to avoid getting stuck in local optima and to explore the search space more effectively.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed |1379|
| Clashes at iteration 1 |12|
| Final best clashes |3|
| Did SA reach 0 clashes? (Yes / No) |No|

**Copy the printed timetable output here:**
```
 Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The biggest drop in clashes happens early in the iterations, where the value quickly decreases from around 12 to about 6. After that, the improvement becomes slower with small step-wise reductions. The curve eventually flattens out, indicating that the algorithm is converging to a near-optimal solution.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        |      8        |       31             |       no           |
| 0.95        |      3        |       135            |       no           |
| 0.995       |      3        |        1379          |       no           |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
Fast cooling (0.80) reduces the temperature very quickly, so the algorithm stops exploring early and gets stuck with a higher number of clashes. Moderate cooling (0.95) performs better, allowing some exploration and achieving fewer clashes in fewer iterations. Slow cooling (0.995) takes much longer but provides a more stable and thorough search, leading to the best and most consistent results. Overall, slower cooling improves solution quality but increases computation time.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The best result is achieved with cooling_rate = 0.995 (and also 0.95 performs similarly). This is because slower cooling allows the algorithm to explore more solutions and avoid getting stuck in local optima. It balances exploration and convergence effectively, leading to fewer clashes.```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 |3| Slow cooling leads to steady convergence and better solutions|
| 2 — Cooling rate | cooling_rate = 0.995|3| Slower cooling gives better results, while fast cooling leads to poorer solutions|

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The most important thing I learned is that the cooling schedule is critical in Simulated Annealing. A fast cooling rate limits exploration and causes the algorithm to converge quickly to suboptimal solutions. In contrast, a slow cooling rate allows more exploration and helps in finding better solutions over time. However, this comes at the cost of more iterations and computation time. Therefore, choosing the right cooling rate is essential for balancing efficiency and solution quality.```

---

## Submission Checklist

- [k] Student name and ID filled in
- [k] Q1, Q2, Q3 answered
- [k] Experiment 1: table filled, timetable pasted, plot observation written
- [k] Experiment 2: results table filled (3 rows), observation and answer written
- [k] Summary table completed and reflection written
- [k] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
