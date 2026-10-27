# ai-instruction-router

A small set of instruction files for any AI model and any tool you use it in. Three load in every session; the rest are opened only at the moment they apply. These are the working principles Ben Gillenwater uses with his AI tools every day, with his personal details taken out, published by Family IT Guy.

## How it works

The three that load in every session:

- `CONTRACT.md` holds the principles: who decides, what to optimize for, what counts as evidence, how to build, and how files and words are written.
- `ROUTER.md` is a table of moments. Each row names something that will be present when it applies (a claim that work is done, a number being written, a rule about to be edited) and what to do then, which is often "open this file".
- `HARD.md` lists the tools and vendors where the obvious reading of what they report is wrong, one row each, and a row applies whenever that name shows up in the work. It starts empty. Add a row the first time acting on a tool's obvious reading costs you something.

The procedures in `when/` are opened only when a router row points at them. Each row is written as "when this happens, do that" because a rule like "don't do X" is rarely acted on: nothing in the work reminds the model of it.

`reply.style.md` is optional. It sets how the AI writes its replies to you: result first, every question in one block at the end, and what wasn't checked always stated.

Two skills go with these files: [rule-creator](https://github.com/Family-IT-Guy/rule-creator), which writes and audits rules in this "when this happens, do that" shape, and [skill-author](https://github.com/Family-IT-Guy/skill-author), which builds skills the model picks up and follows.

## Files

Loaded in every session: `CONTRACT.md`, `ROUTER.md`, `HARD.md`.

Opened when a router row points at them, in `when/`:

- `verify.md`: checking work before calling it done
- `testing-scope.md`: what a test or check has to establish
- `adversary-review.md`: when work needs an independent reader
- `state-capture.md`: where a new fact goes
- `contracts.md`: contracts and negotiations
- `self-change.md`: creating, editing or removing rules, skills and hooks
- `outbound.md`: writing for anyone other than you
- `naming-files-and-folders.md`: naming files and laying out folders

Optional: `reply.style.md`.

The skills: `skills/rule-creator/SKILL.md` and `skills/rule-creator/REFERENCE.md` in [rule-creator](https://github.com/Family-IT-Guy/rule-creator); `skills/skill-author/SKILL.md`, `skills/writing-great-skills/SKILL.md` and `skills/writing-great-skills/GLOSSARY.md` in [skill-author](https://github.com/Family-IT-Guy/skill-author).

## Set it up

Your AI does the setup with you. Paste the prompt below into the AI tool you use. It works in tools that edit files on your computer, in chat apps, and in tools you've built yourself.

If your tool can work with files on your computer, download this repository first so it can read the files directly:

```
git clone https://github.com/Family-IT-Guy/ai-instruction-router.git ~/.agent
```

Any folder works; tell the AI where you put it. If your tool can't read files on your computer, skip this. The AI fetches the files from this page, or asks you to upload them.

The AI takes you through each piece, checks it against the instructions you already have, and adds the pieces you choose in the form your tool uses. It saves a copy of anything before changing it and asks before each change.

```
Help me decide which parts of the instruction set at https://github.com/Family-IT-Guy/ai-instruction-router to adopt, check them against my current setup, and add the ones I choose to the AI tool I'm using now.

1. Get the files listed under "Files" in that repository's README, including the two skills. If you can read the folder ~/.agent on my computer, or a folder I name, read every file in it, and fetch the skills if they aren't there. If not, and you can fetch web pages, fetch each file from https://raw.githubusercontent.com/Family-IT-Guy/<repository>/main/<path>. If you can do neither, tell me exactly which files to upload or paste. Work only from text you have actually read, never from memory or a guess about what a file says.

2. Work out what this tool can do, and tell me what you found: whether you can open a file in the middle of a conversation when you need it, whether this tool keeps files I upload so you can consult them later, or whether it only has a box for standing instructions, and how much text that box holds. Where you can't tell, ask me rather than guess.

3. Read my current setup before recommending anything: the standing instructions, rules, skills or saved memory this tool gives you, and any files where my instructions live. If you can't see them, ask me to paste them. Summarize what I have in a few lines.

4. Take the parts one at a time, in this order: CONTRACT.md, ROUTER.md, HARD.md, the procedures in when/, reply.style.md, then the rule-creator and skill-author skills. For each part, explain in plain words what it makes the AI do and what goes wrong without it. Say whether my current setup already covers it, contradicts it, or lacks it, and quote the line of mine it touches. Recommend keep, merge or skip, ask me what to keep, change or drop, and wait for my answer before the next part. When I drop something, find every line in what I'm keeping that points at it, and remove or reword each one.

5. When every part is decided, list what I kept, changed and dropped. Then show me the plan: each file or setting you will change and the exact text going into it. Fit the plan to what you found in step 2:
   - If you can open files when you need them, keep the procedures as separate files, put CONTRACT, ROUTER and HARD wherever this tool loads instructions in every session, and make every file path in ROUTER point to where the procedures actually are.
   - If this tool asks permission before opening files outside the current folder, add the setting that lets it open the procedures folder without asking, and tell me what you set.
   - If this tool keeps uploaded files, put CONTRACT, ROUTER and HARD in its standing instructions, the procedures in uploaded files, and reword each router row from "open this file" to "consult this file".
   - If there is only a box for standing instructions, condense the parts I kept to fit it, and tell me what the condensing left out.
   - Put the skills wherever this tool loads skills. If it has no such place, give me their text to save or paste.
   - Leave out the block between the --- lines at the top of reply.style.md unless this tool uses it.
   Where a part I kept contradicts a line of mine, ask me which one wins.

6. Before changing anything, save a copy of each file you will change and tell me where it is. Ask before each change. If you can't make a change yourself, give me the exact text and say where to put it.

7. Finish with one question I can ask in a new conversation to see whether it worked, and what a good answer looks like.
```

## Install by hand

If you'd rather do it yourself:

1. Put `CONTRACT.md`, `ROUTER.md` and `HARD.md` wherever your tool loads instructions at the start of every session.
2. Keep the `when/` folder where your AI can open it, and change the paths in `ROUTER.md` if you put it somewhere other than `~/.agent/when/`. If your tool asks permission before opening files outside the current folder, allow that folder in its settings, or it will ask each time a procedure is needed. If your AI can't open files on its own, upload the procedures where it can consult them, or leave them out.
3. Optional: add `reply.style.md` to your standing instructions, or wherever your tool keeps a reply style.

The first time you ask for something substantive, the AI asks whether you're in thinking or working mode: thinking means discuss and plan, working means carry out what you've agreed.

If you use Claude Code, you can also install the two skills from the [Family IT Guy plugin marketplace](https://github.com/Family-IT-Guy/plugins).

## Making it yours

- Delete any rule that doesn't fit how you work. The files are plain text.
- Later changes to this repository don't reach your copy by themselves. Run the prompt again to go through what changed.
- Rules for one project go in that project's own instruction file, not in the router.
- To add a rule, ask your AI to write one with rule-creator, which writes rows in this "when this happens, do that" shape and tells you how to check them.

## Removing it

Restore the copies the setup saved, or delete what it added: the lines in your tool's standing instructions, any uploaded procedure files, the skills, and the `~/.agent` folder if you made one.
