# extract_osm_objects

Downloads OSM XML objects and converts to Simple Features (`sf`) objects
(`sf` data frames of points, lines, or polygons).

## Usage

``` r
extract_osm_objects(
  bbox,
  key = NULL,
  value,
  extra_pairs,
  return_type,
  geom_only = FALSE,
  quiet = FALSE
)
```

## Arguments

- bbox:

  the bounding box within which all key-value objects should be
  downloaded. A 2-by-2 matrix of 4 elements with columns of min and max
  values, and rows of x and y values.

- key:

  OSM key to search for. Useful keys include `building`, `waterway`,
  `natural`, `grass`, `park`, `amenity`, `shop`, `boundary`, and
  `highway`. Others will be passed directly to the overpass API and may
  not necessarily return results.

- value:

  OSM value to match to key. If `NULL`, all keys will be returned.
  Negation is specified by `!value`.

- extra_pairs:

  A list of additional `key-value` pairs to be passed to the overpass
  API.

- return_type:

  If specified, force return of spatial (`point`, `line`, `polygon`,
  `multiline`, `multipolygon`) objects. `return_type = 'line'` will, for
  example, always return an `sf` data frame of lines. If not specified,
  defaults to 'sensible' values (for example, `lines` for highways,
  `points` for trees, `polygons` for buildings).

- geom_only:

  If `TRUE`, return only those OSM data describing the geometric object;
  otherwise return all data describing each object.

- quiet:

  If `FALSE`, provides notification of progress.

## Value

A Simple Features (`sf`) data frame of points, lines, or polygons.

## See also

[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md).

Other data-extraction:
[`connect_highways()`](https://docs.ropensci.org/osmplotr/reference/connect_highways.md),
[`get_bbox()`](https://docs.ropensci.org/osmplotr/reference/get_bbox.md)

## Examples

``` r
if (FALSE) { # \dontrun{
bbox <- get_bbox (c (-0.13, 51.50, -0.11, 51.52))
dat_B <- extract_osm_objects (key = "building", bbox = bbox)
dat_H <- extract_osm_objects (key = "highway", bbox = bbox)
dat_BR <- extract_osm_objects (
    key = "building",
    value = "residential",
    bbox = bbox
)
dat_HP <- extract_osm_objects (
    key = "highway",
    value = "primary",
    bbox = bbox
)
dat_HNP <- extract_osm_objects (
    key = "highway",
    value = "!primary",
    bbox = bbox
)
extra_pairs <- c ("name", "Royal.Festival.Hall")
dat <- extract_osm_objects (
    key = "building", extra_pairs = extra_pairs,
    bbox = bbox
)
} # }
```
