# preferred-tile

[Test change]

A global segmentation where each segment specifies a Sentinel 2 tile from which to read data for any point within the segment. Some properties of the segmentation:
* The segmentation is in WGS84 but can be reprojected to any other coordinate system. No seam artifacts will be introduced by the reprojection.
* For each point within a segment, the specified Sentinel 2 tile has data (in a UTM zone projection) for at least a 9720 m x 9720 m north oriented square patch centered at that point. That means a square patch of at least 6873 m x 6873 m in any orientation, calculated from the 45 deg off-north worst case.
* For each point within a segment, the specified Sentinel 2 tile generally has a UTM projection that gives the smallest north alignment error. In rare cases, a small and redundant segment is eliminated by merging it into a larger segment that specifies an overlapping Sentinel 2 tile, slightly increasing the north alignment error within the eliminated segment.

Limitations:
* Near the poles the segmentation does not reach all the way to the north or south edges of the north or south-most Sentinel 2 tiles. This means that the segmentation is not usable for visualisations that need to show all the data. That would require modificatons in the segmentation for those tiles.

Caveats:
* Segments are split at the antimeridian with id's appended by _0 and _1.

Files:
* `preferred_tiles.geojson` -- The segmentation as a GeoJSON. The properties:
    * `"id"`: Id of the segment, for example `"01CCV"` if there is a one-to-one correspondence between the segment and the Sentinel 2 tile of the same name, or `"01CDH_1"` if multiple segments point to the same tile `"01CDH"`.
    * `"tile_id"`: The Sentinel 2 tile, for example `"01CCV"`
    * `"epsg"`: The EPSG number of the Sentinel 2 UTM tile, as a string, for example `"32701"`
    * `"utm_area"`: The area of the segment, calculated in the Sentinel 2 tile UTM coordinate system, as a number in square meters, for example `514730427.83726776`.

## Prerequisites

Python 3.12 or later.

Pip install:

```
shapely
tqdm
pyproj
pandas
networkx
geopandas
matplotlib
```
