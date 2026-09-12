# osm_line2poly

Converts `sf::sfc_LINSTRING` objects to polygons by connecting end
points around the given bounding box. This is particularly useful for
plotting water and land delineated by coastlines. Coastlines in
OpenStreetMap are lines, not polygons, and so there is no directly way
to plot ocean water distinct from land. This function enables that by
connecting the end points of coastline `LINESTRING` objects to form
closed polygons.

## Usage

``` r
osm_line2poly(obj, bbox)
```

## Arguments

- obj:

  A Simple Features (`sf`) data frame of lines, typically as returned by
  [`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md),
  or by
  [`osmdata::osmdata_sf`](https://docs.ropensci.org/osmdata/reference/osmdata_sf.html).

- bbox:

  bounding box (Latitude-longitude range) to be plotted. A 2-by-2 matrix
  of 4 elements with columns of min and max values, and rows of x and y
  values. Can also be an object of class `sf`, for example as returned
  from `extract_osm_objects` or the `osmdata` package, in which case the
  bounding box will be extracted from the object coordinates.

## Value

A list of three Simple Features (`sf`) data frames, labelled sea islands
and land.

## Details

This is a tricky problem for a number of reasons, and the current
implementation may not be correct, although it does successfully deal
with a few tough situations. Some of the issues are: an osm coastline
query returns a mixture of "ways" and polygons.

Polygons correspond to islands, but not all islands are polygons. A
"way" is a connected set of points with the land on the left. A piece of
coastline in a bounding box may consist of multiple ways, which need to
be connected together to create a polygon. Also, ways extend outside the
query bounding box, and may join other ways that enter the bounding box
(e.g ends of a peninsula). The degree to which this happens depends on
the scale of the bounding box. Coastlines may enter at any bounding box
edge and exit at any other, including the one they entered from.

## See also

Other map-extra:
[`add_axes()`](https://docs.ropensci.org/osmplotr/reference/add_axes.md),
[`add_colourbar()`](https://docs.ropensci.org/osmplotr/reference/add_colourbar.md)

## Examples

``` r
# This example uses the \code{osmdata} package to extract data from
# a named bounding box
if (FALSE) { # \dontrun{
library (magrittr)
library (osmdata)
bb <- osmdata::getbb ("melbourne, australia")
coast <- extract_osm_objects (
    bbox = bb,
    key = "natural",
    value = "coastline",
    return_type = "line"
)
coast <- osm_line2poly (coast, bbox = bb)
# The following map then colours in just the ocean:
map <- osm_basemap (bbox = bb) %>%
    add_osm_objects (coast$sea, col = "lightsteelblue") %>%
    print_osm_map ()
} # }
```
