# A sheet holding a single chart

\`xl_chartsheet()\` is a worksheet-sized chart: a tab of its own holding
one chart and no cells. Give it to \[write_xlsx()\] in place of a data
frame.

Because a chartsheet has no cells, every range in the chart's series
must name the sheet it plots — \`list(sheet = "Data", cols =
"revenue")\` or \`"Data!B2:B10"\`. A bare \`list(cols = )\` has nothing
to resolve against and is refused.

A chartsheet supports only part of what a worksheet does, and the parts
it does not are refused rather than dropped: of \[xl_page_setup()\] it
takes the orientation, paper size, margins and the header and footer; of
\[xl_sheet_view()\] it takes \`active\`, \`selected\`, \`visible\` and
\`first_tab\`.

## Usage

``` r
xl_chartsheet(
  chart,
  tab_color = NULL,
  zoom = NA,
  protect = NULL,
  page = NULL,
  view = NULL
)
```

## Arguments

- chart:

  The \[xl_chart()\] to fill the sheet with.

- tab_color:

  The colour of the sheet tab.

- zoom:

  The zoom level as a percentage, 10 to 400.

- protect:

  \`TRUE\`, a password string, or a named list. A chartsheet has no
  cells, so of Excel's protection options it takes only \`no_content\`
  (let the chart be edited) and \`no_objects\` (let the shapes on it be
  edited); the worksheet options are refused by name.

- page:

  An \[xl_page_setup()\] describing how it prints.

- view:

  An \[xl_sheet_view()\] setting the tab state.

## Value

An \`xl_chartsheet\` object.

## See also

\[xl_chart\], \[xl_sheet\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)

## Examples

``` r
sales <- data.frame(quarter = c("Q1", "Q2"), revenue = c(10, 25))
chart <- xl_chart("column",
                  xl_chart_series(values = list(sheet = "Data",
                                                cols = "revenue")))
write_xlsx(list(Data = sales, Overview = xl_chartsheet(chart)),
           tempfile(fileext = ".xlsx"))
```
