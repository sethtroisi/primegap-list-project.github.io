---
layout: graph
title: Michiel Jansen
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer like 'MJ%' or discoverer = 'M.Jansen';select primedigits from gaps WHERE discoverer like 'MJ%' or discoverer = 'M.Jansen';select merit from gaps WHERE discoverer like 'MJ%' or discoverer = 'M.Jansen';"
xscale: scaleLinear
yscale: scaleLinear
---

{% include graph.html %}

