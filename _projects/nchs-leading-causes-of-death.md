---
name: "How Americans Die: The Evolution of the Lead Causes of Death from 1999 to 2017"
tools: [Python, Altair, vega-lite]
image:
description: "An interactive exploration of how the leading causes of death in the US have changed from 1999 to 2017."
---
# How Americans Die: The Evolution of the Lead Causes of Death from 1999 to 2017

*Author: Ari Coulekar*

## Introduction

The Center for Disease Control and Prevention (or the CDC) tracks numerous amounts of health data for the United States. Some of the statistics they track include the leading causes of death. Using these numbers, we can not only track how many people across the United States pass away from these causes, but also how factors such as how the evolution of medicine, treatments, and health policies can shape the trends of life and death. This post explores these changes using [data from the National Center for Health Statistics](https://catalog.data.gov/dataset/nchs-leading-causes-of-death-united-states)

## How the Causes of Death have Changed: The Data

The interactive chart below shows the age-adjusted death rate (per 100,000 people) for the top 10 leading causes of death in the United states from 1999 to 2017. Each line represents a single cause of death, and each node represents a cause of death, the year, and the death rate per 100,000 people. Clicking on a point in the legend will highlight that specific cause of death. 

<div id="vis"></div>

<script src="https://cdn.jsdelivr.net/npm/vega@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-lite@5"></script>
<script src="https://cdn.jsdelivr.net/npm/vega-embed@6"></script>

<script type="text/javascript">
  var spec = {
    "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
    "title": "Age-Adjusted Death Rates by Cause in the US (1999-2017)",
    "width": 700,
    "height": 400,
    "data": {
      "url": "https://aricoulekar.github.io/assets/data/nchs_lead_cause_of_death.csv",
      "format": {"type": "csv"}
    },
    "transform": [
      {"filter": "datum.State == 'United States'"},
      {"filter": "datum['Cause Name'] != 'All causes'"}
    ],
    "mark": {"type": "line", "point": true},
    "params": [{
      "name": "selected_cause",
      "select": {"type": "point", "fields": ["Cause Name"]},
      "bind": "legend"
    }],
    "encoding": {
      "x": {"field": "Year", "type": "ordinal", "axis": {"labelAngle": -45, "title": "Year"}},
      "y": {"field": "Age-adjusted Death Rate", "type": "quantitative", "axis": {"title": "Age-Adjusted Death Rate (per 100,000)"}},
      "color": {"field": "Cause Name", "type": "nominal", "legend": {"title": "Cause of Death"}},
      "opacity": {"condition": {"param": "selected_cause", "value": 1}, "value": 0.15},
      "tooltip": [
        {"field": "Cause Name", "type": "nominal", "title": "Cause"},
        {"field": "Year", "type": "ordinal"},
        {"field": "Age-adjusted Death Rate", "type": "quantitative", "title": "Death Rate"}
      ]
    }
  };
  vegaEmbed('#vis', spec, {actions: false});
</script>

## The Heart Disease Trend

The most obvious trend in the data is the decline in heart disease over the years. In 1999, heart disease killed roughyl 267 people per 100,000 on average, and that number has dropped to about 165 by 2017. So what could have possibly caused this staggering drop? This is due to a combination of different factors such as medical interventions like statins, better management of high blood pressure and cholesterol due to lifestyle choices, and reduced smoking rates nationwide. Although heart disease remains the #1 leading cause of death in the US, it is certainly not as drastic the beginngng of the 19 years spanned in the data. 

## The Rise of Alzheimers and Unintentional Injuries

Through the visualization, it can be easily observed that most leading causes of death either decline over the years, or stagnates. However, there are two causes that slightly increase: Alzheimer's and Unintentional Injuries. Alzheimer's has a rate of 16.5 deaths per 100,000 in 1999, while it rises to 31 in 2017, almost double the rate. With unintentional injuries, the rate trends upward from 35.3 deaths to 49.4 deaths. The rise in deaths caused by Alzheimer's can be attributed to both higher rates of diagnoses (which might have been prevelant in the past, but just flew under the radar) and the aging population of the United States. For unintentional injuries, which can include drug overdoses and motor vehicle crashes. This is mostly driven by increased motor vehicle fatalities, the aging population (people pass away due to falls or drowning), and the opiods crisis in the 2010s, which can be observed by the slight uptick in the graph after 2010. 

## Contextual Visualiation 1: Obesity Trends

An important trend to note is the steady rise of obesity across the United States. In 2024, every U.S. state and territory had a 25% of higher obesity prevalence. As you can see in the map, most states have an overall obesity rate of around at least 30-40%. Obesity is very commonly linked to diseases such as diabetes and heart disease, and following this trend of increasing obesity rates can explain why the decline in heart disease is much slower than expected despite incredible advancements in technology. 

<img src="https://www.cdc.gov/obesity/media/images/2025/11/2024_Overall.svg" alt="Obseity Map from the CDC" style="width:100%; max-width:700px;">

*Source: Center for Disease Control and Prevention - Obseity (https://www.cdc.gov/obesity/data-and-statistics/adult-obesity-prevalence-maps.html)*

## Contextual Visualization 2: Smoking Rates

A key factor contributing to the decline in heart disease and cancer is the drop in smoking rates across the country. As seen in the visualzation, there has been a significant decline in smoking rates from 1965 to 2021, going from 42.4% to 11.6% in adults. Smoking is a leading cause of lung cancer, as well as responsible for many symptoms of heart disease. But as displayed in our original visualization, there has been a drop in both deaths caused by heart disease and cancer, and we can conclude that the drop in smoking rates has aided this outcome.

![Cigarette smoking rates for adults and youth in the US, 1965-2022](https://aricoulekar.github.io/assets/pngs/smoking_trends.png)

*Source: American Lung Association - Overall Smoking Trends (https://www.lung.org/research/trends-in-lung-disease/tobacco-trends-brief/overall-smoking-trends)*

## Conclusion

Understanding the trends that exist in both the leading causes of death as well as the factors that might influence these patterns are important for shaping public health policies. Tracking this data and making it understandable to the public can help highlight the importance of advancements in medical technology, and practices that can be detrimental to a person's health as shown by related trends. 

## Data Sources and Citations

1. [NCHS - Leading Causes of Death in the US](https://catalog.data.gov/dataset/nchs-leading-causes-of-death-united-states)
2. [CDC - Adult Obesity Prevalence Maps](https://www.cdc.gov/obesity/data-and-statistics/adult-obesity-prevalence-maps.html#cdc_data_surveillance_section_15-map-overall-obesity)
3. [American Lung Association - Overall Smoking Trends](https://www.lung.org/research/trends-in-lung-disease/tobacco-trends-brief/overall-smoking-trends)
4. [Analysis notebook](https://github.com/aricoulekar/aricoulekar.github.io/blob/main/python_notebooks/nchs.ipynb)
