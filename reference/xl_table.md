# Add a worksheet table

\`xl_table()\` turns a range into an Excel table: a named, styled block
with banded rows, a filter dropdown in its header, and an optional total
row. Pass one or a list of them as \`xl_sheet(table = )\`.

Column headers default to the data frame's column names. That is not
just a convenience: Excel records a table's column names separately from
the header cells and rejects a file where the two disagree, so the
default is what makes a table safe to add at all.

## Usage

``` r
xl_table(
  range = NULL,
  name = NULL,
  style = "medium 9",
  header_row = TRUE,
  autofilter = TRUE,
  banded_rows = TRUE,
  banded_columns = FALSE,
  first_column = FALSE,
  last_column = FALSE,
  total_row = FALSE,
  columns = NULL
)
```

## Arguments

- range:

  The cells the table covers, as an Excel range string or a \`list(rows
  = , cols = )\` spec. Defaults to the sheet's used range, including the
  header row and, with \`total_row = TRUE\`, one row below.

- name:

  The table's name. See "Table names".

- style:

  The table style: \`"none"\`, or a type and number such as \`"medium
  9"\` (the default), \`"light 21"\` or \`"dark 11"\`. Light styles are
  numbered 0–21, medium 1–28 and dark 1–11.

- header_row:

  Show the header row. Turning it off also removes the filter dropdown,
  as it does in Excel.

- autofilter:

  Show the filter dropdown in the header row.

- banded_rows, banded_columns:

  Alternating row / column shading.

- first_column, last_column:

  Highlight the first / last column.

- total_row:

  Add a total row below the data. See "The total row".

- columns:

  One \[xl_table_column()\], or a list of them, overriding individual
  columns.

## Value

An \`xl_table\` object.

## Table names

Excel requires table names to be unique across the workbook, and
formulas refer to a table by name. \`name = NULL\` (the default) has
writexl generate a unique name from the sheet name and write it
explicitly, so it cannot shift when another table is added elsewhere.
Give a string to choose your own; it is validated and checked for
collisions. Give \`NA\` to write no name at all and let Excel assign
\`Table1\`, \`Table2\`, ... by insertion order — which makes any formula
naming the table fragile, so that combination warns.

## The total row

A total row is written by libxlsxwriter below the data, and the sheet's
row plan does not know about it: \`auto_colwidth\` does not measure it,
and an \[xl_row_spec()\] aimed at that row will fight it. It has no
cells of its own until a column gives a \`total\` or \`total_label\`.

## See also

\[xl_table_column\], \[xl_sheet\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md),
[`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md),
[`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md),
[`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md),
[`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)

## Examples

``` r
xl_table(style = "light 9")
#> <xl_table: unnamed, 0 column override(s)>
xl_table(name = "Sales", total_row = TRUE,
         columns = list(xl_table_column("fruit", total_label = "Total"),
                        xl_table_column("qty", total = "sum")))
#> <xl_table: Sales, total row, 2 column override(s)>
```
