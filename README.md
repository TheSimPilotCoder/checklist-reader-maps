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

| Detail pack | For map | Zoom | Size | Area | Source | Licence |
|---|---|---|---|---|---|---|
| Sentinel-2: Europe (overview) | Satellite (NASA Blue Marble) | 9–10 (about 100 m per pixel) | 374 MB | 25° W – 45° E, 34° N – 72° N | ESA WorldCover 2021 Sentinel-2 yearly median composite, read at 80 m; sea from NASA Blue Marble | CC BY 4.0 |
| Sentinel-2: Germany, Austria and Switzerland | Satellite (NASA Blue Marble) | 11–12 (about 25 m per pixel) | 358 MB | 5.8° E – 17.2° E, 45.8° N – 55.1° N | ESA WorldCover 2021 Sentinel-2 yearly median composite, read at 40 m; sea from NASA Blue Marble | CC BY 4.0 |

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
average for the levels above, JPEG quality 85), then packed into PMTiles with
the `pmtiles` Python package. The build is reproducible: the same sources give
byte-identical files.

## Files

| File | SHA-256 |
|---|---|
| `natural-earth-relief-v1.0.pmtiles` | `d06393c6f1c6f4807a03603d7c48162bcc45c8915037254728c0faddf55204f4` |
| `nasa-blue-marble-v1.0.pmtiles` | `7f6325808a0f6f69652dc4c1b88ff806257ee71e82c31d04c0271df610b7c91e` |
| `esa-sentinel2-europe-v1.0.pmtiles` | `3417e0ad2471074e188178ca5155a8833439c5bd0d713c659969ff850a546347` |
| `esa-sentinel2-dach-v1.0.pmtiles` | `f4bafe082ae78382322543cc58397b31cb887ee9be465dc88be36439ff52e29a` |
