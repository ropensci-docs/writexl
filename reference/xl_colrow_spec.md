# Column and row specifications for a worksheet

\`xl_col_spec()\` and \`xl_row_spec()\` describe formatting and geometry
for a set of columns or rows within a sheet built by \[xl_sheet()\].
They are \*subclasses\* of \[xl_format\]: they carry the usual
formatting groups (so they combine with \`+\` and the group
constructors) plus a target (which columns/rows) and geometry
(width/height, hidden, outline level).

## Usage

``` r
xl_col_spec(
  cols,
  width = NA,
  hidden = NA,
  level = NA,
  format = NULL,
  width_pixels = NA,
  collapsed = NA,
  na = NA
)

xl_row_spec(
  rows,
  height = NA,
  hidden = NA,
  level = NA,
  format = NULL,
  height_pixels = NA,
  collapsed = NA
)
```

## Arguments

- cols:

  Columns to target: a character vector of column names or a numeric
  vector of 1-based positions.

- width:

  Column width (in Excel character units).

- hidden:

  Logical; hide the column/row.

- level:

  Integer outline (grouping) level, 0–7.

- format:

  An optional \[xl_format\] applied to the column/row as its default
  cell format. Combine groups with \`+\` (e.g. \`xl_font(bold = TRUE) +
  xl_fill(background = "yellow")\`).

- width_pixels, height_pixels:

  The same geometry given in pixels instead. Give one or the other, not
  both. Excel stores character units and points, so the pixel value is
  converted on the way in — read back, a width set as 100 pixels is
  13.57 character units.

- collapsed:

  Logical; draw this column/row as the collapsed summary of the group
  beside it. Excel does not derive this — the rows or columns of the
  group itself need \`hidden = TRUE\` as well, exactly as clicking the
  grouping symbol would leave them.

- na:

  What to write in this column where a value has none, overriding the
  workbook's \[xl_properties()\]\`(na = )\`. \`NA\` (the default)
  inherits it. Columns are where this usually belongs: a substitute that
  suits a numeric column rarely suits a date one.

- rows:

  Rows to target: a numeric vector of 1-based data-row indices (row 1 is
  the first data row, ignoring the header).

- height:

  Row height (in points).

## Value

An \`xl_col_spec\` / \`xl_row_spec\` object (also an \[xl_format\]).

## See also

\[xl_sheet\], \[xl_format\]

Other worksheet layout:
[`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md),
[`xl_page_setup()`](https://docs.ropensci.org/writexl/reference/xl_page_setup.md),
[`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md),
[`xl_sheet_view()`](https://docs.ropensci.org/writexl/reference/xl_sheet_view.md)

## Examples

``` r
xl_col_spec("revenue", width = 14, format = xl_num_format("#,##0.00"))
#> <xl_col_spec>
#>   target: kind=col, index=revenue 
#>   geometry: width=14 
#>   num_format: format=#,##0.00
xl_col_spec(c(1, 2), width = 10) + xl_font(bold = TRUE)
#> <xl_col_spec>
#>   target: kind=col, index=1,2 
#>   geometry: width=10 
#>   font: bold=TRUE
xl_col_spec("logo", width_pixels = 100)
#> <xl_col_spec>
#>   target: kind=col, index=logo 
#>   geometry: width=13.57143 
xl_row_spec(1, height = 24, format = xl_font(bold = TRUE))
#> <xl_row_spec>
#>   target: kind=row, index=1 
#>   geometry: height=24 
#>   font: bold=TRUE
xl_row_spec(1, height_pixels = 40)
#> <xl_row_spec>
#>   target: kind=row, index=1 
#>   geometry: height=30 
```
