# A marker on a chart series

\`xl_chart_marker()\` draws a symbol at each point of a series. Line,
scatter and radar charts are where they show; on other types Excel
ignores them.

\`type = "automatic"\` asks Excel for the default marker of that series,
and is the one type that cannot be given a size or a format —
libxlsxwriter documents that, and Excel drops them, so both are refused
here.

## Usage

``` r
xl_chart_marker(type = NULL, size = NA, format = NULL)
```

## Arguments

- type:

  The symbol: \`"automatic"\`, \`"none"\`, \`"square"\`, \`"diamond"\`,
  \`"triangle"\`, \`"x"\`, \`"star"\`, \`"short_dash"\`,
  \`"long_dash"\`, \`"circle"\` or \`"plus"\`.

- size:

  The symbol's size in points, 2 to 72.

- format:

  An \[xl_format()\] styling the symbol: \[xl_border()\] for its
  outline, \[xl_fill()\] for its fill or pattern.

## Value

An \`xl_chart_marker\` object.

## See also

\[xl_chart_series\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_marker(type = "circle", size = 8)
#> <xl_chart_marker>
#>   set: type, size 
xl_chart_marker(type = "none")
#> <xl_chart_marker>
#>   set: type 
```
