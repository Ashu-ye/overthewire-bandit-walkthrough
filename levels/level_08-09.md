# Bandit Level 8 → Level 9

**Goal:** The password for the next level is stored in `data.txt`. It's the only line of text that appears exactly once in the file.

## The tricky part

We don't know anything about the password except that its line is unique. Every other line appears more than once. To find it, we need two commands: `sort` and `uniq`.

## `sort`

`sort` arranges lines of text in order. By default it sorts alphabetically, from A to Z, and prints the result without changing the original file.

Say `fruits.txt` contains:

```
banana
apple
cherry
```

Running:

```bash
sort fruits.txt
```

gives:

```
apple
banana
cherry
```

## `uniq`

`uniq` filters or reports repeated lines in text. Useful flags:

- `-u` prints only the lines that appear exactly once
- `-d` prints only the lines that appear more than once
- `-c` puts a count in front of each line

**Important:** `uniq` only spots duplicates that are **next to each other**. So you almost always run `sort` first, so identical lines end up side by side. You join the two commands with a pipe (`|`), which sends the output of one command into the next.

## Solution

**Step 1: List the files**

```bash
ls
```

You'll see `data.txt`.

**Step 2: Find the unique line**

```bash
sort data.txt | uniq -u
```

How it works:

- `sort data.txt` puts identical lines next to each other
- `|` passes that sorted output to `uniq`
- `uniq -u` prints only the line that appears once

That line is the password. Copy it and save it somewhere safe.

## Log in to Level 9

First run `exit` to leave the Level 8 session. Then run this from your own machine:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `uniq` only compares neighboring lines, so you need `sort` first
- `uniq -u` shows lines that appear once, and `uniq -d` shows repeated ones
- A pipe (`|`) lets you chain commands so the output of one becomes the input of the next
