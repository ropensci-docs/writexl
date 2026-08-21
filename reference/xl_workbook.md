# A workbook: sheets plus workbook-level properties

\`xl_workbook()\` binds one or more sheets (data frames or
\[xl_sheet\]s) to a set of \[xl_properties\]. It is the single place to
attach workbook-level formatting defaults and metadata. When passed to
\[write_xlsx()\], the workbook's \`col_names\` and \`format_headers\`
settings take precedence over \`write_xlsx()\`'s own arguments.

## Usage

``` r
xl_workbook(
  sheets,
  properties = xl_properties(),
  col_names = TRUE,
  format_headers = TRUE
)
```

## Arguments

- sheets:

  A data frame, an \[xl_sheet\], or a (named) list of them.

- properties:

  An \[xl_properties\] object.

- col_names:

  write column names as the header row at the top of the sheet?

- format_headers:

  apply the workbook's header format to that header row? The default
  header format is bold and centered; change it with
  [`xl_properties`](https://docs.ropensci.org/writexl/reference/xl_properties.md)`(header_format = )`.

## Value

An \`xl_workbook\` object.

## See also

\[xl_properties\], \[xl_sheet\], \[write_xlsx\]

Other workbook settings:
[`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md),
[`xl_properties()`](https://docs.ropensci.org/writexl/reference/xl_properties.md)

## Examples

``` r
wb <- xl_workbook(
  list(Data = data.frame(x = 1:3)),
  properties = xl_properties(title = "Demo", author = "me")
)
tmp <- write_xlsx(wb)
```
