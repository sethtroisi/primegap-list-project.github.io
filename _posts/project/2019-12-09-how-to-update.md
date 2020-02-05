---
layout: post
author: Graham Higgins
category: project
title: How to create a merits.txt
tags: projectdoc
excerpt: Creating a merits.txt for reference
---

Tom Nicely used to publish a list of merits for checking:

“Furthermore, I have also made available for download the zipfile merits.zip, which contains a text file specifying the measure G and the merit M=G/ln(p_1) for all known first occurrence and first known occurrence prime gaps. This much smaller file (less than 1 MB) should be of additional assistance in determining whether or not some newly discovered gap constitutes a new first known occurrence.”

Maintaining the list of known first occurrence prime gaps as a file of SQL statements allows users to create their own version, specific to the range of gaps and merits pertinent to the range being searched.

The first step is to download the latest version is available from the github repository at: [https://raw.githubusercontent.com/primegap-list-project/prime-gap-list/master/allgaps.sql](https://raw.githubusercontent.com/primegap-list-project/prime-gap-list/master/allgaps.sql)

The next step is read the list into the SQLite command-line client

```bash
$ sqlite3 allgaps.db
SQLite version 3.22.0 2018-01-22 18:45:57
Enter ".help" for usage hints.
sqlite> .read allgaps.sql
sqlite> 
```

The following recipe can be copied and pasted into the sqlite3 command-line client and will create a list of gaps and merits for gaps in the range 10000 and 20000

    .mode list
    .separator ','
    .output merits.txt
    SELECT gapsize, merit FROM gaps WHERE gapsize BETWEEN 10000 and 20000 ORDER BY gapsize;
    .exit

producing a `merits.txt` file of which the first 10 lines are:

    10000,30.01
    10002,27.81
    10004,27.77
    10006,27.74
    10008,30.44
    10010,27.77
    10012,30.21
    10014,28.42
    10016,29.22
    10018,26.98

This is how it works on Windows 10:

![Screenshot of Windows 10 session](/img/news/2019-12-10-how-to-create-merits.png)

Notepad users will need to adjust the recipe to include an incantation to create a Windows-specific line ending: `|| char(13)`

    .mode list
    .separator ','
    .output merits.txt
    SELECT gapsize, merit || char(13) FROM gaps WHERE gapsize BETWEEN 10000 and 20000 ORDER BY gapsize;
    .exit

---
