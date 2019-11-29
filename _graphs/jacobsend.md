---
layout: graph
title: Dana Jacobsen
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer = 'Jacobsen';select primedigits from gaps WHERE discoverer = 'Jacobsen';select merit from gaps WHERE discoverer = 'Jacobsen';"
xscale: scaleLinear
yscale: scaleLog
---

{% include graph.html %}

