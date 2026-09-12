# osm_basemap

Generates a base OSM plot ready for polygon, line, and point objects to
be overlain with
[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md).

## Usage

``` r
osm_basemap(bbox, structures, bg = "gray20")
```

## Arguments

- bbox:

  bounding box (Latitude-longitude range) to be plotted. A 2-by-2 matrix
  of 4 elements with columns of min and max values, and rows of x and y
  values. Can also be an object of class `sf`, for example as returned
  from `extract_osm_objects` or the `osmdata` package, in which case the
  bounding box will be extracted from the object coordinates.

- structures:

  Data frame returned by
  [`osm_structures`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md)
  used here to specify background colour of plot; if missing, the colour
  is specified by `bg`.

- bg:

  Background colour of map (default = `gray20`) only if `structs` not
  given).

## Value

A `ggplot2` object containing the base `map`.

## See also

[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md).

Other construction:
[`add_osm_objects()`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`make_osm_map()`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md),
[`osm_structures()`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md),
[`print_osm_map()`](https://docs.ropensci.org/osmplotr/reference/print_osm_map.md)

## Examples

``` r
bbox <- get_bbox (c (-0.13, 51.5, -0.11, 51.52))
map <- osm_basemap (bbox = bbox, bg = "gray20")
map <- add_osm_objects (map, london$dat_BNR, col = "gray40")
print_osm_map (map)
```
