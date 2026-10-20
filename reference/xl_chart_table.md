# The table of values under a chart

\`xl_chart_table()\` prints the plotted numbers in a grid beneath the
chart, which is Excel's "Data Table" chart element. It is given to
\[xl_chart()\] as \`data_table\`.

Naming none of the grid options leaves Excel's own: horizontal, vertical
and outline borders drawn, and no legend keys.

## Usage

``` r
xl_chart_table(
  show_keys = NA,
  horizontal_border = NA,
  vertical_border = NA,
  outline_border = NA,
  format = NULL
)
```

## Arguments

- show_keys:

  Print each series' legend swatch in the table.

- horizontal_border, vertical_border, outline_border:

  Which of the grid's borders to draw.

- format:

  An \[xl_format()\] styling the table's text — the \[xl_font()\] group
  only.

## Value

An \`xl_chart_table\` object.

## See also

\[xl_chart\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
xl_chart_table()
#> <xl_chart_table>
xl_chart_table(show_keys = TRUE, vertical_border = FALSE)
#> <xl_chart_table>
#>   set: show_keys, vertical 
```
