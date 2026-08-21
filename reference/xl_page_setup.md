# How a worksheet prints

\`xl_page_setup()\` collects Excel's page-layout settings for one
worksheet: orientation, paper size, margins, scaling, centring, the
print options, and the header and footer. Pass it as \`xl_sheet(page =
)\`.

None of these affect the cell data — they change only how the sheet
prints and how it looks in Excel's page-break preview.

## Usage

``` r
xl_page_setup(
  orientation = NA,
  paper = NA,
  margins = NULL,
  scale = NA,
  fit_to = NULL,
  center_horizontally = NA,
  center_vertically = NA,
  header = NA,
  footer = NA,
  header_margin = NA,
  footer_margin = NA,
  header_image = NULL,
  footer_image = NULL,
  page_view = NA,
  first_page = NA,
  across = NA,
  black_and_white = NA,
  row_col_headers = NA,
  print_area = NULL,
  repeat_rows = NA,
  repeat_cols = NA,
  h_breaks = NULL,
  v_breaks = NULL
)
```

## Arguments

- orientation:

  \`"portrait"\` or \`"landscape"\`.

- paper:

  Paper size: a name (\`"A4"\`, \`"letter"\`, \`"legal"\`,
  \`"tabloid"\`, \`"ledger"\`, \`"statement"\`, \`"executive"\`,
  \`"A3"\`, \`"A5"\`, \`"B4"\`, \`"B5"\`, \`"folio"\`, \`"quarto"\`,
  \`"default"\`), or an Excel paper-type integer for the envelope and
  specialist sizes that have no name here.

- margins:

  Page margins in inches: a single number for all four sides, four
  numbers in the order left, right, top, bottom, or a named vector using
  any of \`left\`, \`right\`, \`top\`, \`bottom\`.

- scale:

  Print scaling as a percentage (10–400). Ignored by Excel when
  \`fit_to\` is set.

- fit_to:

  Fit the printout to \`c(width, height)\` pages. A \`0\` means "as many
  pages as needed in that direction", so \`c(width = 1, height = 0)\` is
  Excel's "fit all columns on one page".

- center_horizontally, center_vertically:

  Logical; centre the printed output on the page.

- header, footer:

  Header and footer text, at most 255 characters, using Excel's own
  codes: \`&L\`, \`&C\`, \`&R\` start the left, centre and right
  sections, \`&P\` is the page number, \`&N\` the page count, \`&D\` the
  date, \`&A\` the sheet name, and \`&&\` a literal ampersand. For
  example \`"&LQ1 report&RPage &P of &N"\`. Image placeholders (\`&G\` /
  \`&\[Picture\]\`) are not supported yet and are rejected.

- header_margin, footer_margin:

  Header/footer margin in inches (Excel's default is 0.3). Must be
  greater than 0.

- header_image, footer_image:

  Images to place in the header or footer, named by position:
  \`list(left = , center = , right = )\`. Each may be a file path, a raw
  vector, or an in-memory image, exactly as \[xl_image()\] accepts. Each
  image needs a matching \`&G\` placeholder in the corresponding section
  of \`header\`/\`footer\` — \`"&L&G"\` puts one on the left — and the
  counts must agree.

- page_view:

  Logical; open the sheet in Excel's page-layout view rather than normal
  view.

- first_page:

  The page number to start numbering from.

- across:

  Logical; print pages left-to-right before top-to-bottom (Excel's
  "over, then down").

- black_and_white:

  Logical; print without colour.

- row_col_headers:

  Logical; print the row numbers and column letters.

- print_area:

  The range to print: an Excel range string such as \`"A1:F50"\`, or a
  \`list(rows = , cols = )\` spec naming data rows and columns, as
  elsewhere in writexl.

- repeat_rows, repeat_cols:

  Rows/columns to repeat at the top or left of every printed page.
  Either a count (\`repeat_rows = 1\` repeats the first sheet row, which
  is the header when \`col_names = TRUE\`) or a range string (\`"1:2"\`,
  \`"A:B"\`).

  Note these count \*sheet\* rows from 1 with the header included,
  unlike \[xl_row_spec()\], which indexes data rows — repeating the
  header row is the usual reason to use this, and data-row numbering
  could not name it.

- h_breaks, v_breaks:

  Manual page breaks: 1-based sheet positions at which a new page
  starts, so \`h_breaks = 21\` breaks between rows 20 and 21.
  \`v_breaks\` also accepts column letters. Positions must be 2 or
  greater, and at most 1023 breaks are allowed. Excel ignores manual
  breaks when \`fit_to\` is set, which warns.

## Value

An \`xl_page_setup\` object.

## See also

\[xl_sheet\], \[write_xlsx\]

Other worksheet layout:
[`xl_colrow_spec`](https://docs.ropensci.org/writexl/reference/xl_colrow_spec.md),
[`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md),
[`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md),
[`xl_sheet_view()`](https://docs.ropensci.org/writexl/reference/xl_sheet_view.md)

## Examples

``` r
xl_page_setup(orientation = "landscape", paper = "A4",
              fit_to = c(width = 1, height = 0))
#> <xl_page_setup: 3 settings>
#>   orientation: landscape
#>   paper: 9
#>   fit_to: 1, 0

# margins in inches, and a header with page numbers
xl_page_setup(margins = c(left = 1, right = 1),
              header = "&LQuarterly report&RPage &P of &N")
#> <xl_page_setup: 2 settings>
#>   margins: 1, 1
#>   header: &LQuarterly report&RPage &P of &N

df <- data.frame(x = 1:3)
tmp <- write_xlsx(list(Data = xl_sheet(df, page = xl_page_setup(
  orientation = "landscape", header = "&CDraft"
))))
```
