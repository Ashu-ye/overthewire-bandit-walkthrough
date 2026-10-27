# Bandit Level 4 → Level 5

**Goal:** The password for the next level is stored in the only human-readable file in the `inhere` directory.

## What is a human-readable file?

A file in plain text format that a person can read directly, like a `.txt` file. Other files (images, programs, compressed data) are binary, so they look like random junk if you print them.

## The tricky part

The `inhere` directory has 10 files, `-file00` to `-file09`, and only one has readable text. Two things make this annoying:

1. **The names start with a dash.** Commands read `-file00` as an option, so you need `./` or `--` in front of it. Running `cat "-file00"` gives an "unexpected argument" error.
2. **Using `cat` on binary files is messy.** It dumps garbage on your screen and can even mess up your terminal. If that happens, type `reset` to fix it.

## A better way: the `file` command

The `file` command tells you what type of data each file contains, so you don't have to open them one by one.

## Solution

**Step 1: Go into the directory**

```bash
cd inhere
```

**Step 2: List the files**

```bash
ls
```

You'll see `-file00` through `-file09`.

**Step 3: Check the type of every file**

```bash
file ./*
```

`./*` expands to `./-file00`, `./-file01` and so on. The `./` also stops the dash problem. Most files will be listed as `data`. One will be listed as `ASCII text`, and that's the readable one.

**Step 4: Read that file**

```bash
cat ./-fileXX
```

Replace `-fileXX` with the file that `file` showed as ASCII text. I'm not naming it here so you can find it yourself.

Copy the password and save it somewhere safe.

**Option: Try each file one by one**

You can also run `cat -- "-file00"`, then `-file01`, and so on, but it's slow and fills your screen with garbage. `file ./*` is much faster.

## Log in to Level 5

First run `exit` to leave the Level 4 session. Then run this from your own machine:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `file` shows what type of data a file holds without opening it
- `./*` is a safe way to match filenames that start with a dash
- Don't `cat` unknown files. Binary data can break your terminal display, and `reset` fixes it
