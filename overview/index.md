---
title: Overview
layout: en
---

# Overview

PGroonga is a PostgreSQL extension. PGroonga provides a new index that uses [Groonga](http://groonga.org/).

Groonga is an embeddable super fast full text search engine. It can be embedded into MySQL. [Mroonga](http://mroonga.org/) is a storage engine that is based on Groonga. Groonga can also work as standalone search engine. 

As default, PostgreSQL isn't capable for CJK full text search. But you can use super fast CJK full text search by installing PGroonga.

## Related extensions

There are some extensions that implements CJK ready full text search:

  * [pg_trgm](http://www.postgresql.org/docs/9.4/static/pgtrgm.html)
    * It's bundled with PostgreSQL but it's not installed as default.
    * You need to change pg\_trgm source code to support CJK.

  * [pg_bigm](http://pgbigm.osdn.jp/)
    * It supports CJK without changing source code.
    * It requires [Recheck](http://pgbigm.osdn.jp/pg_bigm_en-1-1.html#enable_recheck) to remove false positives.
    * Recheck is slow for many hits case. Because Recheck does sequential search against records found by index search.
    * If you disables Recheck, you may get false positives.

PGroonga supports CJK without changing source code.

PGroonga works without Recheck. PGroonga can find exact records only by index search. PGroonga is fast for many hits case.

PGroonga doesn't support crash recovery and streaming replication because PGroonga doesn't support WAL. Because PostgreSQL doesn't provide API for supporting WAL to extensions. PGroonga will support WAL when PostgreSQL provides the API.

FYI: pg\_trgm and pg\_bigm support WAL. To be precise, GIN and GiST that are used by pg\_trgm and pg\_bigm support WAL.

## History

PGroonga is based on [textsearch_groonga](http://textsearch-ja.projects.pgfoundry.org/textsearch_groonga.html) that was developed by Itagaki Takahiro. Thanks for the works!

## The next step

Interested? [Install](../install/) PGroonga and try [tutorial](../tutorial/). You can understand more about PGroonga.