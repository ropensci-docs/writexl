# Changelog

## writexl 2.0.1

CRAN release: 2026-08-21

A compiled-code cleanup requested by CRAN; nothing changes at the R
level.

- The bundled libxlsxwriter assigned the result of
  `strstr()`/`strpbrk()` on a `const` string to a non-`const` pointer in
  four places. With GCC 16 and glibc 2.43, where the C23 `<string.h>`
  search functions preserve `const`, those assignments drew “discards
  ‘const’ qualifier” warnings, and the CRAN checks on the r-devel Fedora
  flavors flag them as significant. The pointers were only ever read,
  and are now `const` (or gone).

## writexl 2.0.0

CRAN release: 2026-08-05

writexl is now maintained by Bill Denney; Jeroen Ooms remains an author.

### Breaking changes

The version number is 2.0.0 for these, each of which can change what an
existing script writes. Everything else in this release is additive.

- `POSIXct` columns are no longer silently converted to UTC. When every
  datetime in the workbook shares one time zone, the zone is dropped and
  local wall-clock time is written; when they differ, all are converted
  to UTC with a warning. Code that relied on always getting the UTC
  instant will see shifted values.

- `Date` values before 1900-03-01 were written one day too late, and now
  agree with `POSIXct`. Files written earlier that contain such dates
  disagree with files written now.

- Columns of a type writexl cannot represent (`complex`, `raw`, a bare
  list column) are an error naming the column, where before they warned
  and wrote empty cells. A script that ignored the warning now stops.

- Sheet names are repaired differently: truncated to a genuine 31
  characters rather than 29, with characters Excel forbids replaced and
  the resulting duplicates resolved. A workbook with long or awkward
  sheet names may end up with different tab names than before – and, in
  the `"2024/Q1"` case, one Excel will actually open.

