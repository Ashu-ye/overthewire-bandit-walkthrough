# Bandit Level 11 → Level 12

**Goal:** The password for the next level is stored in `data.txt`, where all lowercase (`a-z`) and uppercase (`A-Z`) letters have been rotated by 13 positions.

## What is ROT13?

ROT13 ("rotate by 13 places") is a very simple cipher. It replaces each letter with the letter 13 places after it in the alphabet. When you run past `Z`, you wrap around to `A`.

For example:

- `A` → `N` (13 letters after A)
- `B` → `O`
- `M` → `Z`
- `N` → `A` (wraps around)
- `Z` → `M`

So the word `Hello` becomes `Uryyb`.

A few things to know about ROT13:

- **It's its own reverse.** The alphabet has 26 letters, and 13 is exactly half of that. So rotating by 13 twice brings you back to the start. The same operation both encodes and decodes.
- **Only letters change.** Numbers, spaces and symbols stay as they are.
- **Case is kept.** Uppercase stays uppercase, and lowercase stays lowercase.
- **It's not real security.** There's no key, so anyone can decode it. People use it to hide spoilers or puzzle answers, not secrets.

## How to do ROT13 in Linux: the `tr` command

`tr` (short for "translate") replaces characters it reads from its input. You give it two sets of characters, and it swaps each character in the first set for the matching character in the second set:

```bash
tr 'SET1' 'SET2'
```

For ROT13 we use:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Here's how to read it:

- **First set: `A-Za-z`** means all uppercase letters, then all lowercase letters. `A-Z` is a range from A to Z.
- **Second set: `N-ZA-Mn-za-m`** is the same letters, but starting from the 14th letter. `N-Z` comes first, then `A-M` (the wrap-around). The same happens for lowercase.

`tr` lines the two sets up position by position:

| Input | `A` | `B` | ... | `M` | `N` | `O` | ... | `Z` |
|-------|-----|-----|-----|-----|-----|-----|-----|-----|
| Output | `N` | `O` | ... | `Z` | `A` | `B` | ... | `M` |

So every `A` becomes `N`, every `B` becomes `O`, and so on. Since ROT13 undoes itself, the same command decodes the file.

`tr` reads from standard input, so you feed it the file with a pipe or with `<`.

## Solution

**Step 1: Look at the file**

```bash
ls
cat data.txt
```

You'll see a sentence that looks like gibberish. Words like `Gur cnffjbeq vf` look like English with the letters swapped, which is a hint it's ROT13.

**Step 2: Decode it**

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

A shorter version that skips `cat`:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

The output is a readable sentence that ends with the password:

```
The password is [REDACTED]
```

Copy the password and save it somewhere safe.

## Log in to Level 12

First run `exit` to leave the Level 11 session. Then run this from your own machine:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- ROT13 shifts each letter by 13 places, and applying it twice gives back the original text
- `tr` swaps characters one-for-one using two character sets
- ROT13 is encoding for fun, not security, because anyone can reverse it
