# Filter an autofilter column, hiding the rows that do not match

\`xl_filter()\` sets the criteria on one autofilter column \*and\* hides
the rows that do not match. Both halves are necessary: Excel stores the
criteria and the hidden rows separately and does not apply a filter when
a file is opened, so criteria alone produce a sheet that looks filtered
but shows every row.

Because writexl decides which rows to hide, it reproduces Excel's own
matching rules, which were measured in Excel rather than assumed. Those
rules depend on which of two forms the filter takes:

\* \`"=="\` (with no wildcard) and \`"blanks"\`, and any \`list\`, are
written as a \*\*value list\*\*. Excel matches these against the text a
cell \*displays\*, case-insensitively — so \`"=="\` with \`10\`, with
\`"10"\`, or a \`list\` of \`"10"\` all match both the number \`10\` and
the string \`"10"\`. \* every other criteria, including \`"=="\` with a
\`\*\` or \`?\` in it, is written as a \*\*typed comparison\*\*. If the
value is a number the comparison is numeric and a text cell never
satisfies it (except \`"!="\`, which a text cell satisfies because it is
not that number). If the value is text the comparison is textual,
case-insensitive, with \`\*\` and \`?\` as wildcards, and a number cell
never satisfies it.

The consequence worth knowing is that \`"=="\` with \`"10"\` keeps the
number \`10\`, while \`"=="\` with \`"1\*"\` keeps nothing on a numeric
column: the wildcard changes the form, and so the rule.

Blank means an empty cell or an empty string; \`"non-blanks"\` is its
exact complement. Blanks are excluded by every comparison except
\`"!="\`, which keeps them — a blank is not equal to anything. A
mixed-type column built with \[xl_cell_general()\] is matched cell by
cell, each by its own type.

## Usage

``` r
xl_filter(
  col,
  criteria = NA,
  value = NULL,
  criteria2 = NA,
  value2 = NULL,
  and_or = "and",
  list = NULL
)
```

## Arguments

- col:

  The column to filter: a name or a 1-based position.

- criteria:

  One of \`"=="\`, \`"!="\`, \`"\>"\`, \`"\<"\`, \`"\>="\`, \`"\<="\`,
  \`"blanks"\` or \`"non-blanks"\`. The four magnitude comparisons need
  a numeric value; writexl will not guess how Excel orders text.

- value:

  The value to compare against. In a text comparison \`\*\` matches any
  run of characters and \`?\` any single one.

- criteria2, value2:

  An optional second rule for the same column.

- and_or:

  How the two rules combine: \`"and"\` (default) or \`"or"\`.

- list:

  Instead of a criteria, keep only rows whose value is in this character
  vector. Matched case-insensitively, as Excel does.

## Value

An \`xl_filter\` object.

## Limitations

A value list matches displayed text, which writexl can only predict for
the General format. Filtering a \`Date\` or \`POSIXct\` column by
\`"=="\` or \`list\` is therefore refused — use a comparison such as
\`"\>="\`. For the same reason a numeric column carrying a custom number
format (say two decimal places, or a currency symbol) may display
differently from what writexl compares, so prefer a comparison there
too. Columns whose cells hold formulas cannot be filtered at all, since
writexl does not know what Excel would compute.

## See also

\[xl_sheet\], \[xl_filter_keep\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md),
[`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md),
[`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md),
[`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md),
[`xl_validation()`](https://docs.ropensci.org/writexl/reference/xl_validation.md)

## Examples

``` r
xl_filter("qty", ">", 100)
#> <xl_filter: qty > 100>
xl_filter("qty", ">", 100, "<", 200)          # between, via two rules
#> <xl_filter: qty > 100>
xl_filter("fruit", "==", "ap*")               # wildcard: typed comparison
#> <xl_filter: fruit == ap*>
xl_filter("fruit", list = c("apple", "banana"))
#> <xl_filter: fruit in 2 value(s)>
xl_filter("qty", "==", "10")                  # value list: matches the
#> <xl_filter: qty == 10>
                                              # number 10 and the text "10"
```
