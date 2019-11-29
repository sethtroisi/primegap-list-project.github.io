---
layout: graph
title: The Gapcoin network
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer = 'Gapcoin';select primedigits from gaps WHERE discoverer = 'Gapcoin';select merit from gaps WHERE discoverer = 'Gapcoin';"
xscale: scaleLinear
yscale: scaleLinear
---

{% include graph.html %}

