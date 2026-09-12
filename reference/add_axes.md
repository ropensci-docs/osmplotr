# add_axes

Adds axes to the internal region of an OSM plot.

## Usage

``` r
add_axes(
  map,
  colour = "black",
  pos = c(0.02, 0.03),
  alpha = 0.4,
  fontsize = 3,
  fontface,
  fontfamily,
  ...
)
```

## Arguments

- map:

  A `ggplot2` object to which the axes are to be added.

- colour:

  Colour of axis (determines colour of all elements: lines, ticks, and
  labels).

- pos:

  Positions of axes and labels relative to entire plot device.

- alpha:

  alpha value for semi-transparent background surrounding axes and
  labels (lower values increase transparency).

- fontsize:

  Size of axis font (in `ggplot2` terms; default=3).

- fontface:

  Fontface for axis labels (1:4=plain,bold,italic,bold-italic).

- fontfamily:

  Family of axis font (for example, \``Times`').

- ...:

  Mechanism to allow many parameters to be passed with alternative names
  (`color` for `colour` and `xyz` for `fontxyz`.

## Value

Modified version of `map` with axes added.

## See also

[`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md).

Other map-extra:
[`add_colourbar()`](https://docs.ropensci.org/osmplotr/reference/add_colourbar.md),
[`osm_line2poly()`](https://docs.ropensci.org/osmplotr/reference/osm_line2poly.md)

## Examples

``` r
bbox <- get_bbox (c (-0.13, 51.5, -0.11, 51.52))
map <- osm_basemap (bbox = bbox, bg = "gray20")
map <- add_osm_objects (map, london$dat_BNR, col = "gray40")
map <- add_axes (map)
print (map)


# Map items are added sequentially, so adding axes prior to objects will
# produce a different result.
map <- osm_basemap (bbox = bbox, bg = "gray20")
map <- add_axes (map)
map <- add_osm_objects (map, london$dat_BNR, col = "gray40")
print_osm_map (map)
```
