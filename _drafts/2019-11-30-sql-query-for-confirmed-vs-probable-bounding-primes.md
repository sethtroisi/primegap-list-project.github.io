---
layout: post
author: Graham Higgins
category: project
title:  Confirmed vs probable bounding primes
tags: post project
excerpt: "How to query the SQL database for the total of confirmed vs probable bounding primes"
---

Enter the following into SQLiteBrowser’s “Execute SQL” tab:

    SELECT DISTINCT primecert, COUNT(*) FROM gaps GROUP BY primecert;

result:

    "C" "33355"
    "P" "61177"

It’s traditional practice to use upper-cased words to indicate SQL commands and lower-cased words to indicate (changeable) field names, so if a count of discoverers was wanted, the query would read:

    SELECT DISTINCT discoverer, COUNT(*) FROM gaps GROUP BY discoverer;

