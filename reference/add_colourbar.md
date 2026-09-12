# add_colorbar

Adds a colourbar to an existing map. Intended to be used in combination
with
[`add_osm_surface`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md).
At present, only plots on right side of map.

## Usage

``` r
add_colourbar(
  map,
  barwidth = 0.02,
  barlength = 0.7,
  zlims,
  cols,
  vertical = TRUE,
  alpha = 0.4,
  text_col = "black",
  fontsize = 3,
  fontface,
  fontfamily,
  ...
)
```

## Arguments

- map:

  A `ggplot2` object to which the colourbar is to be added.

- barwidth:

  Relative width of the bar (perpendicular to its direction), either a
  single number giving distance from right or upper margin, or two
  numbers giving left/right or lower/upper limits.

- barlength:

  Relative length of the bar (parallel to its direction), either a
  single number giving total length of centred bar, or two numbers
  giving lower/upper or left/right limits.

- zlims:

  Vector of (min,max) values for scale of colourbar. These should be the
  values returned from
  [`add_osm_surface`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md).

- cols:

  Vector of colours.

- vertical:

  If `FALSE`, colourbar is aligned horizontally instead of default
  vertical alignment.

- alpha:

  Transparency level of region immediately surrounding colourbar,
  including behind text. Lower values are more transparent.

- text_col:

  Colour of text, tick marks, and lines on colourbar.

- fontsize:

  Size of text labels (in `ggplot2` terms; default=3).

- fontface:

  Fontface for colourbar labels (1:4=plain,bold,italic,bold-italic).

- fontfamily:

  Family of colourbar font (for example, \``Times`').

- ...:

  Mechanism to allow many parameters to be passed with alternative names
  (such as `xyz` for `fontxyz`).

## Value

Modified version of `map` with colourbar added.

## See also

[`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`add_osm_surface`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md).

Other map-extra:
[`add_axes()`](https://docs.ropensci.org/osmplotr/reference/add_axes.md),
[`osm_line2poly()`](https://docs.ropensci.org/osmplotr/reference/osm_line2poly.md)

## Examples

``` r
bbox <- get_bbox (c (-0.13, 51.5, -0.11, 51.52))
map <- osm_basemap (bbox = bbox, bg = "gray20")
# Align volcano data to lat-lon range of bbox
dv <- dim (volcano)
x <- seq (bbox [1, 1], bbox [1, 2], length.out = dv [1])
y <- seq (bbox [2, 1], bbox [2, 2], length.out = dv [2])
dat <- data.frame (
    x = rep (x, dv [2]),
    y = rep (y, each = dv [1]),
    z = as.numeric (volcano)
)
map <- add_osm_surface (map,
    obj = london$dat_BNR, dat = dat,
    cols = heat.colors (30)
)
#> Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
#> ℹ Please use `linewidth` instead.
#> ℹ The deprecated feature was likely used in the osmplotr package.
#>   Please report the issue at <https://github.com/ropensci/osmplotr/issues>.
map <- add_axes (map)
# Note colours of colourbar can be artibrarily set, and need not equal those
# passed to 'add_osm_surface'
map <- add_colourbar (map,
    zlims = range (volcano), cols = heat.colors (100),
    text_col = "black"
)
print_osm_map (map)

# Horizontal colourbar shifted away from margins:
map <- osm_basemap (bbox = bbox, bg = "gray20")
map <- add_osm_surface (map,
    obj = london$dat_BNR, dat = dat,
    cols = heat.colors (30)
)
map <- add_colourbar (map,
    zlims = range (volcano), cols = heat.colors (100),
    barwidth = c (0.1, 0.15), barlength = c (0.5, 0.9),
    vertical = FALSE
)
print_osm_map (map)
```
