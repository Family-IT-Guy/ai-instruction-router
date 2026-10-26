# claude-code-instruction-router

A small set of instruction files for Claude Code. Three load in every session; the rest are opened only at the moment they apply. These are the working principles Ben Gillenwater uses with Claude every day, with his personal details taken out, published by Family IT Guy.

## How it works

The three that load in every session:

- `CONTRACT.md` holds the principles: who decides, what to optimize for, what counts as evidence, how to build, and how files and words are written.
- `ROUTER.md` is a table of moments. Each row names something that will be present when it applies (a claim that work is done, a number being written, a rule about to be edited) and what to do then, which is often "open this file".
- `HARD.md` lists the tools and vendors where the obvious reading of what they report is wrong, one row each, and a row applies whenever that name shows up in the work. It starts empty. Add a row the first time acting on a tool's obvious reading costs you something.

The procedures in `when/` load only when a router row opens them. Each row is written as "when this happens, do that" because a rule like "don't do X" is rarely acted on: nothing in the work reminds the model of it.

`reply.style.md` is an optional output style that sets how Claude writes its replies to you: result first, every question in one block at the end, and what wasn't checked always stated.

## Install

1. Clone it to `~/.agent`. The router's rows point at files there.

   ```
   git clone https://github.com/Family-IT-Guy/claude-code-instruction-router.git ~/.agent
   ```

2. Choose what you keep. There is a lot here, and not all of it will fit how you work. Start Claude Code inside the folder, so it can read the files without asking about each one:

   ```
   cd ~/.agent && claude
   ```

   Then paste this prompt. Claude goes through each part with you, edits your copy to match what you choose, and then does the install steps with you, asking before each edit.

   ```
   Walk me through the instruction files in ~/.agent before I install them, so I keep only the parts I want.

   Read ~/.agent/README.md and every file in ~/.agent first. Then take the parts one at a time, in this order: CONTRACT.md, ROUTER.md, HARD.md, the procedures in ~/.agent/when/, and reply.style.md. For each part, explain in plain words, section by section, what it makes Claude do and what goes wrong without it, recommend what to keep, and ask me what to change or drop. Wait for my answer before moving to the next part.

   Make the changes I choose in ~/.agent as we go. When I drop a file, a section or a router row, find every line in ~/.agent that points at it, remove or reword each one, and tell me which lines changed. When I drop a router row, check whether a procedure is left with nothing pointing at it, and ask whether to delete it too.

   When every part is done, list what I kept, changed and dropped. Then go through the steps under "Install by hand" in the README one at a time, and ask before each change to ~/.claude.
   ```

## Install by hand

If you'd rather keep everything and install it yourself, these are the steps the prompt walks through.

1. Add this line to `~/.claude/CLAUDE.md`, creating the file if you don't have one. Anything already in that file stays.

   ```
   @~/.agent/CONTRACT.md
   ```

2. Link `ROUTER.md` and `HARD.md` into Claude Code's rules folder, which it loads in every session.

   ```
   mkdir -p ~/.claude/rules
   ln -s ~/.agent/ROUTER.md ~/.claude/rules/ROUTER.md
   ln -s ~/.agent/HARD.md ~/.claude/rules/HARD.md
   ```

3. Let Claude open the procedures without asking each time. In `~/.claude/settings.json`, add `"Read(~/.agent/**)"` to the `permissions.allow` list. If the file doesn't exist yet, this is the whole file:

   ```json
   {
     "permissions": {
       "allow": ["Read(~/.agent/**)"]
     }
   }
   ```

   Without it, Claude asks permission each time a rule opens one of the procedures.

4. Optional, the reply style: link it, then add `"outputStyle": "reply"` to `~/.claude/settings.json`.

   ```
   mkdir -p ~/.claude/output-styles
   ln -s ~/.agent/reply.style.md ~/.claude/output-styles/reply.md
   ```

Restart Claude Code. The first time you ask it to do something substantive, it asks whether you're in thinking or working mode: thinking means discuss and plan, working means carry out what you've agreed.

## Making it yours

- Delete any rule that doesn't fit how you work. The files are plain text.
- `~/.agent` is your own copy. Later changes to this repo don't reach it by themselves, and `git pull` will ask you to merge them with your edits.
- Rules for one project go in that project's own `CLAUDE.md`, not in the router.
- To add a rule, ask Claude to write one with the `rule-creator` plugin, which writes rows in this "when this happens, do that" shape and tells you how to check them. It and `skill-author` are in the [Family IT Guy plugin marketplace](https://github.com/Family-IT-Guy/plugins).

## Removing it

Delete the `@~/.agent/CONTRACT.md` line from `~/.claude/CLAUDE.md`, the two links in `~/.claude/rules`, the output-style link if you made one, and the `~/.agent` folder.
