# Package index

## Writing a workbook

- [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  : Export to xlsx
- [`xl_workbook()`](https://docs.ropensci.org/writexl/reference/xl_workbook.md)
  : A workbook: sheets plus workbook-level properties
- [`xl_properties()`](https://docs.ropensci.org/writexl/reference/xl_properties.md)
  : Workbook properties, defaults, and metadata

## Cell content

- [`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md)
  [`as.character(`*`<xl_cell_general>`*`)`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md)
  : General cell objects for Excel writing
- [`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  [`xl_hyperlink()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  [`xl_hyperlink_cell()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  : Excel Types
- [`xl_comment()`](https://docs.ropensci.org/writexl/reference/xl_comment.md)
  : Create a cell comment
- [`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)
  [`is_xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)
  [`as.character(`*`<xl_rich_string>`*`)`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)
  : A cell whose text has several formats
- [`xl_rich_run()`](https://docs.ropensci.org/writexl/reference/xl_rich_run.md)
  : One run of a rich (multi-format) string
- [`is_xl_comment()`](https://docs.ropensci.org/writexl/reference/is_xl_comment.md)
  : Test whether an object is an \`xl_comment\`

## Formatting

- [`xl_format()`](https://docs.ropensci.org/writexl/reference/xl_format.md)
  [`` `+`( ``*`<xl_format>`*`)`](https://docs.ropensci.org/writexl/reference/xl_format.md)
  : Combine cell-formatting groups into a single format
- [`xl_font()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  [`xl_fill()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  [`xl_border()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  [`xl_align()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  [`xl_num_format()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  [`xl_protection()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  : Cell formatting groups
- [`xl_color()`](https://docs.ropensci.org/writexl/reference/xl_color.md)
  : Normalize a color to a libxlsxwriter RGB integer
- [`is_xl_format()`](https://docs.ropensci.org/writexl/reference/is_xl_format.md)
  : Test whether an object is an \`xl_format\`

## Worksheet layout

- [`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md)
  : A worksheet with formatting and layout options
- [`xl_col_spec()`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md)
  [`xl_row_spec()`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md)
  : Column and row specifications for a worksheet
- [`xl_sheet_view()`](https://docs.ropensci.org/writexl/reference/xl_sheet_view.md)
  : How a worksheet appears when it opens
- [`xl_page_setup()`](https://docs.ropensci.org/writexl/reference/xl_page_setup.md)
  : How a worksheet prints
- [`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md)
  : Control how outline (grouping) symbols are drawn

## Worksheet features

- [`xl_cond_cell()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  [`xl_cond_scale()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  [`xl_cond_bar()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  [`xl_cond_icons()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  : Format cells according to their contents
- [`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)
  : Restrict what can be typed into a range
- [`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md)
  : Filter an autofilter column, hiding the rows that do not match
- [`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md)
  : Which rows an Excel autofilter would leave visible
- [`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md)
  : Add a worksheet table
- [`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md)
  : Describe a column of a worksheet table
- [`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md)
  : Merge a range of cells

## The bundled library

- [`lxw_version()`](https://docs.ropensci.org/writexl/reference/writexl.md)
  : Version

## Charts and images

- [`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md)
  : Add a chart to a worksheet
- [`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md)
  : A data series within a chart
- [`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md)
  : An axis of a chart
- [`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md)
  : A marker on a chart series
- [`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md)
  [`xl_chart_label()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md)
  : Data labels on a chart series
- [`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md)
  : A trendline on a chart series
- [`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md)
  : Error bars on a chart series
- [`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md)
  : A chart's legend
- [`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md)
  : The table of values under a chart
- [`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md)
  : A sheet holding a single chart
- [`xl_image()`](https://docs.ropensci.org/writexl/reference/xl_image.md)
  : Insert an image into a worksheet
