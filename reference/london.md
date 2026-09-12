# london

A list of `Simple Features` (`sf`) `data.frame` objects containing
OpenStreetMap polygons, lines, and points for various OpenStreetMap
structures in a small part of central London, U.K.
(`bbox = -0.13, 51.51, -0.11, 51.52`). The list includes:

1.  `dat_H`: 974 non-primary highways as linestrings

2.  `dat_HP`: 159 primary highways as linestrings

3.  `dat_BNR`: 1,716 non-residential buildings as polygons

4.  `dat_BR`: 43 residential buildings as polygons

5.  `dat_BC`: 67 commerical buildings as polygons

6.  `dat_A`: 372 amenities as polygons

7.  `dat_P`: 13 parks as polygons

8.  `dat_T`: 688 trees as points

9.  `dat_RFH`: 1 polygon representing Royal Festival Hall

10. `dat_ST`: 1 polygon representing 150 Stamford Street

## Format

A list of spatial objects

## Details

The vignette `basic-maps` details how these data were downloaded. Note
that these internal versions have had all descriptive data removed other
than their names, geometries, and their OSM identification numbers.
