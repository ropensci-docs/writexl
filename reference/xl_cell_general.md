# General cell objects for Excel writing

\`xl_cell_general\` creates a vector of cell objects, each optionally
containing a \*\*value\*\*, a \*\*formula\*\*, and/or a
\*\*hyperlink\*\*. It is the fundamental building block used internally
by \[xl_formula()\] and \[xl_hyperlink()\], and can be used directly for
mixed-type columns or cells that combine multiple features (e.g., a
formula with a pre-calculated result, or a URL with separate display
text and tooltip).

An \`xl_cell_general\` behaves like a vector: it has a \`length()\`,
supports \`\[\`, \`\[\[\`, \`c()\` and \`rep()\`, and recycles
automatically when assigned to a data frame column of a different length
(just like \[xl_formula()\]). It is deliberately not a list, so that
\`df\[, j\] \<- cells\` assigns one column rather than being read as a
list of them.

\`df\[i, j\] \<- x\` sets that cell's \`value\`, whatever \`x\`'s type;
a formula needs \[xl_formula()\], since a cell column carries no
column-wide notion of "these are all formulas".

\`as.character()\` returns what each cell displays, so a cell built for
a sheet can be reused wherever a plain string is wanted —
\[xl_merge()\]'s or \[xl_comment()\]'s \`value\`, for instance. A cell
that carries only a formula shows \`NA\`: its displayed value comes from
Excel, not from writexl.

## Usage

``` r
xl_cell_general(
  value = NULL,
  formula = NULL,
  hyperlink = NULL,
  format = NULL,
  comment = NULL,
  array = FALSE,
  dynamic = FALSE,
  array_range = NULL,
  na = NA
)

