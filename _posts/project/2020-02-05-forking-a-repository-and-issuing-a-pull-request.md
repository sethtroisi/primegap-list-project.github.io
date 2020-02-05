---
layout: post
author: Graham Higgins
category: project
title:  Cloning a repository and creating a Pull Request
tags: projectdoc
excerpt: Illustrated guide to cloning a Prime Gap List project repository and creating a PR
---

## Preparation

#### Step 1 - install [git](https://git-scm.com/), a distributed version control system

The Atlassian tutorial is extensive and recommended [https://www.atlassian.com/git/tutorials/install-git](https://www.atlassian.com/git/tutorials/install-git)

Otherwise ...

###### Windows [Git for Windows](https://gitforwindows.org/)


###### Linux [git](https://git-scm.com/download/linux)


###### Mac OS X [git](https://git-scm.com/download/mac)


#### Step 2 - sign up for a [Github](https://github.com) account

Documentation on:

[Getting started with GitHub](https://help.github.com/en/github/getting-started-with-github), Learn about GitHub’s products, sign up for an account. 

[Setting up and managing your Github account](https://help.github.com/en/github/setting-up-and-managing-your-github-user-account)

---

## Process

### Fork the prime gap list repository

Navigate to the Prime Gap List repository page on Github: `https://github.com/primegap-list-project/prime-gap-list.git` and click on the button labelled "Fork".

---

![the Prime Gap List repository page on Github](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-01.png)

---


### Select the destination

If a choice of destinations is offered, choose an appropriate destination. If no choice is offered the fork will be created in your Github account.

---

![destination options](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-02.png)

---

### Forking in progress

Github’s web UI will show progress. __NOTE__ the location has changed (upper left) from `primegap-list-project/prime-gap-list` to `gjhiggins/prime-gap-list`

---

![forking in progress](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-03.png)

---

### Successfully forked

The repository has been successfully forked into `gjhiggins/prime-gap-list`


![successful fork](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-04.png)

---

### Clone (download) the repository locally

Use the Github web GUI to copy the web URL to use for cloning (copying via downloading) the repository locally with:

    cd <working area>
    git clone <URL>

---

![clone / download the repository](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-05.png)

---

## Updating `allgaps.sql` in your local copy of the repository

Assuming you have already used the prime gap list project web site’s [web GUI conversion facility](https://primegap-list-project.github.io/conversions/) to convert your record prime gap entries into SQL (see the [illustrated guide to checking new record gaps or gaps with better merits](https://primegap-list-project.github.io/project/2019/12/04/how-to-check/)) and have a downloaded file of SQL named (for example) `prime-gap-list-conversion-2020-02-05T01_02_03.123Z.sql`

__NOTE__ in the examples below, you will need to replace references to `https://github.com/gjhiggins` with references to your own account.

### Linux / MacOS shell

#### One-liner

    $ git clone https://github.com/gjhiggins/prime-gap-list.git
    $ cd prime-gap-list
    $ sqlite3 tmp.db <<<$'.read allgaps.sql\n.read prime-gap-list-conversion-2020-02-05T01_02_03.123Z.sql\n.output allgaps.sql\n.dump\n.quit\n'
    $ rm tmp.db
    $ git commit -m "Update for 2020-02-05 by <submitter>"
    $ git push

#### Full line-by-line

    $ git clone https://github.com/gjhiggins/prime-gap-list.git
    $ cd prime-gap-list
    $ sqlite3 tmp.db
    SQLite version 3.22.0 2018-01-22 18:45:57
    Enter ".help" for usage hints.
    sqlite> .read allgaps.sql
    sqlite> .read prime-gap-list-conversion-2020-02-05T01_02_03.123Z.sql
    sqlite> .output allgaps.sql
    sqlite> .dump
    sqlite> .quit
    $ rm tmp.db
    $ git commit -m "Update for 2020-02-05 by <submitter>"
    $ git push


### Windows command shell

#### One-liner

    > git clone https://github.com/gjhiggins/prime-gap-list.git
    > cd prime-gap-list
    > sqlite3 tmp.db ".read allgaps.sql" ".read prime-gap-list-conversion-2020-02-05T01_02_03.123Z.sql" ".output allgaps.sql" ".dump" ".quit"
    > del tmp.db
    > git commit -m "Update for 2020-02-05 by <submitter>"
    > git push

#### Full line-by-line

    > git clone https://github.com/gjhiggins/prime-gap-list.git
    > cd prime-gap-list
    > sqlite3 tmp.db
    SQLite version 3.22.0 2018-01-22 18:45:57
    Enter ".help" for usage hints.
    sqlite> .read allgaps.sql
    sqlite> .read prime-gap-list-conversion-2020-02-05T01_02_03.123Z.sql
    sqlite> .output allgaps.sql
    sqlite> .dump
    sqlite> .quit
    > del tmp.db
    > git commit -m "Update for 2020-02-05 by <submitter>"
    > git push

### State of your Github fork _before_ `git push`

After successfully forking the prime gap repository on github, the fork was reported as being “even with primegap-list-project:master”

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-06.png)

---

### State of your Github fork _after_ `git push`

After pushing your commit (containing the changed `allgaps.sql`) up to your Github fork, it now reports as “1 commit ahead of primegap-list-project:master” - time to click the “New pull request” button and generate a new Pull Request - a request to the repository maintainers to “pull” the changes from the forked repository into the main repository.

__NOTE__ the commit message I used for this working exercise was “Update 2020-02-03 gapcoin merit improvements”, as shown next to the `allgaps.sql` line  

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-07.png)

---

### Basic Pull Request sanity check 

Before actually going through the exercise of actually creating a Pull Request, GitHub’s automata check the committed changes and the web GUI reports whether git can simply merge the changes straightaway or whether the changes are in conflict with the existing code, in which case a repository maintainer is required to resolve the conflicts before the changes can be merged.

In this worked example, the changes to `allgaps.sql` are able to be automatically merged and so it was okay for me to click the “Create pull request” button.

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-08.png)

---

### Opening the pull request

Github’s automata handle the actual merging, all that’s required (by principles of good practice) is an explanatory titled comment to aid the repository maintainers in their task. I have chosen to include the output of Dr Nicely’s `cglp` checker as (weak) confirmation that the primes are indeed such and in preparation for pasting the text, I have entered the appropriate Markdown code for denoting verbatim content - three backticks to denote the start and three to denote the end:

    ```
    ```

##### Basic writing and formatting syntax

Github provides [good documentation of the writing and formatting syntax](https://help.github.com/en/github/writing-on-github/basic-writing-and-formatting-syntax) used for comments.

Of particular note (for its utility in cross-referencing commits, issues and pull requests) is the Github documentation on ”Autolinked references and URLs”, especially the section “[Issues and pull requests](https://help.github.com/en/github/writing-on-github/autolinked-references-and-urls#issues-and-pull-requests)”

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-09.png)

---


### Adding an explanatory or confirmatory message

I then pasted the checked output copied from cglp ...

    =============================================================================
    G=   6098 P1=165780299536768454870526593505937140570016757..(97D).. OK BPSW*1
    G=   6272 P1=148710129286189176623362105968560409845985636..(97D).. OK BPSW*1
    G=   6354 P1=368221405388079181400789997951967077413201972..(87D).. OK BPSW*1
    G=   6364 P1=147872708725008438896840265493528800063370907..(97D).. OK BPSW*1
    G=   6378 P1=114448978367781720231771001349387152044607787..(97D).. OK BPSW*1
    G=   6428 P1=122297977636934185744748044406791875203549301..(97D).. OK BPSW*1
    G=   6432 P1=167670307352479624859373437749938392275931638..(97D).. OK BPSW*1
    G=   6618 P1=529020352802661375241399423756367771225299185..(99D).. OK BPSW*1
    G=   6628 P1=206823118393258320900948642245542552398543310..(97D).. OK BPSW*1
    G=   8056 P1=42025082789596485040260513128144215771069157..(117D).. OK BPSW*1
    =============================================================================
     Errors=0.  OK=10.  T=0.109 seconds.
     Input=gaps.dat.  CL==>./cglp4 gaps.dat<==.
    =============================================================================

between the pairs of triple backticks:

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-10.png)

---

### Previewing the rendering of the comment

By selecting the “Preview” tab, I check that my Markdown content is properly rendered ...

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-11.png)

