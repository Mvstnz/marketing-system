# Installation Guide (Windows)

This sets up the marketing system on your Windows laptop with **Codex**.
Follow the steps in order. It takes about 15 minutes the first time.
You only do this **once**.

> 💡 If you get stuck on any step, copy the error message and send it to your developer —
> don't guess. Each step tells you how to check it worked before moving on.

---

## What you'll end up with

A `/marketing` command in Codex that creates Instagram posts, newsletters, blog posts,
product descriptions, image prompts, reels, and a content calendar — all in your brand's
voice.

---

## Step 0 — Open a terminal

1. Press the **Windows key**, type **`powershell`**, press **Enter**.
2. A blue/black window opens. This is the "terminal". You'll type commands here.

You don't need to understand it — just copy-paste the commands below and press Enter.

---

## Step 1 — Check that Node.js is installed

In the terminal, type this and press Enter:

```
node -v
```

- ✅ If you see something like `v20.11.0` → Node.js is installed. **Skip to Step 2.**
- ❌ If you see "not recognized" → install Node.js:
  1. Go to **https://nodejs.org**
  2. Download the **"LTS"** version (the big green button on the left).
  3. Run the downloaded file, click **Next → Next → Install** (accept all defaults).
  4. **Close and reopen** the PowerShell window, then run `node -v` again to confirm.

> Note: if Codex already works on this laptop, Node.js is probably already installed.

---

## Step 2 — Download the project

You need the project folder on your laptop. Two options — pick one:

### Option A — Download as ZIP (simplest)
1. Open the project page: **https://github.com/Mvstnz/marketing-system**
2. Click the green **`< > Code`** button → **Download ZIP**.
3. Find the ZIP in your **Downloads**, right-click → **Extract All…**
4. Extract it to a place you'll remember, e.g. `Documents`. You now have a folder named
   something like `marketing-system`.

### Option B — With Git (lets you get updates later with one command)
```
cd $HOME\Documents
git clone https://github.com/Mvstnz/marketing-system.git marketing-system
```
(If `git` is "not recognized", just use Option A.)

---

## Step 3 — Go into the project folder

In the terminal, type (adjust the path if you put it elsewhere):

```
cd $HOME\Documents\marketing-system
```

Check you're in the right place — type `dir` and press Enter. You should see files like
`README.md` and a folder `.agents`.

---

## Step 4 — Install the marketing skills library

This downloads the marketing toolkit the system builds on. Type:

```
npx skills add coreyhaines31/marketingskills
```

- If it asks "Ok to proceed?" type **`y`** and press Enter.
- Wait until it finishes (it prints a list of installed skills).

---

## Step 5 — Open Codex in this folder

Start Codex **from inside the project folder** (so it can see the `/marketing` commands).
In the same terminal, start Codex the way you normally do (e.g. `codex`).

Check it worked: type **`/marketing`**.
- ✅ If it shows a menu ("What would you like to create?") → 🎉 you're set up.
- ❌ If it says the command is unknown → see **Troubleshooting** at the bottom.

---

## Step 6 — Build your Brand Kit (one time)

Before creating content, the system needs to learn your brand. Gather:

1. **Your Shopify products** — in Shopify: **Products → Export → Export** (CSV file).
   Move that CSV file into the `.agents\brand\` folder inside the project.
2. **Your best past posts** — save 10–20 typical **Instagram captions** (English) and
   2–3 **newsletters** (German) as text files into `.agents\brand\samples\`.
   (1–2 blog posts in German too, if you have them.)

Then, in Codex, type:

```
/marketing-setup
```

It will read your files and ask you a few questions in English. At the end it shows you
your brand voice — **read it once and correct anything that sounds wrong.**

---

## Step 7 — Start creating 🎉

Type **`/marketing`** and pick what you want to create.

Whenever you add new products or change style later, run **`/marketing-update`**.

---

## Troubleshooting

- **`/marketing` not recognized in Codex:** make sure you started Codex *inside* the
  `marketing-system` folder (Step 3 + Step 5). The skills live in `.agents\skills\`.
  If it still doesn't appear, run `npx skills add` again and send your developer a
  screenshot.
- **`npx` or `node` not recognized:** redo Step 1 (install Node.js), then close and
  reopen the terminal.
- **`git` not recognized:** use Step 2 Option A (Download ZIP) instead.
- **Anything else:** copy the full error text and send it to your developer.
