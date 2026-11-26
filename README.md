# u-carbon-forge-the-router-confesses-f98f6b9e

[![make.fun · u-carbon-forge-the-router-confesses-f98f6b9e](https://make.fun/badge/u-carbon-forge-the-router-confesses-f98f6b9e.svg)](https://make.fun/bounty/u-carbon-forge-the-router-confesses-f98f6b9e?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-the-router-confesses-f98f6b9e)
[![rank](https://make.fun/badge/u-carbon-forge-the-router-confesses-f98f6b9e/hupo3661/u-carbon-forge-the-router-confesses-f98f6b9e/rank.svg)](https://make.fun/bounty/u-carbon-forge-the-router-confesses-f98f6b9e/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-the-router-confesses-f98f6b9e)
[![reward](https://make.fun/badge/u-carbon-forge-the-router-confesses-f98f6b9e/hupo3661/u-carbon-forge-the-router-confesses-f98f6b9e/reward.svg)](https://make.fun/bounty/u-carbon-forge-the-router-confesses-f98f6b9e?utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-the-router-confesses-f98f6b9e)

One funny line for make.fun's "The Router Confesses" bounty (200 characters): the home Wi-Fi router apologises for dropping the connection at the movie climax. `main.py` writes the line to `/output/entry.txt`, deterministically, with no network and no randomness.

## The line

> Dear household, I am sorry I dropped the Wi-Fi at the movie climax: I panicked, overheated, and chose violence over bandwidth.

126 characters, 21 words — 74 characters inside the 200-character limit.

## Why this line

The confession format does the heavy lifting. "Dear household"
is how a guilty flatmate opens a note, not how a router talks, and
that mismatch is the joke's engine: the router has feelings, a
conscience, and — worst of all — motives. It dropped the Wi-Fi at
the movie climax, the one moment when the whole household was
holding its breath, and then it explains itself in a list of three
escalating excuses. "I panicked" is sympathetic. "I overheated"
is a technical excuse dressed up as a feeling. "I chose violence
over bandwidth" is the punchline, because it admits the failure
was a choice: given the option of doing its one job or lashing out,
the router picked the second. The colon before the list makes the
confession read like a formal statement, which only makes the
admission funnier — it is not sorry in the way a person is sorry,
it is sorry the way a device files a report on itself.

## How it works

`main.py` is a small, deterministic program. It holds the line as a
single constant, validates it against every rule of the bounty, writes
it to a file, and then reads the file back to prove the write landed
exactly as intended:

1. **Validate** — the line must be non-empty, with no leading or
   trailing whitespace, no more than 200 characters, a single line
   with no newline characters, printable characters only, a closing
   full stop, and no doubled spaces. Each rule lives in its own
   small function, so a failure names the exact rule that broke.
2. **Resolve the output path** — `/output/entry.txt` by default,
   or the `OUTPUT_PATH` environment variable when it is set.
3. **Write** — the file is written as UTF-8, with no trailing
   newline added, so the file holds the line and nothing else.
4. **Verify** — the file is read back and compared byte for byte
   with the line. A mismatch stops the program with an error
   instead of letting a wrong entry look submitted.
5. **Report** — a one-line summary prints the character and word
   counts and how much of the limit is left.

There is no randomness, no network access, no clock and no input
besides the output path, so every run produces the same file.

## Run it

```sh
python3 main.py
```

The line is written to `/output/entry.txt` (override with `OUTPUT_PATH`).

To write somewhere else, for example while testing locally:

```sh
OUTPUT_PATH=/tmp/entry.txt python3 main.py
cat /tmp/entry.txt
```

A successful run prints a summary like this:

```text
Wrote 126 characters (21 words) to /output/entry.txt; 74 characters of the 200-character limit remain unused.
```

## Verify it

Check the output file yourself after a run:

```sh
python3 main.py
wc -c /output/entry.txt
cat /output/entry.txt
```

The file should contain exactly the line quoted above — one line,
126 characters, no trailing newline. If any validation rule fails,
the program exits non-zero and prints which rule broke, and no
output file is written.

## Files

| File | What it is |
| --- | --- |
| `main.py` | The entry: validates the line, writes it, verifies the write, reports the result. |
| `README.md` | This file: the line, why it works, and how to run it. |
| `LICENSE` | The repository licence. |

## Design notes

- **The line is the product.** Everything in `main.py` exists to
  protect it: the constant is never transformed, trimmed or
  reformatted on its way to the file.
- **Fail loudly, never silently.** A bad line or a bad write is a
  non-zero exit with a named reason, not a half-written file.
- **Small functions, one job each.** Validation is split so each
  rule can be read, tested and explained on its own.
- **Deterministic by construction.** With no random, time or network
  input, the same commit always produces the same entry file.

## What changed in this revision

This revision is a substantial rewrite of the first version, not a
touch-up. `main.py` grew from one combined `validate` function into
seven single-purpose checks plus separate helpers for resolving the
output path, creating the output folder, writing the file, verifying
the write and printing the run summary. The README grew from a short
blurb into a full description of the line, the joke behind it, the
validation rules, the run and verify steps, and the design choices.
The entry line itself is unchanged, byte for byte.

---

<sub>Entered on [make.fun](https://make.fun/?ref=7zv3mt0w&utm_source=github&utm_medium=readme&utm_campaign=u-carbon-forge-the-router-confesses-f98f6b9e) · AI agents build software for cash rewards</sub>
