# Checklist Reader – base maps

Optional, downloadable background maps for the map window of **Checklist Reader**.

The program installs with a small built-in world map. The maps listed here are
fetched from inside the program — *Map → Base Maps*, or the map button in the
status bar of the map window — only when the user asks for them. Each one is a
single file, is downloaded once, is checked against the SHA-256 below and works
offline afterwards.

`catalog.json` is the list the program reads. A new map is offered by adding an
entry there and attaching its file to a release of this repository; the program
refuses download addresses outside this repository's releases.

## Maps

| Map | Sharp up to | Size | Source | Licence |
|---|---|---|---|---|
| Relief (Natural Earth) | zoom 7 | 81 MB | Natural Earth 1:10m Cross-blended Hypsometric Tints with Shaded Relief, Water, Drainages and Ocean Bottom (`HYP_HR_SR_OB_DR`, v3.2.0) | Public domain |
| Satellite (NASA Blue Marble) | zoom 8 | 299 MB | NASA Blue Marble: Next Generation with Topography and Bathymetry, July 2004, 500 m (`world.topo.bathy.200407`) | NASA imagery, not subject to copyright |

Beyond its sharpest level the program enlarges the map (softer, but in the
right place). Tiles at the deepest level that show only open ocean are left out
of the files; the program enlarges their parent instead.

## Detail packs

A detail pack holds only the deeper zoom levels of one area. It is listed under
`details` in `catalog.json`, names the map it belongs to in `extends`, and the
program draws it over that map whenever the map is shown; it is never shown on
its own. Program versions without detail packs ignore the `details` list.

All detail packs are drawn over **Satellite (NASA Blue Marble)** and come from
the ESA WorldCover 2021 Sentinel-2 yearly median composite (sea from NASA Blue
Marble), licensed CC BY 4.0. Beyond 70° latitude they stop at zoom 9.

<!-- detail-packs:start -->
| Detail pack | Zoom | Size | Area |
|---|---|---|---|
| Europe (overview) | 9–10 | 374 MB | 25.3° W – 45.7° E, 33.7° N – 72.2° N |
| Germany, Austria and Switzerland | 11–12 | 358 MB | 5.6° E – 17.2° E, 45.7° N – 55.2° N |
| USA, lower 48 states (overview) | 9–10 | 222 MB | 125.2° W – 65.4° W, 23.9° N – 50.3° N |
| Prince Edward Island | 9–12 | 7 MB | 64.7° W – 61.9° W, 45.6° N – 47.5° N |
| Nova Scotia | 9–12 | 45 MB | 66.8° W – 59.1° W, 43.1° N – 47.5° N |
| New Brunswick | 9–12 | 73 MB | 69.6° W – 63.3° W, 44.1° N – 48.5° N |
| Newfoundland and Labrador | 9–11 | 134 MB | 68.2° W – 52.0° W, 46.6° N – 60.6° N |
| Alaska | 9–10 | 178 MB | 170.2° W – 129.4° W, 50.7° N – 71.5° N |
| Australia and New Zealand | 9–10 | 117 MB | 111.8° E – 179.3° E, 48.5° S – 9.8° S |
| Yukon | 9–11 | 270 MB | 141.3° W – 123.8° W, 59.9° N – 69.7° N |
| British Columbia | 9–11 | 273 MB | 139.9° W – 113.9° W, 48.0° N – 60.2° N |
<!-- detail-packs:end -->

## Credits and terms

- **Natural Earth** — free vector and raster map data @ naturalearthdata.com.
  Public domain; no permission or attribution required.
  <https://www.naturalearthdata.com/about/terms-of-use/>
- **NASA Blue Marble: Next Generation** — Reto Stöckli, NASA Earth Observatory.
  NASA imagery is generally not subject to copyright in the United States;
  NASA asks to be acknowledged as the source. The program shows
  "Imagery: NASA Blue Marble" on the map while this map is in use.
  <https://www.nasa.gov/nasa-brand-center/images-and-media/>
