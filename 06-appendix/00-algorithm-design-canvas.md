---
title: "The Algorithm Design Canvas"
summary: "A structured way to think before you code: the eight areas of the design canvas, what belongs in each, how constraints tell you the answer, and the failure modes the canvas is built to prevent."
essential: true
---

# The Algorithm Design Canvas

Most failed coding interviews are not failures of algorithms. They are failures of **process** — the
candidate hears a problem, recognises something familiar, and starts typing. Twenty minutes later
they are debugging an approach that was never going to work, and there is no time left to start
again.

The canvas is a fixed set of questions you answer **before** writing a line of code. It is not a
form to fill in for its own sake. Each area exists because skipping it causes a specific, common,
expensive mistake.

<div style="border-left:4px solid #15448e;background:rgba(21,68,142,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

📘 **Where to use it.** Synapse has this canvas built in: every problem page has a **Think** tab
beside the code editor with these eight areas, an ℹ️ on each, and a Save button that keeps each
filled-in canvas as a timestamped entry you can re-read or export. Fill it there, then switch to
**Code**.

</div>

---

## The eight areas

| Area | The question it answers | The mistake it prevents |
|---|---|---|
| **Problem** | What am I actually being asked? | Solving a problem nobody asked for |
| **Constraints** | What are the limits? | Designing for the wrong scale |
| **Inputs** | What arrives, and in what shape? | Guessing the signature |
| **Return** | What do I hand back? | A correct algorithm that returns the wrong thing |
| **Error / N/A** | What happens when there is no answer? | Inventing a sentinel mid-code |
| **Maintenance** | What state must stay in sync? | Off-by-one and stale-pointer bugs |
| **Ideas** | What approaches exist, and what do they cost? | Coding the first idea you had |
| **Tests** | What will I run it against? | Discovering the edge case in the judge |

The order matters. Later areas depend on earlier ones — you cannot write Tests without Constraints,
and you cannot compare Ideas without knowing the Return.

---

## 1 · Problem

**Restate the problem in one sentence, in your own words.**

If you cannot restate it, you do not understand it, and every area below will inherit the
confusion. Saying it back also gives the interviewer a chance to correct you in the first minute
rather than the last.

A good restatement:

- is one sentence, not a paraphrase of the whole prompt;
- uses your own words, not the prompt's;
- names the success criterion — what does a *correct* answer look like?

> **Prompt:** "Given an array of integers, move all zeroes to the end while maintaining the relative
> order of the non-zero elements. Do this in place."
>
> **Restatement:** "Rearrange the array in place so every non-zero keeps its original order at the
> front, and all the zeroes end up after them."

Also write down the **category** you think it belongs to — arrays, two pointers, graphs, dynamic
programming. You are usually right, and being explicit means the interviewer can tell you early if
you are not.

---

## 2 · Constraints

This is the area people skip, and it is the one that carries the most information.

An ill-defined problem is unsolvable. Sorting 50 numbers and sorting five billion
million-character strings are different problems with different answers. **Ask — never assume.**

### What to ask about

| Dimension | Ask |
|---|---|
| **Size** | Minimum and maximum of every key value, especially N. Are there several? (`n` rows *and* `m` columns) |
| **Value range** | How large can a value get? Can it be negative? Zero? |
| **Type** | Integers or floats? ASCII or Unicode? Signed or unsigned? |
| **Ordering** | Is the input already sorted? Partially? |
| **Uniqueness** | Are duplicates possible? |
| **Shape** | Array, stream, linked list, adjacency matrix, adjacency list? |
| **Mutability** | May I modify the input? |
| **Memory** | Is there a ceiling? Must the solution be in place? |
| **Time** | Is there a stated budget, or an implied one? |
| **Availability** | Is the whole input in memory, or does it arrive over time? |

### The part both classic write-ups leave out: N tells you the answer

The maximum size of N is not trivia. It is the interviewer telling you which complexity class they
expect. Roughly 10⁸ simple operations run in about a second, so:

