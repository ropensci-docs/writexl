# One run of a rich (multi-format) string

\`xl_rich_run()\` is one fragment of an \[xl_rich_string()\]: a piece of
text plus the font it is drawn in.

## Usage

``` r
xl_rich_run(value, format = NULL)
```

## Arguments

- value:

  A single non-\`NA\`, non-empty string: the run's text.

- format:

  An optional \[xl_format\]. Only its \*\*font\*\* properties apply (see
  \[xl_font()\]); a run has no fill, border, alignment or number format,
  and supplying one warns. \`NULL\` draws the run in the cell's own
  font.

## Value

An \`xl_rich_run\` object.

## See also

\[xl_rich_string\], \[xl_format\]

Other cell content:
[`is_xl_comment()`](https://docs.ropensci.org/writexl/reference/is_xl_comment.md),
[`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md),
[`xl_comment()`](https://docs.ropensci.org/writexl/reference/xl_comment.md),
[`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md),
[`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)

## Examples

``` r
xl_rich_run("bold", xl_font(bold = TRUE))
#> <xl_rich_run: "bold" (formatted)>
xl_rich_run("plain")
#> <xl_rich_run: "plain">
```
