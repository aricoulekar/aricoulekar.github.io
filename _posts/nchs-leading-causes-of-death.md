---
title: "How Americans Die": The Evolution of the Lead Causes of Death from 1999 to 2017
tags: [Health]
style: fill
color: dark
description: An interactive exploration of how the leading causes of death in the US have changed from 1999 to 2017.
---

*Author: Ari Coulekar*

## Introduction

The Center for Disease Control and Prevention (or the CDC) tracks numerous amounts of health data for the United States. Some of the statistics they track include the leading causes of death. Using these numbers, we can not only track how many people across the United States pass away from these causes, but also how factors such as how the evolution of medicine, treatments, and health policies can shape the trends of life and death.

## How the Causes of Death have Changed: The Data

The interactive chart below shows the age-adjusted death rate (per 100,000 people) for the top 10 leading causes of death in the United states from 1999 to 2017. Each line represents a single cause of death, and each node represents a cause of death, the year, and the death rate per 100,000 people. Clicking on a point in the legend will highlight that specific cause of death. 

<script>
  var spec = nchs_chart.json;
  vegaEmbed('#vis', spec, {actions: false});
</script>
