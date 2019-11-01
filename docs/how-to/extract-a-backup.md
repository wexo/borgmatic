---
title: How to extract a backup
---
## Extract

When the worst happens—or you want to test your backups—the first step is
to figure out which archive to extract. A good way to do that is to use the
`list` action:

```bash
borgmatic list
```

(No borgmatic `list` action? Try the old-style `--list`, or upgrade
borgmatic!)

That should yield output looking something like:

```text
host-2019-01-01T04:05:06.070809      Tue, 2019-01-01 04:05:06 [...]
host-2019-01-02T04:06:07.080910      Wed, 2019-01-02 04:06:07 [...]
```

Assuming that you want to extract the archive with the most up-to-date files
and therefore the latest timestamp, run a command like:

```bash
borgmatic extract --archive host-2019-01-02T04:06:07.080910
```

(No borgmatic `extract` action? Try the old-style `--extract`, or upgrade
borgmatic!)

The `--archive` value is the name of the archive to extract. This extracts the
entire contents of the archive to the current directory, so make sure you're
in the right place before running the command.


## Repository selection

If you have a single repository in your borgmatic configuration file(s), no
problem: the `extract` action figures out which repository to use.

But if you have multiple repositories configured, then you'll need to specify
the repository path containing the archive to extract. Here's an example:

```bash
borgmatic extract --repository repo.borg --archive host-2019-...
```

## Extract particular files

Sometimes, you want to extract a single deleted file, rather than extracting
everything from an archive. To do that, tack on one or more `--restore-path`
values. For instance:

```bash
borgmatic extract --archive host-2019-... --restore-path path/1 path/2
```

Note that the specified restore paths should not have a leading slash. Like a
whole-archive extract, this also extracts into the current directory. So for
example, if you happen to be in the directory `/var` and you run the `extract`
command above, borgmatic will extract `/var/path/1` and `/var/path/2`.


## Database restoration

The `borgmatic extract` command only extracts files. To restore a database,
please see the [documentation on database backups and
restores](https://torsion.org/borgmatic/docs/how-to/backup-your-databases/).
borgmatic does not perform database restoration as part of `borgmatic extract`
so that you can extract files from your archive without impacting your live
databases.


## Related documentation

 * [Set up backups with borgmatic](https://torsion.org/borgmatic/docs/how-to/set-up-backups/)
 * [Inspect your backups](https://torsion.org/borgmatic/docs/how-to/inspect-your-backups/)
 * [Monitor your backups](https://torsion.org/borgmatic/docs/how-to/monitor-your-backups/)
 * [Backup your databases](https://torsion.org/borgmatic/docs/how-to/backup-your-databases/)