---
layout: default
title: Variance Chart
parent: Domo
grand_parent: Software
nav_order: 3
---

# Variance Chart
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

You can customize the appearance of a variance chart in several ways, many of which are possible with the **Chart Properties** tool. For more information, see our [Chart Properties](https://domo-support.domo.com/s/article/360042925374?language=en_US) article.

Some unique properties of variance charts are shown in the following table:

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
