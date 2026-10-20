# Getting started with writexl

writexl writes data frames to xlsx. It needs no Java and no Excel, and
for the common case it needs nothing from you either.

## One data frame

``` r

path <- write_xlsx(iris, tempfile(fileext = ".xlsx"))
```

[`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
returns the path it wrote, so it composes with anything that takes a
file name.

## Several sheets

A named list becomes one sheet per element, and the names become the
tabs:

``` r

path <- write_xlsx(list(Flowers = iris, Cars = mtcars[1:5, 1:4]),
                   tempfile(fileext = ".xlsx"))
```

Sheet names are repaired rather than rejected: Excel forbids
`[ ] : * ? / \`, limits a name to 31 characters, and refuses duplicates.
writexl fixes each of those and warns, naming the original and the
replacement, because a sheet name is often taken from data and losing
the whole export over one stray `/` would be unkind.

## What is written

Column types map to Excel’s own:

| R                    | Excel                        |
|----------------------|------------------------------|
| `character`          | text                         |
| `numeric`, `integer` | number                       |
| `logical`            | TRUE/FALSE                   |
| `Date`, `POSIXct`    | a formatted date or datetime |
| `factor`             | its labels, as text          |
| `difftime`           | a number of seconds          |

`NA` becomes an empty cell. A column of a type xlsx has no
representation for — `complex`, `raw`, a plain list column — is an error
rather than a silent approximation.

`na` writes something else in place of an empty cell, for `NaN` as well
as `NA`. It keeps its own type, so a number stays a number:

``` r

tmp <- write_xlsx(data.frame(x = c(1.5, NA)), na = "not measured")
```

Set it for the whole workbook with `xl_properties(na = )`, for one
column with `xl_col_spec(na = )`, or for one cell with
`xl_cell_general(na = )`; the innermost one that is set wins.
Substituting a string into a numeric column makes that column mixed, so
reading it back gives character.

Excel has no concept of a time zone, so `POSIXct` needs a decision.
writexl makes it once for the whole workbook: if every value shares one
zone the local wall-clock reading is written, and if they differ
everything is converted to UTC and you are warned. Either way nothing is
mislabelled.

The header row is written by default and styled bold;
`col_names = FALSE` and `format_headers = FALSE` turn each off.

## Everything else

The rest of the package is optional. Nothing below is needed to write a
workbook, and each has a vignette of its own:

- **[Formatting
  cells](https://docs.ropensci.org/writexl/articles/b-formatting.md)** —
  fonts, fills, borders, number formats and alignment, built from group
  constructors that combine with `+`, plus conditional formatting.

- **[Worksheets and
  workbooks](https://docs.ropensci.org/writexl/articles/c-worksheets-workbooks.md)**
  — column widths and row heights, frozen panes, tab colours, printing
  and page setup, and the document properties.

- **[Charts and
  images](https://docs.ropensci.org/writexl/articles/d-charts-images.md)**
  — all 22 chart types Excel offers, their axes, series parts and
  legends; chartsheets; and pictures placed on or in a sheet.

- **[Formulas, tables and the
  rest](https://docs.ropensci.org/writexl/articles/e-formulas-and-more.md)**
  — formulas and array formulas, hyperlinks, comments, rich strings,
  data validation, autofilters, worksheet tables and merged cells.

- **[Everything at
  once](https://docs.ropensci.org/writexl/articles/f-everything-at-once.md)**
  — one runnable script that exercises the whole package into a couple
  of workbooks, for reviewing what it can do without reading five
  vignettes first.

Two ideas run through all of them and are worth knowing early.

**A format is an object.**
[`xl_font()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md),
[`xl_fill()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
and the rest each return a complete `xl_format`, they combine with `+`,
and the same object styles a cell, a column, a chart series or a
conditional rule.

``` r

money <- xl_num_format("$#,##0.00") + xl_font(bold = TRUE)
```

**A range is written one of two ways.** Either as A1 text, or against
the data frame by column name — and the second is worth preferring,
because it moves with the column and accounts for the header row on its
own:

``` r

xl_sheet(iris, autofilter = "A1:E151")                   # A1 text
#> <xl_sheet: 150 rows x 5 cols>
xl_sheet(iris, filter = xl_filter("Species", "==", "setosa"))  # by column
#> <xl_sheet: 150 rows x 5 cols>
```

## Reading it back

writexl only writes. To read, use readxl:

``` r

readxl::read_xlsx(write_xlsx(head(iris, 3), tempfile(fileext = ".xlsx")))
#> # A tibble: 3 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa
```
