# ErisData

Data the Eris tools collect, one folder per kind.

| Folder | What it holds | Written by |
| --- | --- | --- |
| `GIS/` | A registry of public parcel sources for US counties: adapter specs that point at each county's (or state's) parcel service, the counties recorded unavailable and why, and an index from county to adapter | [ErisGISScraper](https://github.com/Eriskii/ErisGISScraper) |

## GIS

The registry holds pointers, not parcel data. Each adapter names a public source (an ArcGIS
REST layer, WFS, OGC API Features or a download), maps its attributes to a normalized schema
(apn, owner, address, acres, land use, assessed value), and records the counties it passed
validation for: real parcels read from the live source, inside the county, with valid polygons,
working paging and filled fields.

| Path | Contents |
| --- | --- |
| `GIS/adapters/<id>.json` | One adapter spec per source |
| `GIS/unavailable/<fips>.json` | A county with no usable source: the reason (no public GIS, viewer only, paywalled, login required, terms forbid automation), the evidence links and a note |
| `GIS/index.json` | County FIPS → the adapters verified for it |

[ErisMaps](https://github.com/Eriskii/ErisMaps) draws parcels through this registry, and
ErisGISScraper keeps it current (`eris-gis-scraper run --recheck`). Tax-map parcels are
approximate, not survey boundaries.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): use, share and adapt it for any
purpose, crediting ErisData. The license covers this registry; the sources its adapters point
at keep their own terms, noted in each adapter.
