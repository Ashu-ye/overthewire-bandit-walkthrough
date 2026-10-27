# Bandit Level 7 → Level 8

**Goal:** The password for the next level is stored in the file `data.txt`, next to the word `millionth`.

## The tricky part

If you run `cat data.txt`, you get a huge wall of text, and finding one line by eye is basically impossible. Instead, we search the file for the word we know is on the right line.

## What is `grep`?

`grep` is a command-line tool that searches for text patterns inside files or command output. The name comes from "Global Regular Expression Print". It prints every line that matches your search.

```bash
grep "string_to_find" filename
```

## Solution

**Step 1: List the files**

```bash
ls
```

You'll see `data.txt`.

**Step 2: Search for the word `millionth`**

```bash
grep "millionth" data.txt
```

This prints only the line that contains `millionth`. The output looks like this:

```
millionth    [REDACTED]
```

The password is the text right after the word `millionth`. Copy it and save it somewhere safe.

## Log in to Level 8

First run `exit` to leave the Level 7 session. Then run this from your own machine:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `grep` finds lines that match a word or pattern, so you don't have to read a big file yourself
- Searching for a known keyword is the quickest way to find a value in a huge file
