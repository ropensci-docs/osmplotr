# add_osm_groups

Plots spatially distinct groups of OSM objects in different colours.

## Usage

``` r
add_osm_groups(
  map,
  obj,
  groups,
  cols,
  bg,
  make_hull = FALSE,
  boundary = -1,
  size,
  shape,
  border_width = 1,
  colmat,
  rotate
)
```

## Arguments

- map:

  A `ggplot2` object to which the grouped objects are to be added.

- obj:

  An `sf` data frame of points, polygons, or lines (list of polygons or
  lines) returned by
  [`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md).

- groups:

  A list of spatial points objects, each of which contains the
  coordinates of points defining one group.

- cols:

  Either a vector of \>= 4 colours passed to `colour_mat` (if
  `colmat = TRUE`) to arrange as a 2-D map of visually distinct colours
  (default uses `rainbow` colours), or (if `colmat = FALSE`), a vector
  of the same length as groups specifying individual colours for each.

- bg:

  If given, then any objects not within groups are coloured this colour,
  otherwise (if not given) they are assigned to nearest group and
  coloured accordingly (`boundary` has no effect in this latter case).

- make_hull:

  Either a single boolean value or a vector of same length as groups
  specifying whether convex hulls should be constructed around all
  groups (`TRUE`), or whether the group already defines a hull (convex
  or otherwise; `FALSE`).

- boundary:

  (negative, 0, positive) values define whether the boundary of groups
  should (exclude, bisect, include) objects which straddle the precise
  boundary. (Has no effect if `bg` is given).

- size:

  Linewidth argument passed to `ggplot2` (polygon, path, point)
  functions: determines width of lines for (polygon, line), and sizes of
  points. Respective defaults are (0, 0.5, 0.5).

- shape:

  Shape of points or lines (the latter passed as `linetype`); see
  [`shape`](https://ggplot2.tidyverse.org/reference/aes_linetype_size_shape.html).

- border_width:

  If given, draws convex hull borders around entire groups in same
  colours as groups (try values around 1-2).

- colmat:

  If `TRUE` generates colours according to `colour_mat`, otherwise the
  colours of groups are specified directly by the vector of `cols`.

- rotate:

  Passed to `colour_mat` to rotate colours by the specified number of
  degrees clockwise.

## Value

Modified version of `map` with groups added.

## Note

Any group that is entirely contained within any other group is assumed
to represent a hole, such that points internal to the smaller contained
group are \*excluded\* from the group, while those outside the smaller
yet inside the bigger group are included.

## See also

[`colour_mat`](https://docs.ropensci.org/osmplotr/reference/colour_mat.md),
[`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md).

Other maps-with-data:
[`add_osm_surface()`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md)

## Examples

``` r
bbox <- get_bbox (c (-0.13, 51.5, -0.11, 51.52))
# Download data using 'extract_osm_objects'
if (FALSE) { # \dontrun{
dat_HP <- extract_osm_objects (
    key = "highway",
    value = "primary",
    bbox = bbox
)
dat_T <- extract_osm_objects (key = "tree", bbox = bbox)
dat_BNR <- extract_osm_objects (
    key = "building", value = "!residential",
    bbox = bbox
)
} # }
# These data are also provided in
dat_HP <- london$dat_HP
dat_T <- london$dat_T
dat_BNR <- london$dat_BNR

# Define a function to easily generate a basemap
bmap <- function () {
    map <- osm_basemap (bbox = bbox, bg = "gray20")
    map <- add_osm_objects (map, dat_HP, col = "gray70", size = 1)
    add_osm_objects (map, dat_T, col = "green")
}

# Highlight a single region using all objects lying partially inside the
# boundary (via the boundary = 1 argument)
pts <- cbind (
    c (-0.115, -0.125, -0.125, -0.115),
    c (51.505, 51.505, 51.515, 51.515)
)
if (FALSE) { # \dontrun{
dat_H <- extract_osm_objects (key = "highway", bbox = bbox) # all highways
map <- bmap ()
map <- add_osm_groups (map, dat_BNR,
    groups = pts, cols = "gray90",
    bg = "gray40", boundary = 1
)
map <- add_osm_groups (map, dat_H,
    groups = pts, cols = "gray80",
    bg = "gray30", boundary = 1
)
print_osm_map (map)
} # }

# Generate random points to serve as group centres
set.seed (2)
ngroups <- 6
x <- bbox [1, 1] + runif (ngroups) * diff (bbox [1, ])
y <- bbox [2, 1] + runif (ngroups) * diff (bbox [2, ])
groups <- cbind (x, y)
groups <- apply (groups, 1, function (i) {
    matrix (i, nrow = 1, ncol = 2)
})
# plot a basemap and add groups
map <- bmap ()
cols <- rainbow (length (groups))
if (FALSE) { # \dontrun{
map <- add_osm_groups (
    map,
    obj = london$dat_BNR,
    group = groups,
    cols = cols
)
cols <- adjust_colours (cols, -0.2)
map <- add_osm_groups (map, obj = london$dat_H, groups = groups, cols = cols)
print_osm_map (map)

# Highlight convex hulls containing groups:
map <- bmap ()
map <- add_osm_groups (
    map,
    obj = london$dat_BNR,
    group = groups,
    cols = cols,
    border_width = 2
)
print_osm_map (map)
} # }
```
