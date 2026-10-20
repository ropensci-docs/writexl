# Normalize a color to a libxlsxwriter RGB integer

Converts an R color name (e.g. \`"navy"\`), a hex string (\`"#FF0000"\`
or \`"FF0000"\`), or an integer in the range \`0x000000\`..\`0xFFFFFF\`
into the single \`0xRRGGBB\` integer that libxlsxwriter expects. Used
internally by every \`color\`/\`background\`/\`foreground\` argument of
the formatting constructors, and exported so it can be used directly.

## Usage

``` r
xl_color(x)
```

## Arguments

- x:

  A single color: an R color name, a hex string, or an integer. \`NA\`
  returns \`NA_integer\_\` (an unset color).

## Value

A single integer in \`0x000000\`..\`0xFFFFFF\`, or \`NA_integer\_\`.

## See also

Other cell formatting:
[`is_xl_format()`](https://docs.ropensci.org/writexl/reference/is_xl_format.md),
[`xl_format()`](https://docs.ropensci.org/writexl/reference/xl_format.md),
[`xl_format_groups`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)

## Examples

``` r
xl_color("red")
#> [1] 16711680
xl_color("#0000FF")
#> [1] 255
xl_color(255L)
#> [1] 255
```