---

### Creating the completed pull request

At this point, with my comment completed and checked, all I need to do is click on the “Create pull request” button ...

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-12.png)

---

### The opened pull request

On clicking the “Create pull request” button, I am immediately taken to the page showing the newly-created and “open” pull request. As a repository maintainer, I have a privileged view that includes a “Merge pull request” button which is only presented to repository maintainers (a user with an “admin” role, in Github parlance), otherwise the page looks the same.

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-13.png)

---

### Requested changes are available for inspection

Note the small inclusion in the middle of the page ...

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-14.png)


Of interest to repository administrators, the cryptic hexadecimal code `d769e23` is a hyperlink text which leads to a Github page showing an easy-to-encompass rendering of the actual changes.


![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-15.png)


Each git commit is identified by a unique SHA hash code. In this instance, the commit hash is `d769e23e485468e91c33377c7bc0c33f66a0e925` as shown above - opposite my mugshot and the text “__gjhiggins__ committed 22 hours ago”.

The shortened form `d769e23` is used for convenience and to lessen the user-hostility of the full form.

---

### Github repository web presentation updated 

The notification of an existing open pull request appears as a numeral included the "Pull requests" tab and in the web UI's listing of open pull requests.

The listed links simply lead to the page showing the pull request. For this worked example, it is the same as that shown in “The opened pull request” above.

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-16.png)

---

### Merging a pull request

As mentioned above, repository administrators are exclusively shown a “Merge pull request” button which, when clicked, triggers the Github automata to perform the merge and change the status of the pull request from “open” to “closed”, changing the page content to reflect that fact.

Details of closed pull requests are accessible via the Github web UI, via the “Pull Requests” tab, i.e. [All closed pull requests for prime-gap-list](https://github.com/primegap-list-project/prime-gap-list/pulls?q=is%3Apr+is%3Aclosed) and for [this worked example](https://github.com/primegap-list-project/prime-gap-list/pull/1).

Note also the “Fork settings” button, exclusively shown to the user who created the pull request and which triggers an offer to delete the fork from which the pull request originated.

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-17.png)


---

### Tidying up

For a closed pull request, the “Fork settings” button is exclusively shown to the user who created the pull request.

It triggers an offer to delete the fork from which the pull request originated.

#### Keep it clean

It’s good practice to delete your fork of the main prime-gap-list repository and re-create it as required because it is __NOT__ automatically updated with subsequent changes to the main repository made by other group members.

For exactly the same reason, it’s also good practice to delete your locally cloned fork after your pull request has been accepted and closed.

---

![](/img/posts/2020-02-05-forking-a-repository-and-issuing-a-pull-request-18.png)

---


