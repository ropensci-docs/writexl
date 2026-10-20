# Insert an image into a worksheet

\`xl_image()\` places an image on a sheet, either floating over the
cells and anchored to one of them (the default) or, with \`embed =
TRUE\`, inside a cell. Pass one or a list of them as \`xl_sheet(image =
)\`.

The image may be a file path or a raw vector, which is convenient when a
plot has just been written by a graphics device and never touched the
disk. PNG, JPEG, GIF and BMP are supported — the formats Excel reads —
and the format is detected from the file's own bytes rather than its
extension.

## Usage

``` r
xl_image(
  image,
  at = "A1",
  scale = 1,
  offset = NULL,
  position = "move_and_size",
  description = NULL,
  decorative = FALSE,
  url = NULL,
  tip = NULL,
  embed = FALSE,
  format = NULL
)
```

## Arguments

- image:

  The image, in any of four shapes: a path to a PNG, JPEG, GIF or BMP; a
  raw vector holding one of those encoded; a \`raster\` (or anything
  \[grDevices::as.raster()\] accepts, such as a colour matrix or an
  RGB/RGBA array); or a \`nativeRaster\`. The last two are what
  \[graphics::rasterImage()\] draws, so anything you can plot can be
  written.

- at:

  The cell the image is anchored to, such as \`"B2"\`, or a \`list(rows
  = , cols = )\` spec selecting a single cell.

- scale:

  Scale factor: one number for both axes, or \`c(x, y)\`.

- offset:

  Offset from the anchor cell's top-left corner in pixels, as \`c(x,
  y)\`.

- position:

  How the image behaves when rows and columns change size:
  \`"move_and_size"\` (the default), \`"move_dont_size"\`,
  \`"dont_move_dont_size"\`, \`"move_and_size_after"\`, or \`"default"\`
  for Excel's own default. Ignored when \`embed = TRUE\`.

- description:

  Alt text, for screen readers. Excel defaults it to the file name;
  \`""\` writes none.

- decorative:

  Mark the image as decorative, so screen readers skip it. Excel does
  not write a description for a decorative image.

- url:

  An optional hyperlink the image links to.

- tip:

  An optional mouseover tip for \`url\`.

- embed:

  Place the image inside the cell rather than floating above it.
  Requires a version of Excel that supports images in cells.

- format:

  An \[xl_format\] for the cell holding an embedded image. Only
  meaningful with \`embed = TRUE\`.

## Value

An \`xl_image\` object.

## Floating versus embedded

An inserted image floats above the grid: it has a position but occupies
no cell, and \`position\` decides whether it moves and resizes as rows
and columns change. An embedded image (\`embed = TRUE\`) lives \*in\* a
cell and sizes with it, which is the Excel 365 "place in cell"
behaviour. Excel versions without that feature show \`#VALUE!\` in place
of an embedded image, so it is worth choosing deliberately.

## Caveats inherited from Excel

An image's scaling can shift if it crosses a row whose height changed —
for a taller font or wrapped text — so set the height explicitly with
\[xl_row_spec()\] for rows an image spans. BMP is supported only for
backward compatibility and must be 24-bit true colour; prefer PNG. SVG
is refused, because Excel stores it converted to PNG anyway.

## See also

\[xl_sheet\]

Other images and charts:
[`xl_chart()`](https://docs.ropensci.org/writexl/reference/xl_chart.md),
[`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md),
[`xl_chart_error_bars()`](https://docs.ropensci.org/writexl/reference/xl_chart_error_bars.md),
[`xl_chart_labels()`](https://docs.ropensci.org/writexl/reference/xl_chart_labels.md),
[`xl_chart_legend()`](https://docs.ropensci.org/writexl/reference/xl_chart_legend.md),
[`xl_chart_marker()`](https://docs.ropensci.org/writexl/reference/xl_chart_marker.md),
[`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
[`xl_chart_table()`](https://docs.ropensci.org/writexl/reference/xl_chart_table.md),
[`xl_chart_trendline()`](https://docs.ropensci.org/writexl/reference/xl_chart_trendline.md),
[`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md)

## Examples

``` r
logo <- system.file("help", "figures", "logo.png", package = "writexl")
if (nzchar(logo)) {
  xl_image(logo, at = "C2", scale = 0.5)
  xl_image(logo, at = "C2", url = "https://example.com", tip = "Home")
}
```
