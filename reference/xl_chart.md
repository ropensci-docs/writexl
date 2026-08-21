# Add a chart to a worksheet

\`xl_chart()\` builds a chart from one or more \[xl_chart_series()\] and
places it on a sheet, anchored to a cell. Pass one or a list of them as
\`xl_sheet(chart = )\`.

Placement works exactly as it does for \[xl_image()\] — \`at\`,
\`scale\`, \`offset\`, \`position\`, \`description\` and \`decorative\`
mean the same things, because libxlsxwriter describes both with the same
fields.

## Usage

``` r
xl_chart(
  type,
  series,
  title = NULL,
  title_format = NULL,
  title_layout = NULL,
  title_overlay = NA,
  x_axis = NULL,
  y_axis = NULL,
  legend = NULL,
  data_table = NULL,
  plot_area_format = NULL,
  plot_area_layout = NULL,
  chart_area_format = NULL,
  drop_lines = NA,
  high_low_lines = NA,
  up_down_bars = NA,
  hole_size = NA,
  rotation = NA,
  series_gap = NA,
  series_overlap = NA,
  show_blanks = NULL,
  show_hidden_data = NA,
  at = "A1",
  scale = 1,
  offset = NULL,
  position = "move_and_size",
  description = NULL,
  decorative = FALSE,
  style = NA
)
```

## Arguments

- type:

  The chart type: \`"column"\`, \`"bar"\`, \`"line"\`, \`"pie"\`,
  \`"doughnut"\`, \`"area"\`, \`"scatter"\`, \`"radar"\`, and the
  stacked, percent-stacked, smoothed and marker variants.

- series:

  One \[xl_chart_series()\], or a list of them. Every series of a
  scatter chart must have \`categories\`, which are its x axis.

- title:

  The chart title. A string is always taken literally, so to take the
  title from a cell give a range spec — \`list(header = "revenue")\` for
  a column's header cell, or \`list(rows = 1, cols = 1)\` for a data
  cell. \`FALSE\` removes the title Excel would otherwise generate.

- title_format:

  An \[xl_format()\] styling the title text. A title is text, so only
  the \[xl_font()\] group applies.

- title_layout:

  Where to put the title by hand, as \`c(x, y)\` fractions of the chart.
  Excel places it for you otherwise.

- title_overlay:

  Let the title sit over the plot rather than above it.

- x_axis, y_axis:

  An \[xl_chart_axis()\] describing that axis. Pie and doughnut charts
  have none, and several axis options apply to a value or a category
  axis only — see \[xl_chart_axis()\].

- legend:

  An \[xl_chart_legend()\] moving, styling or removing the legend.

- data_table:

  An \[xl_chart_table()\] printing the plotted numbers in a grid beneath
  the chart.

- plot_area_format, chart_area_format:

  An \[xl_format()\] styling the plot area — the panel the data is drawn
  in — and the chart area around it: \[xl_border()\] for the line,
  \[xl_fill()\] for the fill or pattern.

- plot_area_layout:

  Where to put the plot area by hand, as \`c(x, y)\` or \`c(x, y, width,
  height)\` fractions of the chart.

- drop_lines:

  Drop lines from each point to the category axis: \`TRUE\`, or an
  \[xl_format()\] giving the line to draw them with. Line and area
  charts.

- high_low_lines:

  A line joining the highest and lowest series at each category, the
  same way. Line charts.

- up_down_bars:

  Bars between the first and last series at each category: \`TRUE\`, or
  \`list(up = , down = )\` with an \[xl_format()\] for either bar. Line
  charts.

- hole_size:

  The size of a doughnut's hole, 10 to 90 percent.

- rotation:

  Where a pie or doughnut starts, 0 to 360 degrees clockwise from the
  top.

- series_gap:

  The gap between category groups on a bar or column chart, 0 to 500
  percent of a bar's width.

- series_overlap:

  How far bars of one category overlap, -100 to 100 percent. 100 stacks
  them, -100 pushes them apart.

- show_blanks:

  What an empty cell does to the plot: leave a \`"gap"\`, plot it as
  \`"zero"\`, or join across it with \`"connected"\`.

- show_hidden_data:

  Plot data from rows and columns that are hidden. Excel leaves them out
  otherwise.

- at:

  The cell the chart's top-left corner is anchored to.

- scale:

  Scale factor: one number for both axes, or \`c(x, y)\`.

- offset:

  Offset from the anchor cell's corner in pixels, as \`c(x, y)\`.

- position:

  How the chart behaves when rows and columns change size; see
  \[xl_image()\].

- description:

  Alt text, for screen readers.

- decorative:

  Mark the chart as decorative, so screen readers skip it.

- style:

  Excel's built-in chart style, 1–48.

## Value

An \`xl_chart\` object.

## What a chart type supports

Excel silently drops options a chart type cannot use, so writexl refuses
them instead, naming the types that would work. Pie and doughnut charts
have no axes; only a doughnut has a hole; only pie and doughnut rotate;
up-down bars and high-low lines are line-only; the series gap and
overlap are bar and column only.

## See also

\[xl_chart_series\], \[xl_sheet\]

Other images and charts:
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart("column", xl_chart_series(values = list(cols = "revenue")))
#> <xl_chart: column, 1 series>
xl_chart("pie", xl_chart_series(values = "Data!B2:B5"), title = "Share")
#> <xl_chart: pie, 1 series, "Share">
```
