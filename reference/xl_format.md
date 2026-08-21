# Combine cell-formatting groups into a single format

\`xl_format()\` merges any number of \[xl_format\] objects (typically
the single-group objects returned by \[xl_font\], \[xl_fill\],
\[xl_border\], \[xl_align\], \[xl_num_format\] and \[xl_protection\])
into one combined format. The \`+\` operator does the same for two
formats.

Merging is right-biased and works property-by-property: where two
formats set the \*same\* property the later one wins, but properties set
by only one side are all preserved. So partial groups accumulate rather
than overwrite.

## Usage

``` r
xl_format(..., quote_prefix = NA, hyperlink = NA)

# S3 method for class 'xl_format'
e1 + e2
```

## Arguments

- ...:

  \[xl_format\] objects (and/or \`NULL\`s, which are ignored). May also
  include the scalar flags \`quote_prefix\` and \`hyperlink\`.

- quote_prefix:

  Logical; treat the cell contents as literal text (as if prefixed with
  a single quote in Excel).

- hyperlink:

  Logical; apply the internal hyperlink style flag (advanced).

- e1, e2:

  \[xl_format\] objects to combine.

## Value

A combined \[xl_format\] object.

## See also

\[xl_font\], \[xl_fill\], \[xl_border\], \[xl_align\],
\[xl_num_format\], \[xl_protection\], \[xl_color\]

Other cell formatting:
[`is_xl_format()`](https://docs.ropensci.org/writexl/reference/is_xl_format.md),
[`xl_color()`](https://docs.ropensci.org/writexl/reference/xl_color.md),
[`xl_format_groups`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)

## Examples

``` r
xl_format(xl_font(bold = TRUE), xl_border(bottom = "thin"),
          xl_num_format("#,##0.00"))
#> <xl_format>
#>   font: bold=TRUE
#>   border: bottom=thin
#>   num_format: format=#,##0.00

# equivalent, using +
xl_font(bold = TRUE) + xl_border(bottom = "thin") + xl_num_format("#,##0.00")
#> <xl_format>
#>   font: bold=TRUE
#>   border: bottom=thin
#>   num_format: format=#,##0.00
```
