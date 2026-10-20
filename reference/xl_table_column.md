# Describe a column of a worksheet table

\`xl_table_column()\` overrides what \[xl_table()\] does with one
column: its header caption, a formula filling the column, what its
total-row cell shows, and the formats applied to the header and the data
cells.

Only the columns you name need an entry; the rest take the data frame's
column name as their header and are left otherwise alone.

## Usage

``` r
xl_table_column(
  col,
  header = NULL,
  formula = NULL,
  total = NULL,
  total_label = NULL,
  total_value = NULL,
  format = NULL,
  header_format = NULL
)
```

## Arguments

- col:

  The column: a name or a 1-based position within the table's range.

- header:

  The header caption. Defaults to the data frame's column name — which
  is also what makes a table safe to add, since Excel rejects a file
  whose table definition and header cells disagree.

- formula:

  A formula filling every data cell of the column, usually with a
  structured reference such as \`"=SUM(Sales\[@\[Q1\]:\[Q4\]\])"\`.
  Because those name the table, see the \`name\` argument of
  \[xl_table()\].

- total:

  The function shown in this column's total-row cell: one of \`"sum"\`,
  \`"average"\`, \`"count"\`, \`"count_nums"\`, \`"max"\`, \`"min"\`,
  \`"std_dev"\` or \`"var"\`. Needs \`total_row = TRUE\` on the table.

- total_label:

  A string for the total-row cell instead of a function — typically
  \`"Total"\` under the first column.

- total_value:

  The number the total-row cell already holds. Excel recalculates
  \`total\` on open and ignores this, but a reader that does not
  evaluate formulas — \[readxl::read_xlsx()\] among them — shows what is
  cached, which without this is nothing.

- format:

  An \[xl_format\] applied to the column's data cells.

- header_format:

  An \[xl_format\] applied to the column's header cell.

## Value

An \`xl_table_column\` object.

## See also

\[xl_table\], \[xl_sheet\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md),
[`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md),
[`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md),
[`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md),
[`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)

## Examples

``` r
xl_table_column("qty", total = "sum")
#> <xl_table_column: qty total=sum>
xl_table_column("fruit", total_label = "Total")
#> <xl_table_column: fruit>
xl_table_column("margin", formula = "=Sales[@revenue] * 0.3")
#> <xl_table_column: margin formula>
```
