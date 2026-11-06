---
name: filing-to-the-shelf
description: Files a page on the user’s Sediment shelf from Cowork, once the user has seen and approved it, and updates a page already filed. Use when the user asks to save, file, shelve or keep an HTML page, or to put it on the shelf, and the `sediment` command can’t run where you are.
---

# Filing to the shelf

Sediment keeps the user’s HTML pages on a shelf on their Mac. Your shell may not
be on that Mac, so you file through this plugin’s tools, in this order every time.

If the tools `outbox` and `add` aren’t available, tell the user to install or
update Sediment, and stop.

## 1. Show the page

Save the page under `/mnt/user-data/outputs/`, so that Cowork shows it. The user
looks at it and asks for changes, for as many rounds as they want. Even when
they’ve asked you to make a page and file it, show it to them first.

## 2. Ask for approval

Once per conversation, call `tags` and `instructions`, and follow what the
instructions say. A shelf can require a tag, so tag with what the shelf already
uses.

Show the user the file name, `description` and tags you’ll file, and ask for
their approval. Once they’ve seen the page, “file it” is approval.

## 3. Get the page to the Mac

1. Hash the approved file: `sha256sum` or `shasum -a 256`. This is `sha256`.
2. Call `outbox` with the `file_name` and `sha256`. It replies with `folder` and
   `copy_path`.
3. Call `get_device_info`. If `folder` isn’t in `connectedFolders`, call
   `device_request_folder_access` for exactly that folder. The user is asked once.
4. Load `device_commit_files`, which appears once a folder is connected, and
   copy the file from `/mnt/user-data/outputs/` to `copy_path`. If `folder` is
   visible to your shell, `cp` does the same job.

If `outbox` says Sediment can’t be reached, tell the user and send nothing.

**If you can’t copy it**, because the tool isn’t there, the user declined, or
`outbox` says the folder can’t be used, you can send the page itself as `content`:

- Up to about 50 KB, pass the file’s exact contents with its `sha256`. This means
  typing the page out, which is slow and uses many tokens, so say so first.
- Over that, don’t try. Tell the user that the page is still in Cowork, and that
  they can save it and drag it onto Sediment. File nothing.

## 4. File it

Call `add` with the `copy_path` as `path`, and the `sha256`, `description` and
tags. If you’re sending the page inline, pass `file_name` and `content` in place
of `path`. A page that doesn’t match its `sha256` isn’t filed.

Tell the user it’s filed, and give them its `link`. Keep the `id` and
`content_hash` from the reply: you need them to file it again.

## 5. File it again

When the user changes a page you’ve filed and approves it again, repeat steps 3
and 4 with `update`, so that it stays one artifact. Pass the `id` and the
`content_hash` you kept as `expected_hash`, and the new `sha256`. Pass
`description` only if it changed; the tags stay.

**In a new conversation** you have no `id`. Call `find` with the file name. If an
artifact has exactly that name, ask the user whether to update it or add a new
page, and take its `id` and `content_hash` from `find`’s reply.

## 6. When a tool refuses

A refusal carries a `code`, a `message` and a `hint`. A hint may name a command
line flag, such as `--tag`: use the matching argument.

- **`content_changed`:** the artifact changed after you last read it. Tell the
  user, and ask what to do. Never retry without calling `find` for a fresh
  `content_hash` and asking first.
- **A refusal that says the current version can’t be restored:** Sediment doesn’t
  keep versions of large pages. Tell the user what the message says.
  Never pass `accept_lost_version` unless the user has agreed.
- **A failed `update` that says the content was replaced:** your page is on the
  shelf, and its copy is still there. Call `find` for the new `content_hash`, then
  call `update` again with the same file. Don’t report it as someone else’s change.
- **Any other refusal after you’ve copied the page:** tell the user the page is still at `copy_path`,
  and that they can drag it onto Sediment.

## Never

- Never write to the shelf folder, or ask for access to it.
- Never ask for access to all of Downloads: only the `folder` that `outbox` gives.
- Never file a page the user hasn’t seen.
- Never shorten or tidy a page when you send it: its hash won’t match.
