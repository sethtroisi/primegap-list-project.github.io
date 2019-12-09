---
layout: post
author: Graham Higgins
category: project
title: How to update the list of known first occurrence prime gaps
tags: post project
excerpt: Step-by-step process for creating an update of the list of known first occurrence prime gaps
---

#### Assumptions and summary of process

I’ll assume that you have saved a file of SQL statements as produced by the project website conversion facility (see [How to check new gaps / better merits](/project/2019/12/04/how-to-check/) for how to do this). In this example, I’m using the one I created for the bettered merits produced by Gapcoin: `prime-gap-list-conversion-2019-12-06T01_02_55.318Z.sql`

The process is fairly straightfoward.

1. clone your Github fork locally and change directory to the clone
2. start the SQLite3 command-line application with a temporary, empty database (suggested: `tmp.db`)
3. read in the repository’s list of prime gaps expressed as SQL statements (`allgaps.sql`)
4. read in the new gaps/bettered merits expressed as SQL statements
5. dump the database as SQL statements to the file `allgaps.sql` (overwriting the old one)
6. commit the updated `allgaps.sql` to your local clone of the repository
7. push the changes back to your fork on Github.
8. use the Github web ui to issue a Pull Request on the main project repository


##### Step one, clone the `prime-gap-list` repository 

Open Source community best practice is to fork the project repository into your own Github area (see the Appendix for how to do this) and then clone the forked repository to work on locally.

```bash
git clone https://github.com/gjhiggins/prime-gap-list.git
cd prime-gap-list
```

##### Step two, read the SQL files into SQLite3 and dump the result as SQL

```bash
$ sqlite3 tmp.db
SQLite version 3.22.0 2018-01-22 18:45:57
Enter ".help" for usage hints.
sqlite> .read allgaps.sql
sqlite> .read prime-gap-list-conversion-2019-12-06T01_02_55.318Z.sql
sqlite> .output allgaps.sql
sqlite> .dump
sqlite> .quit
```

##### Step three, commit the changed file of SQL to the cloned repos and push the changes

```bash
git commit -m "New merits from Gapcoin" allgaps.sql # Explicit commit messages are good
git push
```

##### For project maintainers - updating the website’s conversion facility

The above process is the absolute minimum for updating the list of known first occurrence prime gaps. However, the conversion process served by the project’s static website won’t be updated unless the accepted changes are propagated to the static website.

```bash
$ sqlite3 tmp.db
SQLite version 3.22.0 2018-01-22 18:45:57
Enter ".help" for usage hints.
sqlite> .mode csv
sqlite> .once allgaps.csv
sqlite> SELECT * FROM gaps
sqlite> .once credits.csv
sqlite> SELECT * FROM credits
sqlite> .quit
```

Locally clone your Github fork of `primegap-list-project.github.io` and use as working directory; copy the CSV files into the `_data` directory; commit and push the changes

```bash
git clone https://github.com/gjhiggins/primegap-list-project.github.io.git
cp ../prime-gap-list/allgaps.csv ../prime-gap-list/credits.csv _data
git commit -m "Update from Gapcoin"
git push
```

## Appendix

If you’re unfamiliar with Github and Git repositories, the following is what to expect ...

### Cloning the prime-gap-list repository

Navigate to the the `primegap-list-project` organisation and then to the `prime-gap-list` repository: [https://github.com/primegap-list-project/prime-gap-list](https://github.com/primegap-list-project/prime-gap-list)

##### Locate the “Fork” button and click it:

![Location of fork button](/img/news/2019-12-09-how-to-update-01.png)

---

##### Choose the destination of the fork, if one is offered

![Destination of fork](/img/news/2019-12-09-how-to-update-02.png)

---

##### Wait a couple of moments for the fork to be created

![Creaing fork](/img/news/2019-12-09-how-to-update-03.png)

---

##### Note successful result, a copy of the repository in your account area

![Successful result](/img/news/2019-12-09-how-to-update-04.png)

---

##### Copy the URL of your fork of the Github repository for cloning to your hard drive

![URL to use](/img/news/2019-12-09-how-to-update-05.png)

---

You should now be in a position to pick up at the beginning of the example interation.


### Issuing a “Pull Request”

I created a fake update by incrementing one of Gapcoin’s merits, then committed and pushed the change to my Github repos.

Now I need to create a “Pull request” so my changes can be merged into the project repository. Github’s web GUI offers a clickable tab:

![Destination of fork](/img/news/2019-12-09-how-to-update-06.png)

---

which, when clicked takes me to a welcome screen that offers a “New pull request” button to click.

Note that this is still within the context of my Github fork.

![Destination of fork](/img/news/2019-12-09-how-to-update-07.png)

---

Github performs some behind-the-scenes checking to ensure that the proposed changes actually can be merged without causing problems and offers a highlighted “Create pull request” button to click.

Note that the context has been changed to the project repository - where the PR will get created.

![Destination of fork](/img/news/2019-12-09-how-to-update-08.png)

---

And finally, I am taken to the business screen where I can write a comment explaining the reason for the PR and use the (highlighted) facility to attach a supporting text file, specifically the confirmatory output from running the cgpl4 gap checker on the new Gapcoin gaps.

I renamed the cgpl4 output file `cgpl4.out` to `gapcoin-cglp4-check-results.txt` for clarity.

**NB** the change in file extension is necessary in order to be able actually to select the file in the file dialog box - as Github only accepts certain extensions (incl. `.txt`) as attachments.

After writing my explanatory comment and attaching the results of the cglp4 gap checker, I can click the “Create new pull request”, thus completing the process.

![Destination of fork](/img/news/2019-12-09-how-to-update-09.png)

---

The “Pull requests” tab of the project repository will show +1 in its tally and the submitted PR will appear in the list of PRs submitted to the project repository maintainers. (The example image shows an unrelated PR that I submitted)

![Destination of fork](/img/news/2019-12-09-how-to-update-10.png)

---


### Linux copy’n’pasta one-liners

Linux users can use one-liners for convenience.

##### Reading SQL and dumping SQL
```bash
$ # Presentation, to avoid long lines wrecking the display
$ mv prime-gap-list-conversion-2019-12-06T01_02_55.318Z.sql updates.sql 
$ sqlite3 tmp.db <<<$'.read allgaps.sql\n.read updates.sql\n.output allgaps.sql\n.dump\n'
```

##### Recreating `allgaps.csv` and `credits.csv`:
```bash
sqlite3 -csv tmp.db "SELECT * FROM gaps;" > allgaps.csv
sqlite3 -csv tmp.db "SELECT * from credits;" > credits.csv
```

---
