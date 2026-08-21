# Create a cell comment

\`xl_comment()\` builds a comment (note) that can be attached to a cell
via \[xl_cell_general()\]'s \`comment\` argument. The simplest form is
just text (\`xl_cell_general(value = x, comment = "see note")\`);
\`xl_comment()\` adds options such as the author, initial visibility,
box size and position, and styling.

Excel comment boxes support only a \*\*background color\*\* and a
\*\*font name/size/family\*\*. These are supplied by reusing the
formatting engine via the \`format\` argument (e.g. \`xl_font(name =
"Arial", size = 10) + xl_fill(background = "lightyellow")\`); any other
format property (bold, borders, number formats, ...) is not supported by
comments and triggers a warning.

## Usage

``` r
xl_comment(
  value,
  format = NULL,
  author = NA,
  visible = NA,
  width_pixels = NA,
  height_pixels = NA,
  x_scale = NA,
  y_scale = NA,
  start_row = NA,
  start_col = NA,
  x_offset = NA,
  y_offset = NA
)
```

## Arguments

- value:

  A single string: the comment's text. Anything with an
  \[as.character()\] method is accepted, so a cell built for a sheet can
  be reused here.

- format:

  An optional \[xl_format\]; only its fill background color and font
  name/size/family are used (see \[xl_fill()\], \[xl_font()\]). Other
  properties are unsupported and warned about.

- author:

  Comment author (shown in Excel's status bar). Defaults to the
  sheet/workbook \`comment_author\` when unset (see \[xl_sheet()\],
  \[xl_properties()\]).

- visible:

  Initial visibility: \`NA\` follows the sheet default (comments are
  hidden unless \`show_comments\` is set), \`TRUE\` shows this comment,
  \`FALSE\` hides it.

- width_pixels, height_pixels:

  Comment box size in pixels (defaults 128 x 74).

- x_scale, y_scale:

  Box scale factors.

- start_row, start_col:

  Zero-based anchor cell of the box (by default a comment sits one row
  up and one column right of its cell).

- x_offset, y_offset:

  Pixel offset of the box from its anchor.

## Value

An \`xl_comment\` object.

## See also

\[xl_cell_general\], \[xl_format\]

Other cell content:
[`is_xl_comment()`](https://docs.ropensci.org/writexl/reference/is_xl_comment.md),
[`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md),
[`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md),
[`xl_rich_run()`](https://docs.ropensci.org/writexl/reference/xl_rich_run.md),
[`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)

## Examples

``` r
# plain text
xl_comment("Double-check this figure")
#> <xl_comment>
#>   value: Double-check this figure 

# with author and styling reused from the format engine
xl_comment("Estimate", author = "Finance",
           format = xl_font(name = "Arial", size = 10) +
                    xl_fill(background = "lightyellow"))
#> <xl_comment>
#>   value: Estimate 
#>   author: Finance
#> <xl_format>
#>   font: name=Arial, size=10
#>   fill: background=16777184, pattern=solid
```
