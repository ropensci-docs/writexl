# Error bars on a chart series

\`xl_chart_error_bars()\` draws an error bar at each point, and is given
to \[xl_chart_series()\] as \`x_error_bars\` or \`y_error_bars\`.

## Usage

``` r
xl_chart_error_bars(
  type,
  value = NA,
  direction = NULL,
  endcap = NA,
  format = NULL
)
```

## Arguments

- type:

  How the size of each bar is worked out: \`"std_error"\` for the
  standard error, \`"fixed"\` for a constant, \`"percentage"\` of the
  point's own value, or \`"std_dev"\` for that many standard deviations.

- value:

  The constant, the percentage, or the number of standard deviations.
  \`"std_error"\` needs none.

- direction:

  \`"both"\`, \`"plus"\` or \`"minus"\`.

- endcap:

  Draw the cap at the end of each bar. On by default.

- format:

  An \[xl_format()\] styling the bars — \[xl_border()\] only, since an
  error bar is a line.

## Value

An \`xl_chart_error_bars\` object.

## See also

\[xl_chart_series\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
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
xl_chart_error_bars("percentage", 5)
#> <xl_chart_error_bars>
#>   set: type, value 
xl_chart_error_bars("std_dev", 1, direction = "plus", endcap = FALSE)
#> <xl_chart_error_bars>
#>   set: type, value, direction, endcap 
```
