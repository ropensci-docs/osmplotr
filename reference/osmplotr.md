# osmplotr.

Produces customisable images of OpenStreetMap (OSM) data and enables
data visualisation using OSM objects. Extracts data using the overpass
API. Contains the following functions, data, and vignettes.

## Data Functions

- [`extract_osm_objects`](https://docs.ropensci.org/osmplotr/reference/extract_osm_objects.md):
  Download arbitrary OSM objects

- [`connect_highways`](https://docs.ropensci.org/osmplotr/reference/connect_highways.md):
  Returns points sequentially connecting list of named highways

## Basic Plotting Functions (without data)

- [`add_axes`](https://docs.ropensci.org/osmplotr/reference/add_axes.md):
  Overlay longitudinal and latitudinal axes on plot

- [`add_osm_objects`](https://docs.ropensci.org/osmplotr/reference/add_osm_objects.md):
  Overlay arbitrary OSM objects

- [`make_osm_map`](https://docs.ropensci.org/osmplotr/reference/make_osm_map.md):
  Automate map production with structures defined in
  [`osm_structures`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md)

- [`osm_structures`](https://docs.ropensci.org/osmplotr/reference/osm_structures.md):
  Define structures and graphics schemes for automating map production

- [`osm_basemap`](https://docs.ropensci.org/osmplotr/reference/osm_basemap.md):
  Initiate a `ggplot2` object for an OSM map

- [`print_osm_map`](https://docs.ropensci.org/osmplotr/reference/print_osm_map.md):
  Print a map to specified graphics device

## Advanced Plotting Functions (with data)

- [`add_osm_groups`](https://docs.ropensci.org/osmplotr/reference/add_osm_groups.md):
  Overlay groups of objects using specified colour scheme

- [`add_osm_surface`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md):
  Overlay data surface by interpolating given data

- [`add_colourbar`](https://docs.ropensci.org/osmplotr/reference/add_colourbar.md):
  Overlay a scaled colourbar for data added with
  [`add_osm_surface`](https://docs.ropensci.org/osmplotr/reference/add_osm_surface.md)

## Colour Manipulation Functions

- [`adjust_colours`](https://docs.ropensci.org/osmplotr/reference/adjust_colours.md):
  Lighted or darken given colours by specified amount

- [`colour_mat`](https://docs.ropensci.org/osmplotr/reference/colour_mat.md):
  Generate continuous 2D spatial matrix of colours

## Other Functions

- [`get_bbox`](https://docs.ropensci.org/osmplotr/reference/get_bbox.md):
  return bounding box from input vector

## Data

- [`london`](https://docs.ropensci.org/osmplotr/reference/london.md):
  OSM Data from a small portion of central London

## Vignettes

- `basic-maps`: Describes basics of downloading data and making custom
  maps

- `data-maps`: Describes how map elements can be coloured according to
  user-provided data, whether categorical or continuous

## See also

Useful links:

- <https://docs.ropensci.org/osmplotr/>

- <https://github.com/ropensci/osmplotr>

- Report bugs at <https://github.com/ropensci/osmplotr/issues>

## Author

**Maintainer**: Mark Padgham <mark.padgham@email.com>

Authors:

- Mark Padgham <mark.padgham@email.com>

- Richard Beare

Other contributors:

- Finkelstein Noam (Author of included stub.R code) \[contributor,
  copyright holder\]

- Bartnik Lukasz (Author of included stub.R code) \[contributor,
  copyright holder\]
