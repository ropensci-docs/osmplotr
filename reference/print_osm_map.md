# print_osm_map

Prints an OSM map produced with `osmplotr` to a specified graphics
device.

## Usage

``` r
print_osm_map(
  map,
  width,
  height,
  filename,
  device,
  units = c("in", "cm", "mm", "px"),
  dpi = 300
)
```

## Arguments

- map:

  The map to be printed; a ggplot2 object produced by `osmplotr`.

- width:

  Desired width of graphics device.

- height:

  Desired height of graphics device. Ignored if width specified.

- filename:

  Name of file to which map is to be printed.

- device:

  Type of graphics device (extracted from filename extension if not
  explicitly provided).

- units:

  Units for height and width of graphics device.

- dpi:

  Resolution of graphics device (dots-per-inch).

## Value

(Invisibly) the ggplot2 map object.

## See also

[`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md).

Other construction:
[`add_osm_objects()`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`make_osm_map()`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md),
[`osm_basemap()`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`osm_structures()`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md)

## Examples

``` r
bbox <- get_bbox (c (-0.13, 51.5, -0.11, 51.52))
map <- osm_basemap (bbox = bbox, bg = "gray20")
map <- add_osm_objects (map, london$dat_BNR, col = "gray40")
print_osm_map (map, width = 7) # prints to screen device
# \donttest{
print_osm_map (map, file = "map.png", width = 500, units = "px")
file.remove ("map.png")
#> [1] TRUE
# }
```
