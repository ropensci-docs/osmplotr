# osm_structures

For the given vector of structure types returns a `data.frame`
containing two columns of corresponding OpenStreetMap `key-value` pairs,
one column of unambiguous suffixes to be appended to the objects
returned by
[`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md),
and one column specifying colours. This `data.frame` may be subsequently
modified as desired, and ultimately passed to
[`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md)
to automate map production.

## Usage

``` r
osm_structures(
  structures = c("building", "amenity", "waterway", "grass", "natural", "park",
    "highway", "boundary", "tree"),
  col_scheme = "dark"
)
```

## Arguments

- structures:

  The vector of types of structures (defaults listed in
  [`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md)).

- col_scheme:

  Colour scheme for the plot (current options include `dark` and
  `light`).

## Value

`data.frame` of structures, `key-value` pairs, corresponding prefixes,
and colours.

## See also

[`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md).

Other construction:
[`add_osm_objects()`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md),
[`make_osm_map()`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md),
[`osm_basemap()`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md),
[`print_osm_map()`](https://docs.ropensci.org/osmplotr/reference/print_osm_map.md)

## Examples

``` r
# Default structures:
osm_structures ()
#>     structure      key value suffix      cols
#> 1    building building           BU #646464FF
#> 2     amenity  amenity            A #787878FF
#> 3    waterway waterway            W #646478FF
#> 4       grass  landuse grass      G #64A064FF
#> 5     natural  natural            N #647864FF
#> 6        park  leisure  park      P #647864FF
#> 7     highway  highway            H #000000FF
#> 8    boundary boundary           BO #C8C8C8FF
#> 9        tree  natural  tree      T #64A064FF
#> 10 background                          gray20
# user-defined structures:
structures <- c ("highway", "park", "ameniiy", "tree")
structs <- osm_structures (structures = structures, col_scheme = "light")
# make_osm_map returns potentially modified list of data
dat <- make_osm_map (osm_data = london, structures = structs)
# map contains updated $osm_data and actual map in $map
# \donttest{
print_osm_map (dat$map)
# }
```
