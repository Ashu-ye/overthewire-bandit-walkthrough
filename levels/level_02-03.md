# Bandit Level 2 → Level 3

**Goal:** The password for the next level is stored in a file called `--spaces in this filename--` in the home directory.

## The tricky part

This filename causes two problems at once:

1. **Spaces.** The shell uses spaces to separate a command from its arguments. So `cat --spaces in this filename--` looks like several different arguments, not one file.
2. **Leading dashes.** The name starts with `--`, so commands like `cat` read it as an option (flag), not a filename.

You need to fix both.

## Ways to handle spaces in a filename

1. **Put the name in quotes.** Single (`'`) or double (`"`) quotes tell the shell to treat everything inside as one argument.

   ```bash
   cat "My project.txt"
   ```

2. **Escape each space with a backslash.** A `\` before a space means "this space is part of the name".

   ```bash
   cat My\ project.txt
   ```

3. **Use Tab completion.** Type the first few letters and press `Tab`. The shell completes the name and adds the backslashes for you.

## Ways to handle a leading dash

1. **Add `./` in front of the name.** The command then sees a path, not an option.
2. **Use `--` (end of options).** Everything after `--` is treated as a filename, not a flag.

## Solution

**Step 1: List the files**

```bash
ls
```

You'll see `--spaces in this filename--`.

**Step 2: Read it**

Quotes for the spaces, plus `--` for the dashes:

```bash
cat -- "--spaces in this filename--"
```

Other options that also work:

```bash
cat ./"--spaces in this filename--"
cat ./--spaces\ in\ this\ filename--
```

Copy the password and save it somewhere safe.

## Log in to Level 3

First run `exit` to leave the Level 2 session. Then run this from your own machine:

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- A filename can have more than one problem at once, so check each one (spaces and leading dashes here)
- Quotes or backslashes fix spaces; `./` or `--` fix leading dashes
- `ls` shows the exact filename, so read it carefully before typing the command
