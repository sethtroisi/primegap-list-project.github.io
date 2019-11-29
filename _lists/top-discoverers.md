---
layout: list
title: "Discoverers of record prime gaps"
description: "Leaderboard"
author: Graham Higgins
category: list
tags: list
columns: [Discoverer, Number, Percent]
dbquery: "SELECT (select display from credits where abbreviation = discoverer) as name, count(*) as number, printf('%.2f', count(*) * 100.0 / (select count(*) from gaps)) as percent from gaps group by name order by number desc, name asc;"
htmltemplate: "<tr><td>${row['name']}</td> <td>${row['number'].toString().padEnd(8, ' ')}</td> <td>${row['percent']}</td></tr>"
---
