# Export to xlsx

Writes a data frame to an xlsx file. To create an xlsx with (multiple)
named sheets, simply set `x` to a named list of data frames.

## Usage

``` r
write_xlsx(
  x,
  path = tempfile(fileext = ".xlsx"),
  col_names = TRUE,
  format_headers = TRUE,
  na = NA,
  use_zip64 = FALSE,
  constant_memory = NA,
  constant_memory_threshold = 128 * 1024^2
)
```

## Arguments

- x:

  a data frame, an \[xl_sheet\], an \[xl_workbook\], or a (named) list
  of data frames / \`xl_sheet\`s that become the sheets in the xlsx

- path:

  a file name to write to

- col_names:

  write column names as the header row at the top of the sheet?

- format_headers:

  apply the workbook's header format to that header row? The default
  header format is bold and centered; change it with
  [`xl_properties`](https://docs.ropensci.org/writexl/reference/xl_properties.md)`(header_format = )`.

- na:

  what to write where a value has none. \`NA\` (the default) leaves the
  cell blank, as writexl has always done; anything else is written in
  its place, keeping its own type. Shorthand for
  [`xl_properties`](https://docs.ropensci.org/writexl/reference/xl_properties.md)`(na = )`,
  so give it there instead when \`x\` is already an \[xl_workbook\]. A
  column or a single cell can override it: see \[xl_col_spec()\] and
  \[xl_cell_general()\].

- use_zip64:

  use [zip64](https://en.wikipedia.org/wiki/Zip_(file_format)#ZIP64) to
  enable support for 4GB+ xlsx files. Not all platforms can read this.

- constant_memory:

  stream rows to disk instead of building the whole workbook in memory.
  \`NA\` (the default) decides per workbook: on for large data, off for
  small, and always off when a feature needs it off. \`TRUE\` forces it
  on for a workbook that would otherwise be judged too small; \`FALSE\`
  forces it off. Features that cannot be written while streaming —
  merged ranges, tables, embedded images and multi-cell array formulas —
  turn it off regardless, with a warning if \`TRUE\` was asked for,
  because the alternative is a file that opens cleanly and is missing
  cells.

- constant_memory_threshold:

  how much extra memory not streaming would have to cost, in bytes,
  before streaming is worth it. Default 128 MiB. The cost is
  \*estimated\* from the number of cells in the workbook, using a fixed
  per-cell figure calibrated against a range of data; the true cost
  varies with the data, and is lowest for text that repeats. Streaming
  saves memory but produces slightly larger files, so it is not used for
  workbooks small enough that the saving would not be noticed.

## Details

Supports strings, numbers, booleans and dates automatically. For cell
formatting (fonts, fills, borders, number formats, ...), worksheet
layout (column widths, frozen panes, ...), and workbook metadata, wrap
columns with
[`xl_cell_general`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md),
sheets with
[`xl_sheet`](https://docs.ropensci.org/writexl/reference/xl_sheet.md),
and the whole workbook with
[`xl_workbook`](https://docs.ropensci.org/writexl/reference/xl_workbook.md).
See the "Formatting and workbook properties" vignette and
[`xl_format`](https://docs.ropensci.org/writexl/reference/xl_format.md).

## See also

Other workbook settings:
[`xl_properties()`](https://docs.ropensci.org/writexl/reference/xl_properties.md),
[`xl_workbook()`](https://docs.ropensci.org/writexl/reference/xl_workbook.md)

## Examples

``` r
# Roundtrip example with single excel sheet named 'mysheet'
tmp <- write_xlsx(list(mysheet = iris))
readxl::read_xlsx(tmp)
#> # A tibble: 150 × 5
#>    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>           <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#>  1          5.1         3.5          1.4         0.2 setosa 
#>  2          4.9         3            1.4         0.2 setosa 
#>  3          4.7         3.2          1.3         0.2 setosa 
#>  4          4.6         3.1          1.5         0.2 setosa 
#>  5          5           3.6          1.4         0.2 setosa 
#>  6          5.4         3.9          1.7         0.4 setosa 
#>  7          4.6         3.4          1.4         0.3 setosa 
#>  8          5           3.4          1.5         0.2 setosa 
#>  9          4.4         2.9          1.4         0.2 setosa 
#> 10          4.9         3.1          1.5         0.1 setosa 
#> # ℹ 140 more rows
```
