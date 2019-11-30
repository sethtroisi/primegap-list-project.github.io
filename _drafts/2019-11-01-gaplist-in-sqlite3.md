---
layout: post
author: Graham Higgins
category: project
title: Handling the allgaps.db SQLite database
description: Read gap data from sqlitedb
excerpt: Options for accessing the allgaps.db SQLite3 database
---

## Download SQL source from:

***Location***: [https://raw.githubusercontent.com/primegap-list-project/primegap-list-project.github.io/master/\_data/allgaps.sql](https://raw.githubusercontent.com/primegap-list-project/primegap-list-project.github.io/master/_data/allgaps.sql)

## Use with ...

### Recommended: “DB Browser for SQLite” open source application

[DB Browser for SQLite](https://sqlitebrowser.org/) (downloadable binaries/packages are available for all the main arch/OS variants: [https://sqlitebrowser.org/dl/](https://sqlitebrowser.org/dl/)).

---
DB Browser for SQLite (DB4S) is a high quality, visual, open source tool to create, design, and edit database files compatible with SQLite. DB4S uses a familiar spreadsheet-like interface, and complicated SQL commands do not have to be learned. Controls and wizards are available for users to:

- Create and compact database files
- Create, define, modify and delete tables
- Create, define, and delete indexes
- Browse, edit, add, and delete records
- Search records
- Import and export records as text
- Import and export tables from/to CSV files
- Import and export databases from/to SQL dump files
- Issue SQL queries and inspect the results
- Examine a log of all SQL commands issued by the application
- Plot simple graphs based on table or query dat

---


![SQLiteBrowser screenshot](https://web.archive.org/web/20190725114121im_/https://sqlitebrowser.org/images/screenshot.png)

### If required: LibreOffice Base on Linux

It is possible to use SQLite3 databases with LibreOffice Base. There are a couple of preliminary `apt install` requirements that need to be satisfied and a straightforward download + `configure; make install` to be done but fortunately there is a competent and accessible walkthrough, thanks to Thej:

![Thej](https://web.archive.org/web/20190828212424im_/https://thejeshgn.com/blog/wp-content/uploads/2008/09/thejesh_at_sitting_tea-300x198.jpg)

His illustrated copy’n’pasta walkthrough is usefully (and appropriately) preserved on archive.org:

[https://web.archive.org/web/20190724053643/https://thejeshgn.com/2018/08/23/using-sqlite-with-libreoffice-base-on-linux/](https://web.archive.org/web/20190724053643/https://thejeshgn.com/2018/08/23/using-sqlite-with-libreoffice-base-on-linux/)

Works for me under Linux Mint 19.2

