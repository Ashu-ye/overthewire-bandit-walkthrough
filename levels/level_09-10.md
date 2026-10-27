# Bandit Level 9 → Level 10

**Goal:** The password for the next level is stored in `data.txt`. It's one of the few human-readable strings in the file, and it comes after several `=` characters.

## The tricky part

`data.txt` is mostly binary data, so printing it with `cat` gives you a mess of random symbols. We need to do two things:

1. Pull out only the readable text with `strings`
2. Filter that text with `grep`

## `strings`

`strings` scans a file and prints the sequences of printable (human-readable) characters it finds. It's great for binary files, because it skips the unreadable parts.

## Solution

**Step 1: Extract the readable text and search for `=`**

```bash
strings data.txt | grep '='
```

`strings` extracts the readable parts, and the pipe (`|`) sends them to `grep`, which keeps only lines containing `=`.

This works, but it also shows random lines that happen to contain a single `=`, like `h_=y` or `Gd;e=`. To cut the noise, search for several equals signs in a row:

```bash
strings data.txt | grep '=='
```

Now you only see the lines that start with a long run of `=`. The output looks like this:

```
========== the
========== password
========== is
========== [REDACTED]
```

The password is on the last line, after the `=` characters. Copy it and save it somewhere safe.

## Log in to Level 10

First run `exit` to leave the Level 9 session. Then run this from your own machine:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `strings` pulls readable text out of binary files
- Piping `strings` into `grep` is a quick way to find a known pattern in binary data
- A more specific search pattern (`==` instead of `=`) cuts down the noise