| Max N | Complexity you can afford | Typical shape |
|---|---|---|
| ≤ 10 | O(n!) · O(2ⁿ · n) | permutations, brute-force search |
| ≤ 20–25 | O(2ⁿ) | subsets, bitmask DP |
| ≤ 100 | O(n⁴) | four nested loops, small DP tables |
| ≤ 500 | O(n³) | Floyd–Warshall, interval DP |
| ≤ 5 000 | O(n²) | pairwise DP, two nested loops |
| ≤ 10⁶ | O(n log n) | sorting, heaps, binary search on answer |
| ≤ 10⁸ | O(n) | single pass, hash map, two pointers |
| > 10⁹ | O(log n) · O(1) | maths, binary search, closed form |

If the prompt says `n ≤ 10⁵` and your idea is O(n²), that is 10¹⁰ operations — the constraint has
already told you the idea is wrong, before you wrote it. Read the constraint **as a hint**.

### Overflow: the constraint nobody writes down

If values reach 10⁹ and you add two of them, you have 2 × 10⁹ — past the ~2.15 × 10⁹ ceiling of a
signed 32-bit integer. Multiply two and you are far past it.

- **Java / C++:** `int` overflows silently and wraps. Use `long`.
- **Python:** integers are arbitrary precision, so this never bites — say so, because the
  interviewer may be checking whether you know it would in another language.
- **Sums over an array:** the sum of n values each up to V needs room for `n × V`, not `V`.
- **Midpoints:** `(lo + hi) / 2` can overflow; `lo + (hi - lo) / 2` cannot.

### Floating point

If the input can be a float, `a == b` is not a safe test and summing in a different order gives a
different answer. Ask whether an epsilon comparison is acceptable, and what precision the output
needs.

---

## 3 · Inputs

Write the signature concretely — the way you would write a docstring.

- Each parameter with its **type**: "array of 32-bit signed ints".
- **Sizes**: "length ≤ 10⁴".
- **Structure**: "string of ASCII", "adjacency matrix", "list of `(start, end)` pairs".
- Whether it arrives **sorted** or **de-duplicated**.

```text
nums:   int[]   length 1 ≤ n ≤ 1e4,  −1e9 ≤ nums[i] ≤ 1e9,  unsorted, duplicates allowed
target: int     −1e9 ≤ target ≤ 1e9
```

This takes thirty seconds and removes an entire class of misunderstanding. It also forces you to
notice things the prose glossed over — if you cannot write the type, you do not know it yet.

---

## 4 · Return

Getting this wrong wastes the whole coding round, and it is a ten-second question.

- **Value and type**: "an `int[]` of two indices".
- **Indices or values?** These are different answers to the same-sounding question.
- **Any order, or a required order?**
- **In place instead of a return value?** Then the return is `void` and the *input* is the output.
- **Void plus printed output?** (Printing all permutations, for example.)
- **What if several answers are valid** — any one, or the first, or all of them?

> The single most common wasted round: returning the **values** when the problem wanted the
> **indices**. Both articles this lesson draws on call it out, and it still happens constantly.

---

## 5 · Error / N/A

What the function does when there is no good answer. Agree this with the interviewer rather than
inventing it silently halfway through coding.

- **Not found** → `-1`, `None`, `null`, an empty array, or an exception?
- **Bad input** → throw, or return defensively?
- **Empty input** → what exactly? (An empty array is not the same as `null`.)
- **Single element** → is the problem even defined? ("Second largest of `[5]`")
- **Ties** → any of them, the first, or all?
- **Out of range** → clamp, wrap, or reject?

Whatever you agree, write it down here, because in ten minutes you will be deep in a loop and will
not remember which one you chose.

---

## 6 · Maintenance

The state your algorithm must keep in sync while it runs. These are the bugs that actually bite:
not the algorithm being wrong, but a pointer you forgot to move.

- **Pointers that must stay valid** — the tail of a linked list, both edges of a sliding window.
- **Running values** — best so far, current sum, the seen-set, a counter.
- **Updates that belong after the loop, not inside it** — the last window, the final group, the
  trailing element.
- **Two structures that must agree** — a heap and a hash map indexing into it; a `count` and the
  container it counts.

### State it as an invariant

