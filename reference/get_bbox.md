# get_bbox

Converts a string of latitudes and longitudes into a square matrix to be
passed as a `bbox` argument (to
[`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md),
[`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
or
[`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md)).

## Usage

``` r
get_bbox(latlon)
```

## Arguments

- latlon:

  A vector of (longitude, latitude, longitude, latitude) values.

## Value

A 2-by-2 matrix of 4 elements with columns of min and max values, and
rows of x and y values.

## See also

Other data-extraction:
[`connect_highways()`](https://docs.ropensci.org/osmplotr/reference/connect_highways.md),
[`extract_osm_objects()`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md)

## Examples

``` r
bbox <- get_bbox (c (-0.15, 51.5, -0.1, 51.52))
```
