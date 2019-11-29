---
layout: graph
title: Hans Rosenthal
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer like 'Rosnt%';select primedigits from gaps WHERE discoverer like 'Rosnt%';select merit from gaps WHERE discoverer like 'Rosnt%';"
xscale: scaleLinear
yscale: scaleLinear
---

{% include graph.html %}

