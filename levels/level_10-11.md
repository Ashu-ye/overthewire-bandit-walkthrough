# Bandit Level 10 → Level 11

**Goal:** The password for the next level is stored in `data.txt`, which contains Base64-encoded data.

## What is Base64?

Base64 is a way to turn binary data (images, files, raw bytes) into plain text made of 64 printable characters. This makes the data safe to send in places that only handle text, like emails or web pages.

### How it works

- **Regrouping bits:** It takes the data in 8-bit bytes and regroups the bits into 6-bit chunks.
- **The alphabet:** Each 6-bit chunk maps to one of 64 characters: `A-Z`, `a-z`, `0-9`, plus `+` and `/`. The `=` character is added at the end as padding when needed.
- **Size increase:** 3 bytes of original data become 4 Base64 characters, so the encoded text is about 33% bigger.
- **URL-safe version:** A variation uses `-` and `_` instead of `+` and `/`, and drops the `=` padding, so it's safe to put in URLs and file paths.

Base64 is **encoding, not encryption**. There's no key or secret, and anyone can decode it.

## Solution

**Step 1: Look at the file**

```bash
cat data.txt
```

You'll see one long line of letters and numbers that ends with `==`. That ending is a common sign of Base64.

**Step 2: Decode it**

```bash
base64 -d data.txt
```

`-d` means decode. (`cat data.txt | base64 -d` also works, but passing the file straight to `base64` is shorter.)

The output is a sentence that ends with the password:

```
The password is [REDACTED]
```

Copy the password and save it somewhere safe.

## Log in to Level 11

First run `exit` to leave the Level 10 session. Then run this from your own machine:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- Base64 turns binary data into printable text, and `base64 -d` decodes it
- A trailing `=` or `==` is a common hint that data is Base64
- Encoding isn't security. Anyone can reverse it, so never use it to hide secrets