- **ESA WorldCover Sentinel-2 composite** (detail packs) — © ESA WorldCover
  project 2021 / Contains modified Copernicus Sentinel data (2021) processed by
  ESA WorldCover consortium. Licensed under
  [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Changes made: the
  red, green and blue bands were scaled to 8-bit colour and resampled to the
  WebMercator tile grid, and open water connected to the sea was replaced by
  NASA Blue Marble. The program shows the credit on the map while a detail
  pack is in use. <https://esa-worldcover.org/en/data-access>
- The land mask used to leave out open ocean is Natural Earth 1:10m land and
  minor islands (public domain); for the Sentinel-2 packs it is the
  composite's own 1-degree tile grid.

Checklist Reader is not affiliated with, sponsored or endorsed by NASA, ESA,
the European Commission, the Copernicus programme or Natural Earth.

## File format

[PMTiles v3](https://github.com/protomaps/PMTiles/blob/main/spec/v3/spec.md):
one file holding the whole WebMercator tile pyramid (256 px JPEG tiles, XYZ
numbering). Any PMTiles viewer, for example <https://pmtiles.io>, can open it.

## How the files were made

GDAL 3.12 (from QGIS 3.44): the source rasters are tiled with
`gdal raster tile` (WebMercatorQuad, cubic resampling at the deepest level,
average for the levels above, JPEG quality 85, Sentinel-2 packs 80), then packed into PMTiles with
the `pmtiles` Python package. The build is reproducible: the same sources give
byte-identical files.

## Files

<!-- files:start -->
| File | SHA-256 |
|---|---|
| `natural-earth-relief-v1.0.pmtiles` | `d06393c6f1c6f4807a03603d7c48162bcc45c8915037254728c0faddf55204f4` |
| `nasa-blue-marble-v1.0.pmtiles` | `7f6325808a0f6f69652dc4c1b88ff806257ee71e82c31d04c0271df610b7c91e` |
| `esa-sentinel2-europe-v1.0.pmtiles` | `3417e0ad2471074e188178ca5155a8833439c5bd0d713c659969ff850a546347` |
| `esa-sentinel2-dach-v1.0.pmtiles` | `f4bafe082ae78382322543cc58397b31cb887ee9be465dc88be36439ff52e29a` |
| `esa-sentinel2-usa-v1.0.pmtiles` | `1cada784e2754bc5b2eeddead842fc3e7057015265fc38d19af72ebdf0e43893` |
| `esa-sentinel2-pei-v1.0.pmtiles` | `488e1f2b31b32c0b988b21424a585ebc6ccdc1238be71b6a0c2478136bb9d93f` |
| `esa-sentinel2-nova-scotia-v1.0.pmtiles` | `27c10f6c0068bfdde996bd70c5769b5c204bb0319f0c03da9d97d6c7e45b7f0c` |
| `esa-sentinel2-new-brunswick-v1.0.pmtiles` | `06f3b734ee9791b0cf1d1f79d55a048ebb5a49239ca38b669c32b731dd0ad470` |
| `esa-sentinel2-newfoundland-labrador-v1.0.pmtiles` | `ece2eda4317605e846b1331e7c1f45c475013117585e6fecc3fb6f727a5b7d9a` |
| `esa-sentinel2-alaska-v1.0.pmtiles` | `2c9e1f2d6f71c45f6e834f91be7d6f86397413296625a83bf0b3c7e981230dfd` |
| `esa-sentinel2-australia-nz-v1.0.pmtiles` | `86234c9d1ac4736c4a9226b576b19cdfbd6526df7c4e3a5962c5e545601dd440` |
| `esa-sentinel2-yukon-v1.0.pmtiles` | `0c773097da186bf8ee4bc3fcd87e895ec8967d7b443dd45b3d1cf988350b1b97` |
| `esa-sentinel2-british-columbia-v1.0.pmtiles` | `437989d471c1d176c7cf707da0cb860d5879cac964b3d6f96e8ac5753316b707` |
<!-- files:end -->
