# ErisData

Data the Eris tools collect, one folder per kind.

| Folder | What it holds | Written by |
| --- | --- | --- |
| `GIS/` | Registries of public GIS sources for US counties, one per dataset (parcels, zoning): adapter specs that point at each county's, city's or state's layer, the counties recorded unavailable and why, and an index from county to adapters | [ErisGISScraper](https://github.com/Eriskii/ErisGISScraper) |

## GIS

The registries hold pointers, not features. Each adapter names a public source (an ArcGIS REST
layer, WFS, OGC API Features or a download), maps its attributes to its dataset's normalized
fields, and records the counties it passed validation for: real features read from the live
source, inside the county, with valid polygons, working paging and filled fields.

| Dataset | Normalized fields | Adapters per county |
| --- | --- | --- |
| `GIS/parcels/` | apn, owner, address, acres, land use, assessed value | One |
| `GIS/zoning/` | zone (the district's code), zone name, jurisdiction, ordinance link | One per jurisdiction: the county's zoning and its cities' |

In each dataset's folder:

| Path | Contents |
| --- | --- |
| `adapters/<id>.json` | One adapter spec per source |
| `unavailable/<fips>.json` | A county with no usable source: the reason (no public GIS, viewer only, paywalled, login required, terms forbid automation, or for zoning none exists), the evidence links and a note |
| `index.json` | County FIPS → the adapters verified for it |

[ErisMaps](https://github.com/Eriskii/ErisMaps) draws parcels and zoning through these
registries, and ErisGISScraper keeps them current (`eris-gis-scraper --dataset <name> run
--recheck`). Tax-map parcels are approximate, not survey boundaries; the adopted zoning map, not
a GIS layer, governs zoning.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use, share and adapt it for any
purpose, crediting ErisData. The license covers this registry; the sources its adapters point
at keep their own terms, noted in each adapter.
