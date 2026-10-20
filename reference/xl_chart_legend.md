# A chart's legend

\`xl_chart_legend()\` moves, styles or removes the legend, and can leave
individual series out of it.

## Usage

``` r
xl_chart_legend(
  position = NULL,
  format = NULL,
  layout = NULL,
  delete_series = NULL
)
```

## Arguments

- position:

  Where the legend sits: \`"right"\` (Excel's default), \`"left"\`,
  \`"top"\`, \`"bottom"\`, \`"top_right"\`, the \`"overlay\_\*"\`
  variants that let the legend sit over the plot, or \`"none"\` to
  remove it.

- format:

  An \[xl_format()\] styling the legend text — the \[xl_font()\] group
  only, since libxlsxwriter gives a legend a font and nothing else.

- layout:

  Where to put the legend by hand, as \`c(x, y)\` or \`c(x, y, width,
  height)\` — fractions of the chart, each above 0 and at most 1. Excel
  places it for you otherwise. \`at\` is a cell everywhere else in
  writexl, so a chart's own fractions are a \`layout\`.

- delete_series:

  Series to leave out of the legend, by position: \`2\` drops the second
  series' entry while still plotting it. This is how a trendline or a
  helper series is kept out of the key.

## Value

An \`xl_chart_legend\` object.

## See also

\[xl_chart\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_legend(position = "bottom")
#> <xl_chart_legend>
#>   set: position 
xl_chart_legend(position = "none")
#> <xl_chart_legend>
#>   set: position 
xl_chart_legend(delete_series = 2)
#> <xl_chart_legend>
#>   set: delete_series 
```
