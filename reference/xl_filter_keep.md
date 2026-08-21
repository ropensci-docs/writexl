# Which rows an Excel autofilter would leave visible

\`xl_filter_keep()\` answers, for a data frame and a set of
\[xl_filter()\] rules, the question \`xl_sheet(filter =)\` has to answer
internally: which rows does Excel leave visible? It writes nothing — it
is the matching rule on its own, exported because reproducing Excel's
filter semantics is hard to get right and useful outside writing a file.

The rules are described in detail under \[xl_filter()\], and were
established by measurement rather than from documentation: a workbook
was written with criteria set and no rows hidden, opened in Excel, and
Data \> Reapply pressed so that Excel computed each match itself.

## Usage

``` r
xl_filter_keep(data, filter)
```

## Arguments

- data:

  A data frame whose columns the filters name.

- filter:

  One \[xl_filter()\], or a list of them. Filters on different columns
  combine with AND, as they do in Excel.

## Value

A logical vector with one element per row of \`data\`, \`TRUE\` where
the row stays visible.

## Accuracy

This function tracks Excel's \*observed\* behaviour, so a case found to
disagree with Excel is treated as a bug and fixed, which may change the
rows it returns. One limitation is known: a filter written as a value
list (\`"=="\` without a wildcard, or \`list\`) matches the text a cell
\*\*displays\*\*, which writexl can only predict for the General format.
A numeric column carrying a custom number format may therefore display
differently from what is compared here — prefer a comparison such as
\`"\>="\` on such a column. Dates are refused outright for the same
reason. See \[xl_filter()\].

## See also

\[xl_filter\], \[xl_sheet\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md),
[`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md),
[`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md),
[`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md),
[`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)

## Examples

``` r
sales <- data.frame(fruit = c("apple", "banana", "cherry"),
                    qty = c(5, 150, 300))
xl_filter_keep(sales, xl_filter("qty", ">", 100))
#> [1] FALSE  TRUE  TRUE
sales[xl_filter_keep(sales, xl_filter("fruit", "==", "*a*")), ]
#>    fruit qty
#> 1  apple   5
#> 2 banana 150

# filters on different columns combine with AND
xl_filter_keep(sales, list(xl_filter("qty", ">", 100),
                           xl_filter("fruit", "==", "b*")))
#> [1] FALSE  TRUE FALSE
```
