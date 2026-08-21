# Restrict what can be typed into a range

\`xl_validation()\` adds Excel data validation to a range: a dropdown
list, a numeric or date bound, a text-length limit, or a custom formula.
Pass one or a list of them as \`xl_sheet(validation = )\`.

Excel's 17 internal validation types are collapsed into the five
\`type\` kinds below. Whether a limit is a literal, a cell formula or a
date is inferred from what you pass: a string starting with \`"="\` is a
formula, and a \`Date\` or \`POSIXct\` is a date/time bound.

## Usage

``` r
xl_validation(
  range,
  type = "any",
  criteria = NA,
  value = NULL,
  min = NULL,
  max = NULL,
  list = NULL,
  input_title = NA,
  input_message = NA,
  error_title = NA,
  error_message = NA,
  error_type = NA,
  ignore_blank = NA,
  show_input = NA,
  show_error = NA,
  dropdown = NA
)
```

## Arguments

- range:

  The cells to validate: an Excel range string such as \`"B2:B100"\`, a
  single cell, or a \`list(rows = , cols = )\` spec.

- type:

  The kind of value allowed: \`"integer"\`, \`"decimal"\`, \`"date"\`,
  \`"time"\`, \`"length"\` (of the text entered), \`"custom"\` (any
  formula that must evaluate \`TRUE\`), or \`"any"\` (no restriction,
  useful when you only want the input message). Ignored when \`list\` is
  given.

- criteria:

  How \`value\` (or \`min\`/\`max\`) limits the entry: \`"between"\`,
  \`"not between"\`, \`"=="\`, \`"!="\`, \`"\>"\`, \`"\<"\`, \`"\>="\`
  or \`"\<="\`. Required for the numeric, date, time and length kinds;
  must not be given for \`list\`, \`custom\` or \`any\`, which carry
  their own meaning. Supplying \`min\` and \`max\` implies
  \`"between"\`.

- value:

  The single limit the criteria applies to. A number, a \`Date\` or
  \`POSIXct\`, or a \`"=..."\` formula.

- min, max:

  The two limits for \`"between"\` / \`"not between"\`. Supplying both
  and omitting \`criteria\` implies \`"between"\`.

- list:

  A dropdown of allowed values: a character vector of choices, or a
  single \`"=..."\` formula naming a range that holds them. The choices
  are stored joined by commas, and Excel limits that joined string to
  255 characters.

- input_title, input_message:

  Text shown in a tooltip when the cell is selected. Titles are limited
  to 32 characters and messages to 255.

- error_title, error_message:

  Text shown when an invalid entry is made. Same limits.

- error_type:

  What Excel does on an invalid entry: \`"stop"\` (refuse it),
  \`"warning"\` or \`"information"\` (both allow it through).

- ignore_blank:

  Logical; allow an empty cell. \`TRUE\` by default, as in Excel.

- show_input, show_error:

  Logical; whether the input tooltip and the error alert are shown at
  all. Both \`TRUE\` by default.

- dropdown:

  Logical; show the in-cell dropdown arrow for a \`list\` validation.
  \`TRUE\` by default.

## Value

An \`xl_validation\` object.

## See also

\[xl_sheet\]

Other worksheet features:
[`xl_conditional`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
[`xl_filter()`](https://docs.ropensci.org/writexl/reference/xl_filter.md),
[`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md),
[`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md),
[`xl_table()`](https://docs.ropensci.org/writexl/reference/xl_table.md),
[`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md)

## Examples

``` r
# a dropdown
xl_validation("C2:C100", list = c("open", "high", "close"))
#> <xl_validation: list on C2:C100>

# a numeric bound, with the message Excel shows on a bad entry
xl_validation("B2:B100", type = "integer", min = 1, max = 10,
              error_message = "Enter a whole number from 1 to 10")
#> <xl_validation: integer on B2:B100>

# a date bound
xl_validation("D2:D100", type = "date", criteria = ">=",
              value = as.Date("2024-01-01"))
#> <xl_validation: date on D2:D100>

df <- data.frame(qty = 1:3)
tmp <- write_xlsx(list(Data = xl_sheet(df,
  validation = xl_validation("A2:A4", type = "integer", min = 0, max = 99))))
```
