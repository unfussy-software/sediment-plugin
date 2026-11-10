# Sediment for Claude Cowork

Connects Claude Cowork to your Sediment shelf. It installs one thing, Sediment’s
MCP server, which runs on your Mac and files the pages you make in Claude Cowork.

How a page is filed is the server’s to say: it hands its steps to Claude when the
session starts, so every app that connects to it, Claude Cowork included, follows
the same ones. This plugin carries no skill of its own.

Each Sediment release publishes this plugin here from its own source, so a change
made here is replaced by the next release.

## Do you need it?

Only if your agent can’t run the `sediment` command or add an MCP server itself,
as in Claude Cowork. An agent that can run the command wants the `using-sediment`
skill from `unfussy-software/sediment-skills` instead.

You need Sediment on the same Mac, in a version that has `sediment mcp`.

## Install

In Claude Desktop, open **Customize**, select **Plugins**, select **Add marketplace**,
and enter `unfussy-software/sediment-plugin`. Then install **sediment**.

Or download `sediment.plugin` from this repository’s releases, and select the upload
option on the same page.

## What it can reach

The server reaches your shelf only through Sediment itself, and asks for no folder
of its own. Claude files a page from a folder you connect to Claude Cowork, any
folder except your shelf’s, and the server reads it from there and deletes
nothing. With no folder connected, Claude sends a small page directly, and asks
you to connect a folder before it sends a large one.