The sharpest version of this area is a single sentence that is true at **every** loop boundary:

> *After processing index `i`, everything in `nums[0..write)` is non-zero and in original order.*

An invariant is worth more than a list of reminders, because you can check it. At every line that
changes state, ask: is the invariant still true? If it is true at the start, preserved by the body,
and the loop terminates, the algorithm is correct — that is the whole proof, in one sentence you
already wrote.

---

## 7 · Ideas

One to three approaches, **brute force first**, then refined. Each gets a short description any
interviewer can follow, plus its time (T) and space (S) complexity.

### Always start with the brute force

Say it out loud even when it is obviously too slow. It does three things: it proves you understood
the problem, it establishes a correctness baseline you can test the fast version against, and it
gives you something to *improve* — which is the conversation the interviewer is actually there to
have.

### Then improve it deliberately

Most optimisations are one of a small number of moves:

| Move | Trade | Typical win |
|---|---|---|
| Add a hash map | space for time | O(n²) → O(n) |
| Sort first | O(n log n) up front | enables two pointers, binary search |
| Two pointers | none | O(n²) → O(n) on sorted or partitionable data |
| Sliding window | none | recomputation → incremental update |
| Precompute prefix sums | O(n) space | range query O(n) → O(1) |
| Binary search the answer | — | O(n) search space → O(log n) |
| Memoise | space for time | exponential → polynomial |
| Heap instead of sort | — | full sort → top-k in O(n log k) |

Name the trade you are making. "I will spend O(n) memory to get from quadratic to linear time" is
the sentence that shows you are choosing rather than guessing.

### Getting complexity right

Say **what n means** before you say the complexity — with two inputs, "O(n)" is ambiguous and
O(n + m) is usually the honest answer.

Then be careful about space, which is where most people are casually wrong:

- **Auxiliary space** is what you allocate. **Total space** includes the input. Interviewers
  usually mean auxiliary — ask which.
- **The recursion stack counts.** A recursive solution with no explicit data structure is not
  O(1) space; it is O(depth). For an unbalanced tree, that is O(n).
- **Output space usually does not count** — returning an array of n results is not "O(n) extra
  space" in the sense being asked about, unless the problem is about space.
- **A sort is not free.** Most library sorts use O(log n) to O(n) auxiliary space.

Only write the code for the idea you and the interviewer **agreed on**.

---

## 8 · Tests

The cases you will run against, written *before* you code. Your Constraints section is the raw
material — go back to it and hit every minimum and maximum it names.

### Derive the cases from the constraints

| Constraint says | Test |
|---|---|
| `1 ≤ n` | single element |
| `0 ≤ n` | empty input |
| values can be negative | all negative, mixed signs |
| values can be zero | zeros in every position |
| duplicates allowed | all identical elements |
| may be sorted | already sorted, reverse sorted |
| `n ≤ 10⁵` | the maximum size, for the time budget |

### Plus the structural classes

- **Empty**: `null`, `""`, `[]` — three different things.
- **One element**, then **two** — most off-by-ones show up at two.
- **Odd and even lengths** — anything with midpoints, pairing, or halving.
- **Boundaries**: the first and last positions, since that is where index errors live.
- **No-solution** — exercise the Error / N/A behaviour you agreed.
- **Already-correct input** — does it stay correct, or does one pass break it?

### Trace one by hand

Pick the smallest interesting case and walk your algorithm through it line by line, updating every
variable in Maintenance. This finds more bugs per minute than any other activity in the interview,
and it is the only way to catch a wrong invariant before the judge does.

---

## Worked example

**Prompt:** move all zeroes in an array to the end, keeping the relative order of the non-zeroes,
in place.

