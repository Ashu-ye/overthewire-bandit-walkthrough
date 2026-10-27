# Bandit Level 12 → Level 13

**Goal:** The password for the next level is stored in `data.txt`, which is a hexdump of a file that has been compressed over and over. The level suggests making a working folder under `/tmp` and using `cp` and `mv` to copy and rename the file.

> **Difficulty:** This is one of the trickiest and most frustrating levels so far. There's no single command that solves it. You have to repeat the same check-and-extract steps many times, and one wrong step (like forgetting to rename a file) stops you with an error. It feels long, but once you see the loop, each round is easy.

## The tricky part

The file isn't just compressed once. It was hexdumped, and then compressed many times using different tools (gzip, bzip2 and tar). You can't know which tool was used for each layer by looking at the file, so you have to check at every step.

Here's what you need to know:

- **Hexdump:** a text version of a binary file, where every byte is written as two hex digits. `xxd -r` reverses it.
- **gzip / bzip2:** compression tools. They shrink a single file.
- **tar:** an archive format. It bundles files together. Unlike gzip and bzip2, extracting a tar creates a **new file with a different name**.
- **`file`:** tells you what type a file is without opening it. It's the key command for this level.

## Setup: make a working folder

You can't create files in your home directory here, so work in `/tmp`.

```bash
mktemp -d                # creates a folder with a hard-to-guess name and prints it
cd /tmp/tmp.XXXXXXXXXX   # use the path it printed
cp ~/data.txt .          # copy the file into the working folder
```

`mktemp -d` is better than picking a name yourself, because other players use `/tmp` too and a guessable name could clash.

## Solution

**Step 1: Undo the hexdump (only once)**

```bash
xxd -r data.txt > data
```

**Step 2: Check the file type**

```bash
file data
```

**Step 3: Decompress or extract based on what `file` says**

| `file` says | Run |
|-------------|-----|
| gzip compressed data | `mv data data.gz`, then `gzip -d data.gz` |
| bzip2 compressed data | `mv data data.bz2`, then `bzip2 -d data.bz2` |
| POSIX tar archive | `tar -xvf data` (creates a **new** file, check its name with the output or `ls`) |
| ASCII text | done, read it with `cat` |

Why rename? `gzip -d` refuses to work on a file without a `.gz` ending ("unknown suffix"). `bzip2 -d` doesn't refuse, but it saves the result to a file ending in `.out` instead of replacing the original, which gets confusing. Renaming first keeps things clean. `tar` doesn't need a rename.

**Step 4: Repeat**

Run `file` on the result and pick the matching row again. Do this until `file` says `ASCII text`.

### The layers I went through

| # | `file` said | What I ran |
|---|-------------|-----------|
| 1 | (hexdump) | `xxd -r data.txt > data` |
| 2 | gzip | `mv data data.gz` and `gzip -d data.gz` |
| 3 | bzip2 | `mv data data.bz2` and `bzip2 -d data.bz2` |
| 4 | gzip | `mv data data.gz` and `gzip -d data.gz` |
| 5 | tar | `tar -xvf data` (made `data5.bin`) |
| 6 | tar | `tar -xvf data5.bin` (made `data6.bin`) |
| 7 | bzip2 | `mv data6.bin data6.bz2` and `bzip2 -d data6.bz2` (made `data6`) |
| 8 | tar | `tar -xvf data6` (made `data8.bin`) |
| 9 | gzip | `mv data8.bin data8.gz` and `gzip -d data8.gz` (made `data8`) |
| 10 | ASCII text | `cat data8` |

Your filenames may differ a little, so always check with `ls` and `file`.

The last file is plain text that ends with the password. Copy it and save it somewhere safe.

## Tips for this level

- Always run `file` before doing anything. Never guess the layer type.
- After a `tar` extraction, the new file has a different name, so run `ls` to find it.
- If you get lost, `ls` and `file *` show what's in your folder.
- Don't use `cat` on binary files. It floods the screen with junk. If your terminal gets garbled, type `reset`.
- Clean up when you're done: `rm -r /tmp/tmp.XXXXXXXXXX`

## Log in to Level 13

First run `exit` to leave the Level 12 session. Then run this from your own machine:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `xxd -r` turns a hexdump back into binary data
- `file` identifies a file's real type, which is how you decide the next step
- gzip and bzip2 handle one file, while tar bundles files and extracts to a new filename
- Long tasks like this are easier when you find the repeating loop instead of treating each layer as a new problem
