# Cell formatting groups

These constructors build \[xl_format\] objects, each populating one
group of Excel cell-formatting properties. Every property defaults to
\`NA\`, meaning "leave unset"; unset properties are simply not written.
Enum-like arguments take lowercase strings and are validated against a
fixed set of choices.

Each constructor returns a full \`xl_format\`, so a single group can be
used on its own (\`xl_cell_general(1, format = xl_font(bold = TRUE))\`),
and groups can be combined with \`+\` (see \[xl_format\]).

## Usage

``` r
xl_font(
  bold = NA,
  italic = NA,
  color = NA,
  size = NA,
  name = NA,
  underline = NA,
  strikeout = NA,
  script = NA,
  family = NA,
  charset = NA,
  outline = NA,
  shadow = NA,
  condense = NA,
  extend = NA,
  scheme = NA,
  theme = NA,
  color_indexed = NA,
  font_only = NA
)

xl_fill(background = NA, foreground = NA, pattern = NA, transparency = NA)

xl_border(
  all = NA,
  left = NA,
  right = NA,
  top = NA,
  bottom = NA,
  color = NA,
  left_color = NA,
  right_color = NA,
  top_color = NA,
  bottom_color = NA,
  diagonal = NA,
  diagonal_style = NA,
  diagonal_color = NA,
  transparency = NA
)

xl_align(
  horizontal = NA,
  vertical = NA,
  wrap = NA,
  rotation = NA,
  indent = NA,
  shrink = NA,
  reading_order = NA
)

xl_num_format(format = NA, index = NA)

xl_protection(locked = NA, hidden = NA)
```

## Arguments

- bold, italic, strikeout, outline, shadow, condense, extend, font_only:

  Logical font flags.

- color, background, foreground, left_color, right_color, top_color,
  bottom_color, diagonal_color:

  A color: an R color name, a hex string, or an integer (see
  \[xl_color\]).

- size:

  Font size in points (1–409).

- name:

  Font name, e.g. \`"Calibri"\`.

- underline:

  One of \`"none"\`, \`"single"\`, \`"double"\`,
  \`"single-accounting"\`, \`"double-accounting"\`.

- script:

  One of \`"super"\`, \`"sub"\`.

- family, charset, theme, color_indexed:

  Advanced integer font properties (rarely needed).

- scheme:

  Font scheme string (advanced).

- pattern:

  Fill pattern, e.g. \`"solid"\`, \`"light-gray"\` (18 choices). When
  \`background\` is supplied and \`pattern\` is unset, a \`"solid"\`
  pattern is assumed.

- transparency:

  Percentage transparency, 0–100. \*\*Charts only\*\*: Excel has no
  transparency for a cell's fill or border, so this is ignored
  everywhere except a chart's line and fill (see \[xl_chart()\]).

- all:

  Border style applied to all four sides at once (one of \`"none"\`,
  \`"thin"\`, \`"medium"\`, \`"dashed"\`, \`"dotted"\`, \`"thick"\`,
  \`"double"\`, \`"hair"\`, \`"medium-dashed"\`, \`"dash-dot"\`,
  \`"medium-dash-dot"\`, \`"dash-dot-dot"\`, \`"medium-dash-dot-dot"\`,
  \`"slant-dash-dot"\`).

- left, right, top, bottom:

  Per-side border styles (override \`all\`).

- diagonal:

  Diagonal border direction: \`"up"\`, \`"down"\`, \`"up-down"\`.

- diagonal_style:

  Diagonal border style (same choices as \`all\`).

- horizontal:

  Horizontal alignment: \`"left"\`, \`"center"\`, \`"right"\`,
  \`"fill"\`, \`"justify"\`, \`"center-across"\`, \`"distributed"\`.

- vertical:

  Vertical alignment: \`"top"\`, \`"bottom"\`, \`"center"\`,
  \`"justify"\`, \`"distributed"\`.

- wrap:

  Logical; wrap text in the cell.

- rotation:

  Text rotation in degrees (-90..90, or 270).

- indent:

  Integer indentation level.

- shrink:

  Logical; shrink text to fit.

- reading_order:

  One of \`"default"\`, \`"ltr"\`, \`"rtl"\`.

- format:

  A number-format string, e.g. \`"#,##0.00"\`, \`"0 \`"yyyy-mm-dd"\`.

- index:

  An Excel built-in number-format index (alternative to \`format\`).

- locked:

  Logical; whether the cell is locked (Excel's default is \`TRUE\`).
  Only takes effect when the worksheet is protected. \`FALSE\` unlocks
  the cell.

- hidden:

  Logical; hide the cell's formula.

## Value

An \[xl_format\] object.

## See also

\[xl_format\], \[xl_color\]

Other cell formatting:
[`is_xl_format()`](https://docs.ropensci.org/writexl/reference/is_xl_format.md),
[`xl_color()`](https://docs.ropensci.org/writexl/reference/xl_color.md),
[`xl_format()`](https://docs.ropensci.org/writexl/reference/xl_format.md)

## Examples

``` r
xl_font(bold = TRUE, color = "navy", size = 12)
#> <xl_format>
#>   font: size=12, color=128, bold=TRUE
xl_fill(background = "#FFF2CC")
#> <xl_format>
#>   fill: background=16773836, pattern=solid
xl_border(all = "thin", color = "gray")
#> <xl_format>
#>   border: left=thin, right=thin, top=thin, bottom=thin, left_color=12500670, right_color=12500670, top_color=12500670, bottom_color=12500670
xl_align(horizontal = "center", vertical = "top", wrap = TRUE)
#> <xl_format>
#>   align: horizontal=center, vertical=top, wrap=TRUE
xl_num_format("#,##0.00")
#> <xl_format>
#>   num_format: format=#,##0.00
xl_protection(locked = FALSE)
#> <xl_format>
#>   protection: locked=FALSE
```
