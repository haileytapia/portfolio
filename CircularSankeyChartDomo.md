---
layout: default
title: Circular Sankey Chart
parent: Domo
grand_parent: Software
nav_order: 3
---

# Circular Sankey Chart
{: .no_toc }

Mar 22, 2023 ∙ [Domo Knowledge](https://domo-support.domo.com/s/article/000005156?language=en_US)
{: .fs-5 : .fw-300 }

{:  .about }
> Charts in Domo, an ABI platform, are visual representations of data that help users understand and analyze information more easily.

The Sankey chart—often called a flow diagram—is a great way to illustrate flows, including flows of energy, materials, and web page paths. In addition to the flow of an item, the Sankey chart captures the relative size of the flow itself by changing the line width from node to node. For more information, see our [Sankey Chart](https://domo-support.domo.com/s/article/360043429273?language=en_US) article.

Sankey charts consist of nodes, or end points, and colored arrows or lines. The following image shows a typical Sankey chart:

![Sankey chart](https://github.com/haileytapia/portfolio/assets/78626762/6f89c694-a97b-4aa0-b8c9-f3a4a05a911b)

The original Sankey chart is ideal for physical flows that go to a destination once per flow, like energy and materials. However, it's not ideal for recursive concepts like web traffic, where flows need to circle back to previous nodes and require special treatment to display properly. To meet these needs, Domo has created the circular Sankey chart.

The following image emphasizes the chart's circular reference:

![Circular Sankey chart](https://github.com/haileytapia/portfolio/assets/78626762/95b4b813-cf06-4b18-b068-266c803bc387)

## Power circular Sankey charts

A circular Sankey chart requires each of the following:

* **A `From` dimension:** The source of the flow.
* **A `To` dimension:** The destination of the flow.
* **A value:** The size of the flow.
* 
For information about value, category, and series data, see our article about [Understanding Chart Data](https://domo-support.domo.com/s/article/360043428693?language=en_US).

In Analyzer, you can choose the columns containing the data for your circular Sankey chart. For more information about choosing data columns, see our article about [Applying DataSet Columns to Your Chart](https://domo-support.domo.com/s/article/360043428713?language=en_US).

The following image shows how data from a typical column-based spreadsheet is converted into a circular Sankey chart:

![Data converted from spreadsheet to circular Sankey chart.](https://github.com/haileytapia/portfolio/assets/78626762/ccb84f53-8b9d-44b8-b083-5a82cdb5925c)

## Customize circular sankey chart

You can customize the appearance of a circular Sankey chart in several ways, many of which are possible with the **Chart Properties** tool. For more information, see our [Chart Properties](https://domo-support.domo.com/s/article/360042925374?language=en_US) article.



Some unique properties of circular Sankey charts are shown in the following table:
