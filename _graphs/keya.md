---
layout: graph
title: Antonio Key
description: Graph of gap length plotted against number of prime digits
author: Graham Higgins
category: graph
tags: graph
dbquery: "select gapsize from gaps WHERE discoverer = 'Toni_Key';select primedigits from gaps WHERE discoverer = 'Toni_Key';select merit from gaps WHERE discoverer = 'Toni_Key';"
xscale: scaleLinear
yscale: scaleLinear
---

{% include graph.html %}

