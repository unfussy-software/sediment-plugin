# Sediment for Cowork

Files the HTML pages you make in Cowork on your Sediment shelf. Cowork shows you
the page, you ask for changes and approve it, and it goes on the shelf. File it
again and it updates the same artifact.

Each Sediment release publishes this plugin here from its own source, so a change
made here is replaced by the next release.

## Do you need it?

Only if your agent can’t run the `sediment` command, as in Cowork. An agent that
can run it wants the `using-sediment` skill from `unfussy-software/sediment-skills`
instead.

You need Sediment on the same Mac, in a version that has `sediment mcp`.

## Install

In Claude Desktop, open **Customize**, select **Plugins**, select **Add marketplace**,
and enter `unfussy-software/sediment-plugin`. Then install **sediment**.

Or download `sediment.plugin` from this repository’s releases, and select the upload
option on the same page.

## What it can reach

It asks Cowork for access to one folder, `~/Downloads/Sediment`, and files the pages
Cowork saves there. That folder holds nothing but pages waiting to be filed, and a page is
deleted from it once it’s on the shelf. If filing fails, the page stays there, and
you can drag it onto Sediment.

It never asks for all of Downloads, or for the shelf folder.
