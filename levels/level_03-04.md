# Bandit Level 3 → Level 4

**Goal:** The password for the next level is stored in a hidden file inside the `inhere` directory.

## What are hidden files?

In Linux, a hidden file or directory is one whose name starts with a dot (`.`). These are often called "dotfiles".

Linux skips them in normal directory listings, mostly so you don't accidentally change or delete important settings files. They are not encrypted and have no special permissions. They're just left out of the default `ls` output because of their name.

## Working with hidden files

- **Show them:** `ls -a` (all files) or `ls -la` (all files, long format)
- **Create one:** start the name with a dot, for example `touch .myfile.txt`

## Solution

**Step 1: Go into the directory**

```bash
cd inhere
```

**Step 2: List all files, including hidden ones**

```bash
ls -la
```

A plain `ls` shows nothing here. With `-a`, you'll see the hidden file `...Hiding-From-You`.

**Step 3: Read the file**

```bash
cat ...Hiding-From-You
```

Copy the password and save it somewhere safe.

## Log in to Level 4

First run `exit` to leave the Level 3 session. Then run this from your own machine:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- Files that start with `.` are hidden from a normal `ls`
- `ls -a` shows them, and `ls -la` adds details like permissions and size
- Hidden doesn't mean secure. Anyone can see these files with the right flag
