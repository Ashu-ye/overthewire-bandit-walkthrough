# Bandit Level 0 → Level 1

**Goal:** Find the password for the next level. It's stored in a file called `readme` in the home directory.

## Solution

**Step 1: Check where you are (optional)**

```bash
pwd
```

When you log in, you start in your home directory, so this just confirms it.

**Step 2: List the files**

```bash
ls
```

You'll see the `readme` file.

**Step 3: Read the file**

```bash
cat readme
```

This prints the password for the next level. Copy it and save it somewhere safe, because you need it to log in to Level 1.

**Step 4: Log out**

```bash
exit
```

Don't skip this. The server blocks SSH connections from inside the server itself (localhost). If you try to log in to the next level while still logged in, you get "Connecting from/to localhost is blocked". Log out first, then run the SSH command from your own machine.

## Log in to Level 1

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `pwd` shows your current directory
- `ls` lists files in a directory
- `cat` prints the contents of a file
