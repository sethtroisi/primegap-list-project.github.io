---
layout: post
author: Graham Higgins
category: project
title:  "Project Roadmap"            # Title used in HTML Meta, Post Header, Recent Posts list
tags: post project feature                   # Tags to relate multiple topics to a post
excerpt: "Roadmap outlining possible future directions / activities"
---

Copied over from mersenneforum.

#### *Dana Jacobsen*

I was thinking of something like [*this page*](http://ntheory.org/gaps/stats.pl). So we don't have to keep posting these big lists. If I was ambitious I could crawl gapcoin's results, and have some way to submit data.

Other things to display:

    Overall top-20 gaps
    Record holders, with numbers of gaps and percent of total
    Stats about my new un-submitted gaps
    Graphs
    Interesting stats about gaps in the last month?
    Something else?

---

#### *Robert Smith*

    Achievements
    Theory
    Programming
    Very small gaps - 1,300 - 4,000
    Small gaps 4,000 - 60,000
    Medium gaps 60,000 - 500,000
    Large gaps >500,000
    Collaboration requests

---

#### *Dana Jacobsen*

There are a lot of goals people are pursuing. Feel free to point out more.

**Number of gaps.**
The easiest way to increase this, I believe, is to look a bit past the frontier. This used to be in the 60-80k range, now it's in the 120k or so range. This has lots of open spaces so most gaps have no record and those that do are relatively small so there is a decent chance of beating the result.

**Filling in the frontier.**
There has been some effort to fill in all the remaining gap lengths under 100k, and also to see if we can get all non-maximal lengths under 100k to have a merit >= 10. I have some searches going through these ranges, and I believe Antonio and Rosenthal are also doing this.

**Large gap sizes.**
At this point I think anything 300k+. These take a lot of time per result. Martin Raab is finding huge gaps, while Rob and I are finding a few. The chances of finding a 30+ merit here is quite small given the time required to find any gap. Rosenthal found the largest recently: 31.78 merit at length 309030. The next largest is Rob Smith's 30.38 at length 157194.

**Small gap sizes.**
I don't believe anyone is doing exhaustive searches any more, but there are quite a few people looking for results in the sub-2k range. This is a big effort for very few results (but IMO useful ones!). In the last year it looks like Leif Leonhardy, Bertil Nyman, Helmut Spielauer, and Rob Smith are doing this and getting results.

**Large merits.**
I've found searches in the 4k to 12k range seem to push these out quite rapidly. Finding 30+ merit gaps in here seems to not be too difficult. Under 4k doesn't produce much for me, and the searches take longer as the length rises of course. In theory doing more searches in the 2k-4k range, perhaps with an all-GMP C program to minimize overhead, would be more efficient. The 5k-8k range is where Gapcoin seems to have concentrated, with their newer miner also looking to \~24k (concentrated in 12k-16k). Most of their high merits are in the 6k-8k range.

#### *Antonio Key*

Here's my stats for this weeks submission (checked against merits.txt dated 2015-10-14). Maintaining >18 records/day/core, despite taking one (of four) core out to try a few search modification ideas. Nothing spectacular to report, but I live in hope

         Gap   -   Entries 
        Owner  -   Improved
      Rosnthal -      143
      Jacobsen -       83
      RobSmith -       21
      M.Jansen -       17
      Toni_Key -        7
      PierCami -        4
      TorAlmJA -        4
      Andersen -        2
      JLGPardo -        1
      MJPC&JKA -        1
       Gapcoin -        1
         Total -      284
    523 new entries for merits.txt
    239 first time gaps found
    Smallest merit increase        =  0.009355
    Largest merit increase         = 11.372329
    Largest merit found            = 25.683840
    Largest merit (first time gap) = 21.487940
    Smallest gap recorded          =     13046
    Largest gap recorded           =    219390


#### *Dana Jacobsen*

The small gaps are interesting. I kind of want to see what an AWS instance churning on small numbers could do. It's not as exciting as the 60-100k range though, where every hour sees visible results. Above 4k digits or so, a different library should be used -- gwnum is better than GMP for this.

I was debating writing a script that would take as input something like `1 * 37993# / 30` and do the presieve with my code to get the list of candidates, then call OpenPFGW on each one to test compositeness until a PRP is found (which can then be tested with BPSW or Paul's gwnum-Frobenius routine).

More polished would be a C program that pulls all that in.

#### *Rob Smith*

“merit” should not be float but a rounded 6 decimal number with trailing zeros if applicable, for example <math>35.678020</math>. Reporting from the system can be a smaller number of decimals, but there should be a lower limit on what constitutes a new record and I think 6 decimals is adequate.

Regarding the database can we add month of the year as a 3 alpha, in the form Jan, Feb, etc? This would encourage more frequent submissions and a better sense for the rate of discovery. [Prime Searches Group, Mersenne Forum](https://www.mersenneforum.org/showpost.php?p=531740&postcount=159)



---
