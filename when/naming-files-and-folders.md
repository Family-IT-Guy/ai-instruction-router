# Naming files and folders

Opened because a file or folder is being created, named or renamed, or a project's folders are being laid out. The reader of every name here is the model, and that changes what a good name is.

## Why the usual conventions do not apply

`src/`, `lib/`, `utils/`, `docs/` and short lowercase names all come from one reader: a person with a file browser, scanning alphabetically, holding a mental model built over months, typing paths by hand. Short names are cheap to type, and the missing context lives in that person's head.

The model has none of those properties. It holds no memory between sessions. It does not scan alphabetically; it globs, greps and reads a whole tree at once. It types nothing by hand. It pays a few tokens for a long name and nothing else. So the name is the entire signal available at the moment of deciding what to open, and there is no head for the missing context to live in.

Measured: renaming six skills, one word each and nothing else (same descriptions, same prompts, same model), moved them from 0 of 6 firing to 3 of 6. The three that started firing were renamed to words the user actually types. The three that did not were renamed to the correct technical term.

## Name for the words that will be in context at the moment of need

Not what the thing contains, not what it produces, not the canonical term for it: the words someone would use when they need it. The failure has a signature: a name is right, precise, and never matches. `download-video` is correct, and the user types "grab this YouTube video." Where the two pull apart, the user's words win. Where it is unclear which words those are, read the user's past requests.

A name is also spoken back to the user in every reply about the thing, so a figurative name becomes vocabulary they have to think in. Name things in literal words for that reason as well as for retrieval.

## Long is fine; vague is not

`decided-do-not-relitigate.md` says when to open it and when not to; `decisions.md` does not. `how-information-reaches-a-session.md` says what question it answers; `architecture.md` says nothing. File systems allow names many times longer than any convention uses, so pick a name that reads as a phrase rather than a label.

## Group folders by when a session needs them, not by artifact type

`docs/` versus `deliverables/` versus `evidence/` sorts by what a thing is. The session's question is whether it needs this now, and sorting by type answers that only by accident. Group by need instead: what every session must read, what a session working in this area needs, what is consulted only when a specific question arises, and what is kept as a record and rarely opened.

## Each folder says what it answers

A folder's main file (a project's `CLAUDE.md`, otherwise its `README.md`) opens with one sentence saying what the folder answers, because a session choosing where to look reads that sentence and the folder name, and nothing else. When a name seems to need that sentence to be understood, first ask whether the name is wrong: a rename beats an annotation, and an annotation beats nothing.

## A file is current state or a dated record

Current-state files are rewritten in place. Narrative that stops being current moves under a dated name or into a records folder, or is deleted, because a handoff file that outlives its session reads as current to every later session.

## Where the tree is not the model's to name

A build tool owns part of its own tree: `src/`, `tests/`, `node_modules/`, folders a framework requires. Match the tooling exactly there; these conventions govern everything the tooling does not claim.

## Improve on touch, never by campaign

A session working in a folder that breaks these conventions fixes what it touches as part of its own work: one opening sentence, one rename proposal, one stale file moved. Propose renames to the user; never rename as a side effect, because other files and sessions point at the old name.