| Area | Filled in |
|---|---|
| **Problem** | Rearrange in place so non-zeroes keep their order at the front and zeroes follow. |
| **Constraints** | `1 ≤ n ≤ 10⁴`; values fit in 32 bits, may be negative; duplicates allowed; unsorted; **must** be in place; O(1) extra space implied by "in place". |
| **Inputs** | `nums: int[]`, length n. |
| **Return** | `void` — the input array is the output. |
| **Error / N/A** | All zeroes → unchanged. No zeroes → unchanged. Empty → no-op, not an error. |
| **Maintenance** | `write` = index of the next slot for a non-zero. Invariant: after reading index `i`, `nums[0..write)` holds every non-zero seen so far, in order. |
| **Ideas** | ① Stable partition into a new array, copy back — T O(n), S O(n). Rejected: not in place. ② Repeatedly find a zero and shift the tail left — T O(n²), S O(1). Too slow at n = 10⁴. ③ Two pointers: `write` lags `read`; copy each non-zero forward, then fill the tail with zeroes — T O(n), S O(1). **Agreed.** |
| **Tests** | `[]` · `[0]` · `[1]` · `[0,0,0]` · `[1,2,3]` · `[0,1,0,3,12]` · `[1,0,1,0]` · 10⁴ elements. |

Only now does the code get written — and it is short, because every decision in it was already
made:

```python
def move_zeroes(nums: list[int]) -> None:
    write = 0
    for read in range(len(nums)):
        if nums[read] != 0:
            nums[write] = nums[read]
            write += 1          # the Maintenance step — easy to forget
    for i in range(write, len(nums)):
        nums[i] = 0             # the after-the-loop step — also easy to forget
```

Both comments mark lines that came straight from the Maintenance area. That is what the area is
for.

---

## Common failure modes

<div style="border-left:4px solid #8e1515;background:rgba(142,21,21,0.08);padding:0.6rem 1rem;border-radius:0 0.5rem 0.5rem 0;margin:1.25rem 0">

⚠️ **Filling it in silently.** The canvas is a script for a conversation, not paperwork. Say each
area out loud as you write it. Half its value is that the interviewer can correct you cheaply.

⚠️ **Skipping the brute force** because it is "obvious". The interviewer cannot see that it was
obvious to you.

⚠️ **Treating it as a form.** If an area is genuinely empty — no meaningful error case, say —
write "none, guaranteed by the constraints" and move on. Do not invent content.

⚠️ **Filling it in after coding.** Then it is documentation, and it prevents nothing.

⚠️ **Spending too long.** Aim for five to eight minutes on the whole canvas in a
forty-five-minute interview. Constraints and Ideas deserve most of it; Inputs and Return should
take under a minute each.

</div>

---

## What the canvas is not for

It is a tool for **algorithmic** problems with a defined input, a defined output and a correctness
criterion. It is the wrong shape for:

- **System design** — no single function, no return value; use a different frame (requirements,
  estimation, high-level design, deep dives, bottlenecks).
- **Object-oriented design** — the output is a class model, not an algorithm.
- **Debugging an existing system** — you are working backwards from a symptom.
- **Open-ended data or ML questions** — the success criterion is itself under discussion.

Knowing when a tool does not apply is part of using it well.

---

## Practising it

The canvas is a habit, and habits need reps. Fill it in for problems you already know how to solve
— that is when it feels pointless and is doing the most work, because you are training the
sequence rather than discovering the answer.

In Synapse, the **Think** tab on any problem page keeps each canvas you save as a timestamped entry
against that problem, so you can compare how you framed a problem before solving it with how it
actually went. Saved entries can be exported as JSON if you want them elsewhere.

---

## Sources

This lesson expands on two write-ups, and credits both:

- **HiredInTech — The Algorithm Design Canvas**, and its
  [Common Constraints handout (PDF)](https://www.hiredintech.com/files/the-common-constraints-handout.pdf).
  The original four-area canvas (Constraints, Ideas, Complexities, Code) and the constraint
  checklist this lesson's Constraints section builds on.
- **Startup Next Door — [My Algorithm Design Canvas](https://startupnextdoor.com/my-algorithm-design-canvas/)**.
  The extended eight-area version — the source of the Problem, Inputs, Return, Error / N/A and
  Maintenance areas used here.

Added here and not in either source: the N-to-complexity budget table, overflow and floating-point
as first-class constraints, the invariant formulation of Maintenance, the auxiliary-versus-total
space rules, deriving test cases systematically from the constraints, time-boxing, and the note on
where the canvas does not apply.
