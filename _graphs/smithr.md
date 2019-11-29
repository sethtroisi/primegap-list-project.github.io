---
layout: graph
title: Rob Smith
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer = 'RobSmith';select primedigits from gaps WHERE discoverer = 'RobSmith';select merit from gaps WHERE discoverer = 'RobSmith';"
xscale: scaleLinear
yscale: scaleLinear
---

{% include graph.html %}

