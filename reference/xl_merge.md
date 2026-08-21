# Merge a range of cells

\`xl_merge()\` merges a rectangle of cells into one, as Excel's "Merge
and Centre" does. Pass one or a list of them as \`xl_sheet(merge = )\`.

A merged range holds a single value, so \`xl_merge()\` carries its own
\`value\` rather than taking it from the data frame. Merging over cells
the data frame filled keeps only the merged value, exactly as merging in
Excel discards everything but the top-left value.

## Usage

``` r
xl_merge(range, value = NULL, format = NULL)
```

## Arguments

- range:

  The cells to merge: an Excel range string such as \`"A1:C1"\`, or a
  \`list(rows = , cols = )\` spec. It must cover more than one cell —
  Excel has no single-cell merge.

- value:

  The value shown in the merged cell: a string, or anything with an
  \[as.character()\] method such as an \[xl_rich_string()\]. \`NULL\`
  leaves the cell empty.

- format:

  An optional \[xl_format\] applied to the whole merged range. Merged
  cells usually want \`xl_align(horizontal = "center")\`.

## Value

An \`xl_merge\` object.

## See also

\[xl_sheet\], \[xl_format\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md),
[`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md),
[`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md),
[`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md),
[`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)

## Examples

``` r
xl_merge("A1:C1", "Quarterly results",
         format = xl_align(horizontal = "center") + xl_font(bold = TRUE))
#> <xl_merge: A1:C1 "Quarterly results">

df <- data.frame(a = 1:3, b = 4:6)
sheet <- xl_sheet(df, merge = xl_merge("A5:B5", "Total",
                                       format = xl_font(bold = TRUE)))
tmp <- write_xlsx(list(Data = sheet))
```