# S3 method for class 'xl_cell_general'
as.character(x, ...)
```

## Arguments

- value:

  An atomic vector or a list of scalars, one per cell. Use \`NA\` for a
  cell that is empty unless \`na\` says otherwise (see \`na\` below, and
  note that a workbook-wide \`na\` reaches these values too). A list
  enables mixed types across cells in the same column (e.g., \`list(1.5,
  "text", TRUE)\`). Date and POSIXct scalars are supported and formatted
  as in \[write_xlsx()\]. When \`hyperlink\` is also set for the same
  cell, a \*\*character\*\* \`value\` is used as the display text shown
  in the cell instead of the raw URL; all other types are ignored for
  hyperlink cells.

- formula:

  A character vector of Excel formulas (each must start with \`"="\`),
  or \`NA\` for cells with no formula. When both \`value\` and
  \`formula\` are supplied for the same cell, \`value\` is used as a
  pre-calculated result stored alongside the formula via
  \`worksheet_write_formula_num()\` (numeric value) or
  \`worksheet_write_formula_str()\` (character value). This allows
  static xlsx exports that display formula text in the formula bar but
  do not require Excel to recalculate on open.

- hyperlink:

  A character vector of URLs, or a list where each element is \`NA\`, a
  single character URL, or a named list with elements:

  \`url\`

  :   (required) The target URL.

  \`tooltip\`

  :   (optional) Tooltip text shown on hover.

  Supply a character \`value\` alongside \`hyperlink\` to show custom
  display text in the cell instead of the raw URL. The hyperlink is
  written via \`worksheet_write_url_opt()\`.

- format:

  An \[xl_format\] object (applied to every cell), or a list of
  \`xl_format\` objects (one per cell, recycled), or \`NULL\` for no
  formatting. Build formats with \[xl_font()\], \[xl_fill()\],
  \[xl_border()\], \[xl_align()\], \[xl_num_format()\] and
  \[xl_protection()\], combined with \[xl_format()\] or \`+\`. When a
  cell's value is a date/time and its format sets no number format, the
  default date/time number format is applied automatically.

- comment:

  Cell comments (notes): a character vector of comment text (one per
  cell, recycled; \`NA\` for no comment), a single \[xl_comment()\]
  (recycled to every cell), or a list mixing strings / \`xl_comment\` /
  \`NA\` per cell. \`NULL\` for no comments.

- array, dynamic:

  Logical (one per cell, recycled): how the cell's \`formula\` is
  stored. \`array = TRUE\` writes a legacy \*array\* (Ctrl-Shift- Enter)
  formula; \`dynamic = TRUE\` writes a modern \*dynamic array\* formula,
  which Excel spills over as many cells as the result needs. Neither can
  carry a character \`value\`, because Excel stores no cached string
  result for an array formula. On a cell that has no \`formula\` the
  flags are inert, so a single \`array = TRUE\` can be recycled across a
  column that mixes formula and value cells.

- array_range:

  The range a legacy array formula covers, for the rare case where it
  must be declared: an Excel range string (\`"C2:C11"\`) or a
  \`list(rows = , cols = )\` spec, one per cell (\`NA\` for none). It
  must start at the cell holding the formula, and must extend into cells
  the sheet does not otherwise write — the range is padded on write, so
  an overlap would have the padding and the sheet's own values overwrite
  each other.

  Leave it unset for almost everything: a single-cell \`dynamic\`
  formula spills automatically in Excel 365 / 2021, and a single-cell
  \`array\` formula is the right spelling for a \`SUMPRODUCT\`-style
  aggregate. Supplying it forces the workbook out of the
  memory-efficient row-streaming mode, since libxlsxwriter cannot pad an
  array range while streaming.

- na:

  What to write in a cell that has no value, one per cell and recycled.
  \`NA\` (the default) inherits the column's \[xl_col_spec()\]\`(na =
  )\`, and failing that the workbook's \[xl_properties()\]\`(na = )\`; a
  cell that sets its own overrides both. This is also how a cell asks
  for a blank where the column or workbook would otherwise substitute
  something — give it the value you want, \`""\` for an empty string.

- x:

  An \`xl_cell_general\`.

- ...:

  Ignored.

## Value

An object of class \`c("xl_cell_general", "xl_cell")\`, which is a list
of length \`n\` where each element is a named list with fields
\`value\`, \`formula\`, \`hyperlink\`, \`format\`, \`comment\`,
\`array\`, \`dynamic\` and \`array_range\`.

## See also

\[xl_formula()\], \[xl_hyperlink()\], \[write_xlsx()\]

Other cell content:
[`is_xl_comment()`](https://docs.ropensci.org/writexl/reference/is_xl_comment.md),
[`xl_comment()`](https://docs.ropensci.org/writexl/reference/xl_comment.md),
[`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md),
[`xl_rich_run()`](https://docs.ropensci.org/writexl/reference/xl_rich_run.md),
[`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)

## Examples

``` r
# Value-only cell
xl_cell_general(value = 42)
#> [xl_cell_general: 1 cell]
#>   [1] value=42

# Formula with a pre-calculated numeric result (static export)
xl_cell_general(value = 42.0, formula = "=SUM(A1:A10)")
#> [xl_cell_general: 1 cell]
#>   [1] value=42, formula==SUM(A1:A10)

# Hyperlink with display text (value) and tooltip
xl_cell_general(
  value    = "Visit",
  hyperlink = list(url = "https://example.com", tooltip = "Go to example.com")
)
#> [xl_cell_general: 1 cell]
#>   [1] value=Visit, hyperlink=<set>

# Vector of cells: value and formula cells in one column
cells <- c(
  xl_cell_general(value = 1.5),
  xl_cell_general(value = "note"),
  xl_cell_general(formula = "=A1+A2")
)

# Used in a data frame (length-1 recycles to fill all rows, as with
# xl_formula())
df <- data.frame(x = 1:3)
df$formula_col <- xl_formula("=A1*2")   # backward-compatible shorthand
df$cell_col    <- xl_cell_general(value = 99L)  # all rows get 99
```
