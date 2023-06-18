---
layout: default
title: Variance Charts in Domo
parent: Software
---

# Variance Charts in Domo
{: .no_toc }

Mar 24, 2023 ∙ [Domo Knowledge](https://domo-support.domo.com/s/article/000005156?language=en_US)
{: .fs-5 : .fw-300 }

{:  .about }
> Charts in Domo are visual representations of data that help users understand and analyze information more easily.

Unlike other chart types that show data directly, variance charts show the differences between two sets of data, such as actual versus budget or actual versus forecast.

Below are two charts. The first shows sales versus budget data as a simple two-line chart, while the second shows the same data as a variance chart. Notice that the variance chart highlights the delta, or difference, data. This is useful when you want to analyze differences between lines.

![Two-line chart](https://github.com/haileytapia/portfolio/assets/78626762/9c98424a-334c-4b49-bb4d-8f0b9d85932b)

![Variance chart](https://github.com/haileytapia/portfolio/assets/78626762/23aa52fa-224e-443f-bfe5-4b90664c305b)

## Power variance charts

A variance chart requires a `Date` field and an `Actual` value. Although not required, a `Target` value is key to emphasizing the power of the chart. For information about value, category, and series data, see our article about [Understanding Chart Data](https://domo-support.domo.com/s/article/360043428693?language=en_US).

In Analyzer, you can choose the columns containing the data for your variance chart. For more information about choosing data columns, see our article about [Applying DataSet Columns to Your Chart](https://domo-support.domo.com/s/article/360043428713?language=en_US).

The following image shows how data from a typical column-based spreadsheet is converted into a variance chart:

![Data converted from spreadsheet to variance chart.](https://github.com/haileytapia/portfolio/assets/78626762/62ef91ef-f7f1-44d4-8991-721566adbd5b)

## Customize variance charts
