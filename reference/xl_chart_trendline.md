# A trendline on a chart series

\`xl_chart_trendline()\` fits a line through a series.

Two of Excel's own restrictions are enforced, because it discards these
rather than complain: a \*\*moving average\*\* has no forecast, no
equation and no R-squared, and an \*\*intercept\*\* applies only to
exponential, linear and polynomial fits.

## Usage

``` r
xl_chart_trendline(
  type,
  order = NA,
  period = NA,
  forward = NA,
  backward = NA,
  intercept = NA,
  equation = NA,
  r_squared = NA,
  name = NULL,
  format = NULL
)
```

## Arguments

- type:

  \`"linear"\`, \`"log"\`, \`"poly"\`, \`"power"\`, \`"exp"\` or
  \`"average"\` for a moving average.

- order:

  The order of a polynomial fit, 2 or more. \`"poly"\` only.

- period:

  The number of points a moving average covers, 2 or more. \`"average"\`
  only.

- forward, backward:

  How far to project the line beyond the data, in categories.

- intercept:

  Force the line through this value on the y axis. Exponential, linear
  and polynomial fits only.

- equation:

  Print the fitted equation on the chart.

- r_squared:

  Print the R-squared value on the chart.

- name:

  The trendline's name in the legend. Excel generates one otherwise.

- format:

  An \[xl_format()\] styling the line — \[xl_border()\] only, since a
  trendline is a line.

## Value

An \`xl_chart_trendline\` object.

## See also

\[xl_chart_series\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_trendline("linear", equation = TRUE, r_squared = TRUE)
#> <xl_chart_trendline>
#>   set: type, equation, r_squared 
xl_chart_trendline("poly", order = 3)
#> <xl_chart_trendline>
#>   set: type, order 
xl_chart_trendline("average", period = 2)
#> <xl_chart_trendline>
#>   set: type, period 
```
