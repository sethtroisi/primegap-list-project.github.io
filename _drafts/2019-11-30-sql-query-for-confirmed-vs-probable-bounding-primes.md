---
layout: post
author: Graham Higgins
category: project
title:  Confirmed vs probable bounding primes
tags: post project
excerpt: "How to query the SQL database for the total of confirmed vs probable bounding primes"
---

Enter the following into SQLiteBrowser’s “Execute SQL” tab:

    select distinct primecert, count(*) from gaps group by primecert;

result:

    "C" "33355"
    "P" "61177"

