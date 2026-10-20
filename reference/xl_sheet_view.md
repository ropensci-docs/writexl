# How a worksheet appears when it opens

\`xl_sheet_view()\` collects a worksheet's tab state and opening view:
which tab is active, selected or hidden, where the sheet is scrolled and
selected, and a few display options. Pass it as \`xl_sheet(view = )\`.

None of these affect the cell data.

## Usage

``` r
xl_sheet_view(
  active = NA,
  selected = NA,
  visible = NA,
  first_tab = NA,
  selection = NULL,
  top_left = NULL,
  hide_zero = NA,
  right_to_left = NA,
  split = NULL
)
```

## Arguments

- active:

  Logical; make this the tab Excel opens on. At most one sheet in a
  workbook may be active.

- selected:

  Logical; include this tab in the selected group. The active sheet is
  always selected.

- visible:

  Logical; \`FALSE\` hides the sheet's tab. A hidden sheet cannot be
  active or selected, the first sheet cannot be hidden unless another is
  made active, and at least one sheet must stay visible or Excel will
  not open the file. All four rules are checked before writing.

- first_tab:

  Logical; make this the leftmost visible tab in the tab strip.
  Independent of which sheet is active.

- selection:

  The cell or range selected when the sheet opens, as an Excel reference
  (\`"B2"\`, \`"B2:D10"\`) or a \`list(rows = , cols = )\` spec.

  Excel also uses the order of a selection's corners to mark which cell
  in it is active; writexl does not expose that, because ranges are
  normalised by the shared range parser, which rejects an inverted
  range.

- top_left:

  The cell scrolled to the top-left of the window when the sheet opens,
  as an Excel reference such as \`"A5"\`.

- hide_zero:

  Logical; display zero values as blank cells.

- right_to_left:

  Logical; order the columns right to left, for a sheet in a
  right-to-left language.

- split:

  Split the sheet into scrollable panes with a visible, movable divider,
  given as the cell reference the split sits above and to the left of —
  \`"B3"\` splits above row 3 and left of column B. Mutually exclusive
  with \`xl_sheet(freeze = )\`, which does the same thing without the
  divider.

  libxlsxwriter positions a split by distance, in row-height and
  column-width units, not by row and column number. writexl converts the
  cell reference using the sheet's actual row heights and column widths,
  so the split lands where you asked even after resizing. Pass
  \`list(vertical = , horizontal = )\` to give those units directly.

  Note that libxlsxwriter derives the pane's scroll anchor back from
  that distance assuming default row heights, so on a sheet with resized
  rows or columns the divider is placed correctly but the anchor cell
  may be a row or two out.

## Value

An \`xl_sheet_view\` object.

## See also

\[xl_sheet\], \[xl_page_setup\]

Other worksheet layout:
[`xl_colrow_spec`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md),
[`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md),
[`xl_page_setup()`](https://docs.ropensci.org/writexl/reference/xl_page_setup.md),
[`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md)

## Examples

``` r
xl_sheet_view(active = TRUE, selection = "B2")
#> <xl_sheet_view: 2 settings>
#>   active: TRUE
#>   selection: B2
xl_sheet_view(visible = FALSE)
#> <xl_sheet_view: 1 setting>
#>   visible: FALSE

df <- data.frame(x = 1:3)
tmp <- write_xlsx(list(
  Summary = xl_sheet(df, view = xl_sheet_view(active = TRUE)),
  Working = xl_sheet(df, view = xl_sheet_view(visible = FALSE))
))
```
