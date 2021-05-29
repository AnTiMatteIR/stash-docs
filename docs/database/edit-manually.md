---
title: Manually editing the Stash sqlite database
summary: Explanation on how to manually edit the Stash database using sqlite.
authors:
    - victorhooi
    - AnTiMatteIR
date: 2021-05-29
---

# Manually editing the Stash sqlite3 database

## Location

The Stash Sqlite3 database file is located at `~/.stash/stash-go.sqlite`.

Before making changes to the Stash sqlite3 database - **please make a [backup](backup-restore.md#backup) first!**

You can use the `sqlite3` client to directly edit this file.

## Opening the database file

```bash
cd ~/.stash
sqlite3 stash-go.sqlite
```

## Deleting all tags

If you need to delete all tags, you can use the following commands:

```sql
sqlite> DELETE FROM scenes_tags;
sqlite> DELETE FROM tags;
```

Please note that this will not work if you have Scene market tags (TODO: What to do then?)


{% include 'links.md' %}