- A cell column has no column-wide notion of “these are all formulas”,
  so `df[i, j] <- "=SUM(A1:A2)"` writes the eleven characters rather
  than a formula, and warns that it has.
  [`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  returned a classed character vector in 1.5.4 and the class survived a
  row assignment, which is what made the older spelling work; it now
  returns a cell object, where a formula is a property of each cell.
  Build the column and mark it once:

  ``` r

  NOTES[[2]] <- xl_formula(NOTES[[2]])   # after the rows are filled in
  ```

- `xl_hyperlink(name = )` is deprecated in favour of `value`, which now
  occupies the position `name` used to, so positional calls are
  unaffected. Supplying `name` warns; supplying both is an error.

### New features

writexl now reaches the whole feature set of the libxlsxwriter it
bundles. Each entry below names the one or two functions to start from;
the vignettes carry the detail.

- **Cell content** —
  [`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md)
  writes any combination of value, formula, hyperlink, format and
  comment, in mixed-type columns. It also carries array and dynamic
  array formulas, comments
  ([`xl_comment()`](https://docs.ropensci.org/writexl/reference/xl_comment.md))
  and rich strings, one cell in several fonts
  ([`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)).
  [`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  and
  [`xl_hyperlink()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  return these objects and stay backward compatible;
  [`xl_hyperlink()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  now writes a real URL hyperlink, with display text and a tooltip.

- **Formatting** —
  [`xl_format()`](https://docs.ropensci.org/writexl/reference/xl_format.md)
  and the group constructors
  [`xl_font()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md),
  [`xl_fill()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md),
  [`xl_border()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md),
  [`xl_align()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md),
  [`xl_num_format()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  and
  [`xl_protection()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  build reusable format objects that combine with `+`, and apply to a
  cell, a column, a row, a sheet or the workbook.

- **Conditional formatting** — `xl_sheet(conditional =)`, with
  [`xl_cond_cell()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  pairing a rule with a format and
  [`xl_cond_scale()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md),
  [`xl_cond_bar()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  and
  [`xl_cond_icons()`](https://docs.ropensci.org/writexl/reference/xl_conditional.md)
  for colour scales, data bars and icon sets.

- **Data validation** — `xl_sheet(validation = xl_validation(...))`:
  dropdown lists, numeric, date, time and text-length bounds, and custom
  formulas, with the input and error messages Excel shows
  ([\#43](https://github.com/ropensci/writexl/issues/43)).

- **Autofilters** — `xl_sheet(filter = xl_filter(...))`. Excel does not
  apply a filter when a file is opened, so writexl also hides the rows
  the criteria exclude; without that the sheet looks filtered but shows
  every row.
  [`xl_filter_keep()`](https://docs.ropensci.org/writexl/reference/xl_filter_keep.md)
  exposes the same matching rule on its own. The rules reproduce
  Excel’s, which were measured rather than assumed.

- **Worksheets and workbooks** —
  [`xl_sheet()`](https://docs.ropensci.org/writexl/reference/xl_sheet.md)
  carries column and row geometry (in Excel’s units or in pixels),
  frozen and split panes, gridlines, tab state and the opening view,
  protection, outline display
  ([`xl_outline()`](https://docs.ropensci.org/writexl/reference/xl_outline.md)),
  and the error indicators Excel shows on cells it believes are wrong.
  [`xl_workbook()`](https://docs.ropensci.org/writexl/reference/xl_workbook.md)
  and
  [`xl_properties()`](https://docs.ropensci.org/writexl/reference/xl_properties.md)
  set document metadata — custom properties may now be `Date` or
  `POSIXct` — and the workbook-wide formatting defaults, including
  `hyperlink_format = NULL` for hyperlinks with no styling at all.

- **Page setup and printing** — `xl_sheet(page = xl_page_setup(...))`:
  orientation, paper size, margins, scaling and fit-to-pages, centring,
  headers and footers, print area, repeating heading rows and columns,
  manual page breaks, and the print options.

- **Tables** — `xl_sheet(table = xl_table(...))` and
  [`xl_table_column()`](https://docs.ropensci.org/writexl/reference/xl_table_column.md):
  a named, styled range with banded rows, a filter dropdown, an optional
  total row, and per-column headers, formats and formulas.

- **Merged cells** — `xl_sheet(merge = xl_merge(...))`. A merged range
  holds one value, so
  [`xl_merge()`](https://docs.ropensci.org/writexl/reference/xl_merge.md)
  carries its own; merging over cells the data frame filled keeps only
  that value, as it does in Excel.

- **Images** — `xl_sheet(image = xl_image(...))`, floating over the
  cells or placed inside one with `embed = TRUE`. The source may be a
  file path, a raw vector or an in-memory picture (a `raster`, colour
  matrix, RGB array or `nativeRaster`), so a plot never has to touch the
  disk. Also a tiled screen backdrop via `xl_sheet(background_image =)`,
  and images in printed headers and footers. Two arrangements
  libxlsxwriter miscounts — an embedded image alongside any other, and a
  header/footer or background image on a sheet before one with a
  floating image — are refused with the order that works.

- **Charts** — `xl_sheet(chart = xl_chart(...))` and
  [`xl_chart_series()`](https://docs.ropensci.org/writexl/reference/xl_chart_series.md),
  in all 22 types Excel offers, with axes
  ([`xl_chart_axis()`](https://docs.ropensci.org/writexl/reference/xl_chart_axis.md)),
  the parts of a series (markers, data labels, trendlines, error bars
  and a format per point) and the chart’s own furniture (legend, data
  table, plot and chart areas, manual layouts).
  [`xl_chartsheet()`](https://docs.ropensci.org/writexl/reference/xl_chartsheet.md)
  gives one chart a tab of its own.

  A series names its values and categories either as an A1 range
  (`"Data!B2:B10"`) or by column (`list(cols = "revenue")`), so a range
  follows the data when rows are added or a header is written, and a
  series that plots a column is named after that column’s header. Series
  and titles are styled with the ordinary
  [`xl_format()`](https://docs.ropensci.org/writexl/reference/xl_format.md)
  groups —
  [`xl_border()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  becomes the line,
  [`xl_fill()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  the fill,
  [`xl_font()`](https://docs.ropensci.org/writexl/reference/xl_format_groups.md)
  the title text — so one format object can style both a cell and a
  chart.

  Anything the chart cannot draw is refused by name rather than dropped
  silently, which is what Excel does with it: a format group no chart
  shape has, a value-axis option on a category axis, a doughnut hole on
  a bar chart, a data label in a position its chart type disallows.
  Tests read the function lists out of the bundled `chart.h`, so a
  function added upstream surfaces as a failure rather than as a gap.

- **A stand-in for missing values** via `na`, which writexl has always
  written as an empty cell
  ([\#76](https://github.com/ropensci/writexl/issues/76)).
  `write_xlsx(df, na = "not measured")` sets it for a whole workbook,
  `xl_properties(na = )` does the same on a workbook object, and
  `xl_col_spec(na = )` and `xl_cell_general(na = )` narrow it to one
  column or one cell — the innermost setting wins. It covers `NaN` as
  well as `NA`, and keeps its own type, so `na = 0` writes a number and
  leaves a numeric column numeric. The default, `na = NA`, is the empty
  cell as before.

- Argument names are consistent across the new functions. Whatever a
  cell, label or box will show is `value`, whatever its type; a size in
  pixels says so (`width_pixels`); and a caption is `title`, with
  `title_format` and `title_layout` beside it.
  [`as.character()`](https://rdrr.io/r/base/character.html) methods on
  [`xl_cell_general()`](https://docs.ropensci.org/writexl/reference/xl_cell_general.md)
  and
  [`xl_rich_string()`](https://docs.ropensci.org/writexl/reference/xl_rich_string.md)
  mean a cell built for a sheet can be reused anywhere a plain string is
  wanted.

- [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  now errors informatively when a data frame exceeds the xlsx column
  limit (16384) or row limit (1048576).

- Bundled libxlsxwriter updated to 1.2.4.

- See the “Getting started with writexl” vignette, and the five that
  follow it for formatting, worksheets and workbooks, charts and images,
  formulas and tables, and one runnable example of everything.

### Bug fixes

- Fix installation on systems without GNU make, by replacing a
  GNU-specific pattern rule in `src/Makevars` with a portable static
  library recipe
  ([\#97](https://github.com/ropensci/writexl/issues/97)).

- Fix a `strcpy()` buffer overflow in the internal `C_set_tempdir()`; a
  tempdir path of 2048 bytes or more now errors informatively.

## writexl 1.5.4

CRAN release: 2025-04-15

- Fix LTO build for bundled libxlsxwriter

## writexl 1.5.3

CRAN release: 2025-04-06

- [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  now gives a warning if a column is of unsupported type
- Fix crash in
  [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  for corrupted data frames

## writexl 1.5.2

CRAN release: 2025-03-17

- Fix parallel make; cleanup after build

## writexl 1.5.0

CRAN release: 2024-02-09

- Update libxlsxwriter from b0c76b33

## writexl 1.4.2

CRAN release: 2023-01-06

- Bugfix for NA timestamps

## writexl 1.4.1

CRAN release: 2022-10-18

- Fix strict-prototypes warnings

## writexl 1.4.0

CRAN release: 2021-04-20

- Update libxlsxwriter to 1.0.3

## writexl 1.3.1

CRAN release: 2020-08-26

- Fix a unit test in R-devel for timezone attribute comparisons

## writexl 1.3

CRAN release: 2020-05-05

- [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  gains option `use_zip64` for 4GB+ file support
- libxlsxwriter error messages are printed to `REprintf` instead of
  `fprintf`
- Handle overly long or duplicate sheet names
- The help assistant only appears once per session

## writexl 1.2

CRAN release: 2019-11-27

- Update bundled libxlsxwriter 0.8.8
- [`xl_formula()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  and
  [`xl_hyperlink()`](https://docs.ropensci.org/writexl/reference/xl_formula.md)
  now correctly support `NA`
- Oil clippy a bit

## writexl 1.1

CRAN release: 2018-12-02

- Update bundled libxlsxwriter 0.8.4
- Do not write blank xlsx strings for `NA` and `""` character values
- Coerce bit64 vectors to double with warning (xlsx does not have int64)

## writexl 1.0

CRAN release: 2018-05-10

- Save R `Date` types as proper datetime strings
- Update vendored libxlsxwriter to 0.7.6

## writexl 0.2

CRAN release: 2017-09-06

- Add support for lists in
  [`write_xlsx()`](https://docs.ropensci.org/writexl/reference/write_xlsx.md)
  to create xlsx with multiple sheets
- Automatically coerce columns of type `Date` and `hms` to strings

## writexl 0.1

CRAN release: 2017-08-30

- Initial CRAN release with clippy
