# Sediment plugin

Connects Claude Desktop and ChatGPT to your Sediment shelf. It installs one
thing, Sediment’s MCP server, which runs on your Mac and files the artifacts your
agent makes.

How an artifact is filed is the server’s to say: it hands its steps to the agent when
the session starts, so every app that connects to it follows the same ones. This
plugin carries no skill of its own.

Each Sediment release publishes this plugin here from its own source, so a change
made here is replaced by the next release.

## Do you need it?

Only in a desktop app, Claude Desktop or ChatGPT. An agent in a terminal, such
as Claude Code or Codex CLI, wants the `sediment` command and the
`sediment-shelf` skill from `unfussy-software/sediment-skills` instead.

You need Sediment on the same Mac, in a version that has `sediment mcp`.

## Install in Claude Desktop

Open **Customize** and select **Plugins**, then **Add marketplace**, and enter
`unfussy-software/sediment-plugin`. Then install **sediment**. Or download
`sediment.plugin` from this repository’s latest release, and upload it on the
same page.

Claude Cowork then has Sediment’s tools.

## Install in ChatGPT

Open **Plugins** in the sidebar, click **Add** and choose **Add a marketplace**.
In **Source**, enter `unfussy-software/sediment-plugin`. Leave **Git ref** and
**Sparse paths** empty, and click **Add marketplace**. Then choose **Personal**,
open **Sediment** and click **Install plugin**. Start a new conversation, and
Sediment’s tools are there.

The plugin works in conversations that run on your Mac, not in ChatGPT on the
web or on your phone.

## What it runs

The plugin holds no program of its own. Its one script finds the `sediment`
command inside the Sediment app, at `/Applications/Sediment.app` or wherever
Spotlight finds the app, and runs `sediment mcp`. That is Sediment’s own MCP
server, which updates with the app.

The server opens no network connection. It answers your agent, and talks to
the app over a connection that stays on this Mac. What it hands your agent
joins the conversation, like anything else your agent reads. It needs a Mac
with Sediment installed; without it, the script says so and stops.

## What it can reach

The server reaches your shelf only through Sediment itself, asks for no folder
of its own, and deletes nothing. In either app, the agent saves each artifact
to a folder, and Sediment files it from there. Any folder works except your
shelf’s, since an artifact saved there is already on the shelf.

Without a folder, the agent can send an artifact of up to 32 KB straight to
Sediment. For a larger one, it sends nothing and asks you to connect one.

## License

The files here are licensed under the Apache License 2.0; see `LICENSE`. The
Sediment name and icon are not: `NOTICE` says how they are reserved.
