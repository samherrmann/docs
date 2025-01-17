---
title: SQL
---

# SQL

## Running SQL queries

There are two ways to run SQL queries against your database:

- `dolt sql` runs SQL queries from your shell
- `dolt sql-server` starts a MySQL-compatible server

### dolt sql

Using `dolt sql` you can issue SQL statements against a local database
without starting a server.

With no arguments, `dolt sql` begins an interactive shell.

```bash
% dolt sql
# Welcome to the DoltSQL shell.
# Statements must be terminated with ';'.
# "exit" or "quit" (or Ctrl-D) to exit.
menus> show tables;
+------------+
| Table      |
+------------+
| menu_items |
+------------+
menus> exit
Bye
```

With the `-q` flag, it executes queries specified as arguments.

```bash
% dolt sql -q "show tables"
+------------+
| Table      |
+------------+
| menu_items |
+------------+
```

You can also use `STDIN` to the `dolt sql` command to execute many SQL statements at once. This is useful for importing a dump from another database.

```bash
% dolt sql < mysqldump.sql
```

View the `dolt sql` command documentation [here](./cli.md#dolt-sql).

### dolt sql-server

The `dolt sql-server` command runs a MySQL compatible server which
clients can connect to and execute queries against. Any library or tool
that can connect to MySQL can connect to Dolt.

```bash
% dolt sql-server
Starting server with Config HP="localhost:3306"|U="root"|P=""|T="28800000"|R="false"|L="info"
```

The host, user, password, timeout, logging info and other options can
be set on the command line or via a config file.

View the `dolt sql-server` command documentation
[here](./cli.md#dolt-sql-server).

## Dolt CLI in SQL

Most of Dolt's CLI commands, e.g. `dolt status`, `dolt commit`, `dolt merge`, `dolt push`, `dolt pull`, are available in the SQL context, either via [system tables](sql/dolt-system-tables.md) or as [custom SQL functions](sql/dolt-sql-functions.md). All CLI functionality will eventually
be exposed in SQL.

## System Tables

Many of Dolt's unique features are accessible via system tables. These
tables allow you to query the same information available from various
Dolt commands, such as branch information, the commit log, and much
more. You can write queries that examine the history of a table, or
that select the diff between two commits.

- [dolt_log table](sql/dolt-system-tables.md#dolt_log)
- [dolt_branches table](sql/dolt-system-tables.md#dolt_branches)
- [dolt_commit_diff tables](sql/dolt-system-tables.md#dolt_commit_diff_usdtablename)
- [dolt_diff tables](sql/dolt-system-tables.md#dolt_diff_usdtablename)
- [dolt_history tables](sql/dolt-system-tables.md#dolt_history_usdtablename)
- [dolt_status table](sql/dolt-system-tables.md#dolt_status)
- [dolt_conflicts tables](sql/dolt-system-tables.md#dolt_conflicts_usdtablename)
- [dolt_remotes table](sql/dolt-system-tables.md#dolt_remotes)