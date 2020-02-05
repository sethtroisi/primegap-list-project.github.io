---
layout: post
author: Graham Higgins
category: project
title:  Updating the CSV file that drives the website conversion GUI
tags: projectdoc
excerpt: A walkthrough of a shortened process for updating the prime gap list project website's CSV data file 
---


### Concise summary

Rather than go through the extended process of raising a PR, here’s a direct way of updating the CSV data file used by the website GUI’s conversion pages.

Locally clone the `prime-gap-list-project` repository, get the latest `allgaps.sql` file from the `prime-gap-list` repository and copy it into the `prime-gap-list-project` repository’s `_data` folder. Navigate to the `prime-gap-list-project` repository’s `_data` folder and copy’n’paste the appropriate one-liner to generate an updated `allgaps.csv` from the downloaded latest `allgaps.sql`. Tidy up by removing the processing detritus, commit and push the changed `allgaps.csv` file, then finish up by deleting the `prime-gap-list-project` repository.

### Preparation

1. In a suitable temporary working area, locally clone the primegap list project website repository into `primegap-list-project`:

        git clone https://github.com/primegap-list-project/primegap-list-project.github.io.git primegap-list-project

2. Get the latest prime gaps list in SQL format - `allgaps.sql`

    Either by locally cloning the prime gap list with:

        git clone https://github.com/prime-gap-list

    Or just download the latest `allgaps.sql` from:

        https://github.com/primegap-list-project/prime-gap-list/raw/master/allgaps.sql

3. Copy `allgaps.sql` to `primegap-list-project/_data`


### To generate the CSV from the SQL:

Being aware that sqlite3 _has_ to have a database file to work with even though we won’t be using it, so we will label it as such (`junk.db`) ...

Navigate to `primegap-list-project/_data` and copy and paste the following one-liners or the (in full) line-by-line commands:

##### Windows command shell (using `>` as prompt character):

One-liner:

    > sqlite3 junk.db ".read allgaps.sql" ".mode csv" ".output allgaps.csv" "select * from gaps;" ".quit"

In full:

    > sqlite3 junk.db 
    sqlite> .read allgaps.sql
    sqlite> .mode csv
    sqlite> .output allgaps.csv
    sqlite> select * from gaps;
    sqlite> .quit

Lastly, tidy up by removing the `junk.db` temporary database created by sqlite3 and the no-longer-needed `allgaps.sql` data file:

    > del junk.db allgaps.sql

##### Linux or MacOS shell (using `$` as prompt character):

One-liner:

    $ sqlite3 junk.db <<<$'.read allgaps.sql\n.mode csv\n.output allgaps.csv\nselect * from gaps;\n.quit\n'

In full:

    $ sqlite3 junk.db 
    sqlite> .read allgaps.sql
    sqlite> .mode csv
    sqlite> .output allgaps.csv
    sqlite> select * from gaps;
    sqlite> .quit

Lastly, tidy up by removing the `junk.db` temporary database created by sqlite3 and the no-longer-needed `allgaps.sql` data file:

    $ rm junk.db allgaps.sql

### Commit the changes to the Github repository

1. Navigate to `primegap-list-project` (i.e. `cd ..` from the above `_data` location)
2. Check status of clone with `git status .`
3. Commit the changed CSV file:

     `git commit -m "Updated allgaps CSV file" _data/allgaps.csv`

   Then push the changes up to Github so that the Github repository is updated and the prime gap list project website will be automatically refreshed by Github’s own scripts:

      `git push`


### Tidying up is good group practice
Finish up by deleting the locally cloned repository `primegap-list-project` and, if it was cloned, the `prime-gap-list` repository.

Deleting the locally cloned repositories ensures that next time you follow this process, a fresh local clone of the project repository will include any subsequent changes made and committed to the repository by other members of the group.


### All in one chunk

    cd /tmp;
    git clone https://github.com/primegap-list-project/primegap-list-project.github.io.git primegap-list-project
    cd primegap-list-project/_data
    curl -O https://github.com/primegap-list-project/prime-gap-list/raw/master/allgaps.sql
    sqlite3 junk.db <<<$'.read allgaps.sql\n.mode csv\n.output allgaps.csv\nselect * from gaps;\n.quit\n'
    rm junk.db allgaps.sql
    cd ..
    git commit -m "Updated allgaps CSV file" _data/allgaps.csv
    git push
    # If not using git credential helper, enter username and password at the prompt
    cd ..
    rm -rf primegap-list-project

#### Github username and password credential helper
To avoid having always to enter the username and password, use the git credential helper as described on [Push to GitHub without entering username and password every time (Git Bash on Windows)](https://www.tilcode.com/push-github-without-entering-username-password-windows-git-bash/)

On Windows, (using [Git SCM for Windows](https://gitforwindows.org/))

    git config --global credential.helper wincred

On Linux and MacOS

    git config --global credential.helper cache

---
