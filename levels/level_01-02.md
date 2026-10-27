# Bandit Level 1 → Level 2

**Goal:** The password for the next level is stored in a file called `-` in the home directory.

## The tricky part

If you just run `cat -`, nothing useful happens. The terminal looks stuck because `cat` waits for you to type something. That's because most Linux commands treat a lone `-` as "read from standard input (stdin)", not as a filename. (Press `Ctrl+C` to get out.)

More generally, a filename that starts with a dash is hard to use because commands read a leading dash as an option or flag, not as a filename.

## Ways to read a file that starts with a dash

1. **Add `./` in front of the name.**
   `./` means "the current directory", so the command sees a path instead of a flag.

   ```bash
   cat ./-filename
   ```

2. **Use `--` (end of options).**
   In most commands, `--` means "no more options after this". Everything after it is treated as a filename.

   ```bash
   cat -- -filename
   ```

3. **Redirect the file into the command.**
   The shell opens the file for you, so `cat` never has to read the name.

   ```bash
   cat < -filename
   ```

Note: for this level the file is named just `-`, and `cat` still treats a lone `-` as stdin even after `--`. So method 2 won't work here. Use method 1 or 3.

## Solution

**Step 1: List the files**

```bash
ls
```

You'll see a file named `-`.

**Step 2: Read it**

```bash
cat ./-
```

Or, using redirection:

```bash
cat < -
```

Copy the password and save it somewhere safe.

## Log in to Level 2

First run `exit` to leave the Level 1 session. Then run this from your own machine:

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- A leading `-` in a filename gets read as an option
- `./` and `--` are two ways to avoid that
- A lone `-` usually means stdin, so `cat -` just waits for input
