# Data labels on a chart series

\`xl_chart_labels()\` prints the numbers next to the points that carry
them. With no arguments it shows the value of each point, which is
Excel's own default.

\`xl_chart_label()\` describes one label, for \`custom\`: a label can be
given its own text or hidden, one point at a time.

Excel allows different label positions for different chart types, and
drops one that does not apply. The table is in libxlsxwriter's header
and is enforced here: \`"center"\` is allowed everywhere, \`"right"\`,
\`"left"\`, \`"above"\` and \`"below"\` on line and scatter charts,
\`"inside_base"\` on bar and column, \`"inside_end"\` and
\`"outside_end"\` on bar, column, pie and doughnut, and \`"best_fit"\`
on pie and doughnut.

## Usage

``` r
xl_chart_labels(
  show_value = NA,
  show_name = NA,
  show_category = NA,
  show_percentage = NA,
  show_legend_key = NA,
  num_format = NULL,
  position = NULL,
  separator = NULL,
  format = NULL,
  leader_lines = NA,
  custom = NULL
)

xl_chart_label(value = NULL, hide = NA, format = NULL)
```

## Arguments

- show_value, show_name, show_category, show_percentage:

  What each label holds: the point's value, the series name, the
  category, and the value as a percentage of the series. Naming any of
  them means the label holds exactly those, so \`show_percentage =
  TRUE\` alone gives a percentage and nothing else; naming none of them
  leaves Excel's default, the value. Percentages are meaningful on pie
  and doughnut charts.

- show_legend_key:

  Print the series' legend swatch in each label.

- num_format:

  A number format for the labels, as an Excel format string or an
  \[xl_num_format()\].

- position:

  Where the label sits relative to its point; see the description for
  which chart types allow which.

- separator:

  What joins the parts of a label when it holds more than one:
  \`"comma"\`, \`"semicolon"\`, \`"period"\`, \`"newline"\` or
  \`"space"\`.

- format:

  An \[xl_format()\] styling the labels. A label is a shape with text in
  it, so all of \[xl_font()\], \[xl_border()\] and \[xl_fill()\] apply.

- leader_lines:

  Draw a line from a label back to its point. Excel only shows one once
  the label has been dragged away from the point.

- custom:

  A list of \[xl_chart_label()\]s, one per point in order, giving
  individual labels their own text, styling, or \`hide = TRUE\`.
  \`NULL\` in the list leaves that point's label alone.

- value:

  The label's text. A string beginning with \`"="\` is a formula, so
  \`"=Sheet1!\$A\$1"\` takes the text from a cell.

- hide:

  Remove this point's label, leaving the others.

## Value

An \`xl_chart_labels\` object.

## See also

\[xl_chart_series\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_labels()
#> <xl_chart_labels>
xl_chart_labels(show_category = TRUE, show_percentage = TRUE,
                separator = "newline", position = "outside_end")
#> <xl_chart_labels>
#>   set: show_category, show_percentage, position, separator 
```
