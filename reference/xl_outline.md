# Control how outline (grouping) symbols are drawn

Grouping itself comes from \`level\` in \[xl_col_spec()\] /
\[xl_row_spec()\]. \`xl_outline()\` only changes how the controls are
\*displayed\*, which is rarely needed — the defaults match Excel's own.

## Usage

``` r
xl_outline(
  visible = TRUE,
  symbols_below = TRUE,
  symbols_right = TRUE,
  auto_style = FALSE
)
```

## Arguments

- visible:

  Show the outline symbols at all. \`FALSE\` keeps the grouping (and so
  the collapsing) but hides the +/- controls.

- symbols_below:

  Put the summary row \*below\* the detail rows, which is Excel's
  default. \`FALSE\` puts it above.

- symbols_right:

  Put the summary column to the \*right\* of the detail columns, Excel's
  default. \`FALSE\` puts it to the left.

- auto_style:

  Apply Excel's automatic outline styling to the grouped rows and
  columns.

## Value

An \`xl_outline\` object, for \[xl_sheet()\]'s \`outline\` argument.

## See also

\[xl_sheet\], \[xl_colrow_spec\]

Other worksheet layout:
[`xl_colrow_spec`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md),
[`xl_page_setup()`](https://docs.ropensci.org/writexl/reference/xl_page_setup.md),
[`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md),
[`xl_sheet_view()`](https://docs.ropensci.org/writexl/reference/xl_sheet_view.md)

## Examples

``` r
xl_outline(symbols_below = FALSE)
#> <xl_outline: visible=TRUE below=FALSE right=TRUE auto_style=FALSE>
xl_outline(visible = FALSE)
#> <xl_outline: visible=FALSE below=TRUE right=TRUE auto_style=FALSE>
```
