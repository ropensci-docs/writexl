# An axis of a chart

\`xl_chart_axis()\` describes one axis, and is given to \[xl_chart()\]
as \`x_axis\` or \`y_axis\`.

Several options apply to one kind of axis only, and Excel discards the
rest without a word, so writexl refuses them instead. A scatter chart
plots numbers against numbers, so both of its axes are \*\*value\*\*
axes; every other type has a \*\*category\*\* x axis and a value y axis.
(A bar chart is drawn with its categories up the side, but the axes keep
their names.) Pie and doughnut charts have no axes at all.

\* value axes only — \`min\`, \`max\`, \`log_base\`, \`major_unit\`,
\`minor_unit\`, \`display_units\`, \`display_units_visible\`; \*
category axes only — \`position\`, \`label_align\`, \`interval_unit\`,
\`interval_tick\`.

## Usage

``` r
xl_chart_axis(
  title = NULL,
  title_format = NULL,
  title_layout = NULL,
  label_format = NULL,
  num_format = NULL,
  line_format = NULL,
  visible = NA,
  reverse = NA,
  min = NA,
  max = NA,
  log_base = NA,
  major_unit = NA,
  minor_unit = NA,
  display_units = NULL,
  display_units_visible = NA,
  interval_unit = NA,
  interval_tick = NA,
  position = NULL,
  label_position = NULL,
  label_align = NULL,
  major_tick = NULL,
  minor_tick = NULL,
  crossing = NULL,
  major_gridlines = NA,
  minor_gridlines = NA,
  major_gridlines_format = NULL,
  minor_gridlines_format = NULL
)
```

## Arguments

- title:

  The axis title: a string, or a range spec holding one — see
  \[xl_chart_series()\] for the spellings, including \`list(header =
  "revenue")\`.

- title_format:

  An \[xl_format()\] styling the axis title. A title is text, so only
  the \[xl_font()\] group applies.

- title_layout:

  Where to put the axis title by hand, as \`c(x, y)\` fractions of the
  chart, each above 0 and at most 1. Excel places it for you otherwise.

- label_format:

  An \[xl_format()\] styling the tick labels — the \[xl_font()\] group
  only.

- num_format:

  A number format for the tick labels, as an Excel format string
  (\`"#,##0"\`) or an \[xl_num_format()\].

- line_format:

  An \[xl_format()\] styling the axis line itself: \[xl_border()\] for
  the line, \[xl_fill()\] for the fill behind it. An axis has four parts
  that can be styled, so none of them is just \`format\`.

- visible:

  \`FALSE\` hides the axis.

- reverse:

  Draw the axis in the opposite direction.

- min, max:

  The axis bounds. Value axes only.

- log_base:

  Use a logarithmic scale with this base, 2 or more. Value axes only.

- major_unit, minor_unit:

  The spacing between major and minor tick marks. Value axes only.

- display_units:

  Scale the labels by \`"thousands"\`, \`"millions"\`, \`"billions"\`
  and so on; see Details for the full set. Value axes only.

- display_units_visible:

  Whether the caption naming the units — the small rotated "Millions"
  beside the axis — is drawn. Setting \`display_units\` turns it
  \*\*on\*\*, as Excel does, so this is really for \`FALSE\`: rescaled
  labels with no caption. Value axes only.

- interval_unit:

  Label one category in every \`n\`. Category axes only.

- interval_tick:

  Put a tick mark on one category in every \`n\`. Category axes only.

- position:

  Whether the data sits \`"on_tick"\` or \`"between"\` the tick marks.
  Category axes only.

- label_position:

  Where the tick labels go: \`"next_to"\`, \`"high"\`, \`"low"\`, or
  \`"none"\` for no labels.

- label_align:

  Tick-label alignment: \`"center"\`, \`"left"\` or \`"right"\`.
  Category axes only.

- major_tick, minor_tick:

  The tick marks: \`"default"\`, \`"none"\`, \`"inside"\`, \`"outside"\`
  or \`"crossing"\`.

- crossing:

  Where the other axis crosses this one: a number, or \`"min"\` or
  \`"max"\` for either end.

- major_gridlines, minor_gridlines:

  Show the gridlines. A chart's major y gridlines are on by default and
  everything else is off.

- major_gridlines_format, minor_gridlines_format:

  An \[xl_format()\] styling the gridlines — \[xl_border()\] only, since
  a gridline is a line.

## Value

An \`xl_chart_axis\` object.

## Details

\`display_units\` is one of \`"none"\`, \`"hundreds"\`, \`"thousands"\`,
\`"ten_thousands"\`, \`"hundred_thousands"\`, \`"millions"\`,
\`"ten_millions"\`, \`"hundred_millions"\`, \`"billions"\` or
\`"trillions"\`.

## See also

\[xl_chart\], \[xl_chart_series\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
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
xl_chart_axis(title = "Quarter")
#> <xl_chart_axis>
#>   set: title 
xl_chart_axis(title = "Revenue", min = 0, num_format = "$#,##0",
              major_gridlines = FALSE)
#> <xl_chart_axis>
#>   set: title, num_format, min, major_gridlines 
```
