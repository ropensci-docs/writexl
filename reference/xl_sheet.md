# A worksheet with formatting and layout options

\`xl_sheet()\` wraps a data frame together with worksheet-level options
(column/row formatting and geometry, frozen panes, gridlines, tab color,
zoom). Pass it anywhere \[write_xlsx()\] accepts a data frame; a plain
data frame continues to behave exactly as before.

## Usage

``` r
xl_sheet(
  data,
  cols = NULL,
  rows = NULL,
  freeze = NULL,
  gridlines = NA,
  tab_color = NA,
  zoom = NA,
  default_row_height = NA,
  auto_colwidth = FALSE,
  autofilter = FALSE,
  protect = FALSE,
  comment_author = NA,
  show_comments = FALSE,
  page = NULL,
  view = NULL,
  merge = NULL,
  validation = NULL,
  conditional = NULL,
  filter = NULL,
  outline = NULL,
  ignore_errors = NULL,
  table = NULL,
  image = NULL,
  background_image = NULL,
  chart = NULL
)
```

## Arguments

- data:

  A data frame (the sheet contents).

- cols:

  An \[xl_col_spec()\], or a list of them.

- rows:

  An \[xl_row_spec()\], or a list of them.

- freeze:

  Frozen panes: an Excel cell reference such as \`"A2"\` (freeze the
  rows above and columns left of that cell), or \`list(row =, col =)\`
  giving the number of rows/columns to freeze.

- gridlines:

  Logical; show (\`TRUE\`) or hide (\`FALSE\`) screen gridlines. \`NA\`
  leaves Excel's default.

- tab_color:

  Sheet tab color (see \[xl_color\]).

- zoom:

  Zoom level as a percentage (10–400).

- default_row_height:

  Default height (in points) for rows in the sheet.

- auto_colwidth:

  If \`TRUE\`, size each column to fit its contents (a character-count
  heuristic, since the xlsx format has no true "AutoFit"). Columns given
  an explicit width via \[xl_col_spec()\] are left untouched.

- autofilter:

  Add an autofilter (filter dropdowns). \`TRUE\` covers the whole used
  range (header plus data); an Excel range string such as \`"A1:D51"\`
  restricts it; \`FALSE\` (default) adds none.

- protect:

  Protect the worksheet: \`FALSE\` (default) leaves it unprotected,
  \`TRUE\` applies the standard protection, and a string sets a
  password. A named list gives fine-grained control, e.g.
  \`list(password = "secret", format_cells = TRUE)\`; an editing option
  set to \`TRUE\` \*allows\* that action on the protected sheet.
  Available option names: \`format_cells\`, \`format_columns\`,
  \`format_rows\`, \`insert_columns\`, \`insert_rows\`,
  \`insert_hyperlinks\`, \`delete_columns\`, \`delete_rows\`, \`sort\`,
  \`autofilter\`, \`pivot_tables\`, \`scenarios\`, \`objects\`,
  \`no_select_locked_cells\`, \`no_select_unlocked_cells\`. Cell locking
  via \[xl_protection()\] only has an effect on a protected sheet.

- comment_author:

  Default author for this sheet's cell comments (a per-comment
  \`author\` overrides it).

- show_comments:

  If \`TRUE\`, all comments on the sheet are initially shown (individual
  comments can still be forced via \`xl_comment(visible=)\`).

- page:

  An \[xl_page_setup()\] describing how the sheet prints (orientation,
  paper size, margins, scaling, header and footer). Affects printing
  only, never the cell data.

- view:

  An \[xl_sheet_view()\] describing the sheet's tab state and opening
  view (active/selected/hidden tab, selection, scroll position, zero
  display, direction, split panes).

- merge:

  One \[xl_merge()\], or a list of them, merging rectangles of cells
  into single cells. Merges are applied after the sheet's rows are
  written, so a merge over cells the data frame filled keeps only the
  merged text — as merging in Excel does. Any merge turns off the
  memory-efficient row-streaming mode, since it writes back over rows
  already emitted.

- validation:

  One \[xl_validation()\], or a list of them, restricting what may be
  typed into a range — a dropdown, a numeric or date bound, a text
  length limit or a custom formula.

- conditional:

  One conditional format (\[xl_cond_cell()\], \[xl_cond_scale()\],
  \[xl_cond_bar()\], \[xl_cond_icons()\]), or a list of them, formatting
  cells according to their contents.

- filter:

  One \[xl_filter()\], or a list of them, setting autofilter criteria.
  Each also hides the rows it excludes, because Excel does not apply a
  filter when a file is opened — criteria on their own produce a sheet
  that looks filtered but shows every row. Implies \`autofilter = TRUE\`
  over the used range when \`autofilter\` is not set separately.

- outline:

  An \[xl_outline()\] controlling how the grouping symbols created by
  \`level\` in \[xl_col_spec()\] / \[xl_row_spec()\] are drawn. It
  changes their display only, never which rows are grouped.

- ignore_errors:

  A named list turning off the green error triangle Excel shows in cells
  it believes are wrong. Each name is an error type and each value a
  range, e.g. \`list(number_stored_as_text = "A2:A99")\`. Types:
  \`number_stored_as_text\`, \`eval_error\`, \`formula_differs\`,
  \`formula_range\`, \`formula_unlocked\`, \`empty_cell_reference\`,
  \`list_data_validation\`, \`calculated_column\`,
  \`two_digit_text_year\`.

- table:

  One \[xl_table()\], or a list of them, turning a range into an Excel
  table — a named, styled block with banded rows, a filter dropdown and
  an optional total row. Any table turns off the memory-efficient
  row-streaming mode, which libxlsxwriter refuses to combine with
  tables.

- image:

  One \[xl_image()\], or a list of them, placing images on the sheet —
  floating over the cells, or inside a cell with \`embed = TRUE\`.

- background_image:

  An image tiled behind the sheet's cells, in any shape \[xl_image()\]
  accepts. It is a screen backdrop only — Excel never prints it.

- chart:

  One \[xl_chart()\], or a list of them, placed on the sheet and
  anchored to a cell. A chart's series may plot data from any sheet in
  the workbook, not only this one.

## Value

An \`xl_sheet\` object.

## See also

\[xl_col_spec\], \[xl_row_spec\], \[write_xlsx\]

Other worksheet layout:
[`xl_colrow_spec`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md),
[`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md),
[`xl_page_setup()`](https://docs.ropensci.org/writexl/reference/xl_page_setup.md),
[`xl_sheet_view()`](https://docs.ropensci.org/writexl/reference/xl_sheet_view.md)

## Examples

``` r
df <- data.frame(name = c("a", "b"), revenue = c(1000.5, 2000.25))
sheet <- xl_sheet(
  df,
  cols   = xl_col_spec("revenue", width = 14, format = xl_num_format("#,##0.00")),
  freeze = "A2",
  tab_color = "steelblue"
)
tmp <- write_xlsx(list(Data = sheet))
```
