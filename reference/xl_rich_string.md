# A cell whose text has several formats

\`xl_rich_string()\` builds the value of a single cell out of
differently formatted runs, so that one cell can read "This is
\*\*bold\*\* text". Pass it as the \`value\` of \[xl_cell_general()\].

Excel requires at least two runs: a string with one format is an
ordinary character value, so pass it as one.

\`as.character()\` returns the cell's text with the per-run fonts
dropped.

## Usage

``` r
xl_rich_string(...)

is_xl_rich_string(x)

# S3 method for class 'xl_rich_string'
as.character(x, ...)
```

## Arguments

- ...:

  Runs, in order. A bare string is taken as an unformatted run; an
  \[xl_rich_run()\] carries its own font. Lists of either are flattened,
  so runs can be assembled programmatically.

- x:

  An object to test.

## Value

An \`xl_rich_string\` object: a list of runs.

## See also

\[xl_rich_run\], \[xl_cell_general\], \[xl_font\]

Other cell content:
[`is_xl_comment()`](https://docs.ropensci.org/writexl/reference/is_xl_comment.md),
[`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md),
[`xl_comment()`](https://docs.ropensci.org/writexl/reference/xl_comment.md),
[`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md),
[`xl_rich_run()`](https://docs.ropensci.org/writexl/reference/xl_rich_run.md)

## Examples

``` r
xl_rich_string("This is ", xl_rich_run("bold", xl_font(bold = TRUE)), " text")
#> <xl_rich_string: 3 runs>
#>   "This is "
#>   "bold"  <formatted>
#>   " text"

# in a cell, with a cell-wide format alongside the per-run fonts
xl_cell_general(
  value  = xl_rich_string("2 H", xl_rich_run("2", xl_font(script = "sub")), "O"),
  format = xl_align(horizontal = "center")
)
#> [xl_cell_general: 1 cell]
#>   [1] value=2 H2O, format=<set>
```
