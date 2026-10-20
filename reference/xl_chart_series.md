# A data series within a chart

\`xl_chart_series()\` names the values a chart plots, and optionally the
categories to plot them against and a name for the legend. A series that
plots a column is named after that column's header unless told
otherwise.

Each range may live on a different sheet from the chart, so it takes an
optional \`sheet\`:

\* \`"Data!B2:B10"\` — an A1 range, sheet-qualified; \* \`list(cols =
"revenue")\` — resolved against the chart's own sheet; \* \`list(sheet =
"Data", cols = "revenue")\` — against another sheet; \* \`list(header =
"revenue")\` — that column's header cell, which is where a series name
usually lives.

A range that selects no data is an error rather than an empty chart.

## Usage

``` r
xl_chart_series(
  values,
  categories = NULL,
  name = NULL,
  format = NULL,
  marker = NULL,
  labels = NULL,
  trendline = NULL,
  x_error_bars = NULL,
  y_error_bars = NULL,
  points = NULL,
  smooth = NA,
  invert_if_negative = NA
)
```

## Arguments

- values:

  The range holding the numbers to plot.

- categories:

  The range holding the labels to plot them against. Omit for a chart
  that numbers its points.

- name:

  The series name, shown in the legend. Left unset, a series that plots
  a column takes its name from that column's header cell, which is what
  Excel does when you chart a column along with its header; \`FALSE\`
  leaves it unnamed. A string is always taken literally — a series may
  legitimately be called \`"Q1!"\` — so to take the name from another
  cell, give a range spec: \`name = list(header = "cost")\` for a
  different column's header, or \`name = list(rows = 1, cols = 1)\` for
  a data cell.

- format:

  An \[xl_format\] styling the series — its line and fill. See
  \[xl_chart()\] for which format properties a chart can express.

- marker:

  An \[xl_chart_marker()\] drawn at each point.

- labels:

  An \[xl_chart_labels()\] printing the numbers beside the points.

- trendline:

  An \[xl_chart_trendline()\] fitted through the series.

- x_error_bars, y_error_bars:

  An \[xl_chart_error_bars()\] on each point.

- points:

  An \[xl_format()\] per point, as a list, styling individual points —
  one slice of a pie, one bar of a column chart. \`NULL\` in the list
  leaves that point as it is.

- smooth:

  Draw the line smoothed. Line and scatter charts only.

- invert_if_negative:

  Fill negative values with the inverse colour.

## Value

An \`xl_chart_series\` object.

## See also

\[xl_chart\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_series(values = list(cols = "revenue"))
#> <xl_chart_series>
xl_chart_series(values = "Data!B2:B10", categories = "Data!A2:A10",
                name = "2024")
#> <xl_chart_series: 2024>
```
