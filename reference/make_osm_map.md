# make_osm_map

Makes an entire OSM map for the given bbox using the submitted data, or
by downloading data if none submitted. This is a convenience function
enabling an entire map to be produced according to the graphical format
specified with the `structures` argument.

## Usage

``` r
make_osm_map(
  bbox,
  osm_data,
  structures = osm_structures(),
  dat_prefix = "dat_"
)
```

## Arguments

- bbox:

  The bounding box for the map. A 2-by-2 matrix of 4 elements with
  columns of min and max values, and rows of x and y values. If `NULL`,
  `bbox` is taken from the largest extent of OSM objects in `osm_data`.

- osm_data:

  A list of OSM objects as returned from
  [`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md).
  These objects may be included in the plot without downloading. These
  should all be named with the stated `dat_prefix` and have suffixes as
  given in `structures`.

- structures:

  A `data.frame` specifying types of OSM structures as returned from
  [`osm_structures`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md),
  and potentially modified to alter lists of structures to be plotted,
  and their associated colours. Objects are overlaid on plot according
  to the order given in `structures`.

- dat_prefix:

  Prefix for data structures (default `dat_`). Final data structures are
  created by appending the suffixes from
  [`osm_structures`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md).

## Value

List of two components:

1.  List of OSM structures each as an `sf` data frame of points, lines,
    or polygons, and appended to `osm_data` (which is `NULL` by
    default), and

2.  The `map` as a `ggplot2` object

## Note

If `osm_data` is not given, then data will be downloaded, which can take
some time. Progress is dumped to screen.

## See also

[`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md).

Other construction:
[`add_osm_objects()`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`osm_basemap()`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`osm_structures()`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md),
[`print_osm_map()`](https://docs.ropensci.org/osmplotr/reference/print_osm_map.md)

## Examples

``` r
structures <- c ("highway", "park")
structs <- osm_structures (structures = structures, col_scheme = "light")
# make_osm_map returns potentially modified list of data using the provided
# 'london' data for highways and parks.
dat <- make_osm_map (osm_data = london, structures = structs)
# or download data automatically using a defined bounding boox
bbox <- get_bbox (c (-0.14, 51.51, -0.12, 51.52))
if (FALSE) { # \dontrun{
# This calls the overpass API server to extract data:
dat <- make_osm_map (bbox = bbox, structures = structs)
print_osm_map (dat$map)
} # }
```
