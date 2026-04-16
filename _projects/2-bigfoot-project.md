---
name: Bigfoot Sightings Visualization
tools: [Python, Altair, vega-lite]
image: 
description: An exploration of Bigfoot sighting reports across the US using interactive visualizations.
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---

# Bigfoot Sightings in the US

## Plot 1: Sightings by State and Classification

This chart visualizes the total number of Bigfoot sightings reported across the continental United States, broken down by report classification. Each bar represents a state, and the height of the bar corresponds to the total number of sightings in that state. The bars are stacked by classification, allowing the viewer to compare both the overall volume of sightings per state and the proportion of each classification type within that state. For encoding types, the x-axis uses a nominal encoding for state names, and the y-axis uses a quantitative encoding for the count of sightings. Color is used as a nominal encoding to distinguish between the three classification types: Class A, Class B, and Class C. The color scheme uses Altair's default categorical color palette. Before plotting, the data was transformed using a pandas groupby aggregation on the state and classification columns, counting the number of reports in each group. This aggregated count was stored in a new column called count and passed to Altair, rather than passing the raw row-level data.

<vegachart schema-url="{{ site.baseurl }}/assets/json/bigfoot_barchart.json" style="width: 100%"></vegachart>

## Plot 2: Interactive Map of Sightings by Season

This chart visualizes the geographic distribution of Bigfoot sightings across the continental United States. Each point on the map represents a single reported sighting, plotted at its recorded latitude and longitude. The map allows the viewer to explore where sightings are most densely concentrated and whether seasonal patterns emerge across different regions of the country. Longitude and latitude are used as quantitative encodings to position each point geographically on the map. Color is used as a nominal encoding to represent the season in which each sighting was reported, using intuitive seasonal colors: green for Spring, yellow for Summer, orange for Fall, blue for Winter, and gray for Unknown. Before plotting, all rows with missing latitude or longitude values were dropped, and the data was filtered to only include sightings within the bounds of the continental United States, bringing the final count to 3,786 rows. A dropdown selection filter was added that allows the user to filter the displayed points by classification (Class A, Class B, or Class C). When a classification is selected, matching points remain fully visible while unselected points fade to near-invisibility, allowing the viewer to isolate and compare the geographic distribution of each classification type independently.

<vegachart schema-url="{{ site.baseurl }}/assets/json/bigfoot_map.json" style="width: 100%"></vegachart>

<div class="left">
{% include elements/button.html link="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/aricoulekar/aricoulekar.github.io/blob/main/python_notebooks/bigfoot_analysis.ipynb" text="The Analysis" %}
</div>
</a>
</div>
</a>
</div>
