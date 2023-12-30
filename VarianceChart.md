---
layout: default
title: Variance chart
parent: Domo
nav_order: 3
---

# Variance chart
{: .no_toc }

Mar 24, 2023 ∙ [Original document](https://domo-support.domo.com/s/article/000005156?language=en_US)
{: .fs-5 : .fw-300 }

Variance charts show the differences between two sets of data. Use this chart type to compare performance over time, identify trends, spot outliers, and track progress toward goals.

This article describes how to:

- TOC
{:toc}

## Understand variance charts

The following two-line chart shows sales versus budget data for the past three years. Although the lines are colored differently to distinguish between sales and budget, the chart does not highlight the differences between the data.

![Two-line chart](https://github.com/haileytapia/portfolio/assets/78626762/9c98424a-334c-4b49-bb4d-8f0b9d85932b)

The following variance chart shows the previous data more effectively by highlighting the delta, or difference, between sales and budget. This makes it easier to see how sales have changed over time relative to budget.

![Variance chart](https://github.com/haileytapia/portfolio/assets/78626762/23aa52fa-224e-443f-bfe5-4b90664c305b)

## Power variance charts

To power a variance chart, specify a `Date` field and an `Actual` value. You can also specify a `Target` value to highlight how much each value varies from the target. See [Understanding chart data](https://domo-support.domo.com/s/article/360043428693?language=en_US) for more information about value, category, and series data.

In Analyzer, you can choose the columns that contain the data for your variance chart. See [Applying dataset columns to your chart](https://domo-support.domo.com/s/article/360043428713?language=en_US) for more information.

The following image shows data from a typical column-based spreadsheet as a variance chart:

![Data converted from spreadsheet to variance chart.](https://github.com/haileytapia/portfolio/assets/78626762/62ef91ef-f7f1-44d4-8991-721566adbd5b)

## Customize variance charts

Use the Chart Properties tool to customize the appearance of a variance chart. See [Chart properties](https://domo-support.domo.com/s/article/360042925374?language=en_US) for more information.

The following table shows the unique properties of variance charts:

<table>
    <tbody>
        <tr>
            <td>
                <strong>Property</strong>
            </td>
            <td>
                <strong>Description</strong>
            </td>
            <td>
                <strong>Example</strong>
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Value Format
            </td>
            <td>
                Determines whether currency symbols are appended to values.
            </td>
            <td>
                —
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Value Decimal Places
            </td>
            <td>
                Determines the number of decimal places in values.
            </td>
            <td>
                —
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Percent Value Decimal Places
            </td>
            <td>
                Determines the number of decimal places in percent values.
            </td>
            <td>
                —
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Line Style
            </td>
            <td>
                Allows you to select a default, straight, curved, or steeped line style between points. You can see which one looks best for your data.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006u8jU" alt="Line Style">
                </figure>
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Positive Color
            </td>
            <td>
                Allows you to select the color displayed when the variance is positive.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006u8jZ" alt="Positive Color">
                </figure>
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Negative Color
            </td>
            <td>
                Allows you to select the color displayed when the variance is negative.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006u8je" alt="Negative Color">
                </figure>
            </td>
        </tr>
        <tr>
            <td>
                General &gt; Show Absolute Difference
            </td>
            <td>
                Displays the values as absolute differences relative to zero. This better visualizes the size or scope of the differences.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006u8kh" alt="Show Absolute Difference">
                </figure>
            </td>
        </tr>
        <tr>
            <td>
                Actual Line
            </td>
            <td>
                Allows you to set the type, color, and thickness of the actual line.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006uAdO" alt="Actual Line">
                </figure>
            </td>
        </tr>
        <tr>
            <td>
                Target Line
            </td>
            <td>
                Allows you to set the value, label, type, color, and thickness of the target line.
            </td>
            <td>
                <figure class="image">
                    <img src="https://domo-support.domo.com/servlet/rtaImage?eid=ka05w000001277K&amp;feoid=00N5w00000Ri7BU&amp;refid=0EM5w000006u8jo" alt="Target Line">
                </figure>
            </td>
        </tr>
    </tbody>
</table>

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
