Note: this preliminary release subject to change.

# preferred-tile

A global non-overlapping and exhaustive spatial partitioning or segmentation where each segment corresponds to a single Sentinel 2 tile. Properties:
* The segmentation is in WGS84 but can be reprojected to any other coordinate system. No seam artifacts will be introduced by the reprojection, because neighboring segments share polygon vertices.
* For each point within a segment, the corresponding Sentinel 2 tile has data for at least a roughly 9720 m x 9720 m north-oriented square patch centered at that point. This corresponds to a square patch of at least 6873 m x 6873 m in any orientation (45-degree worst case).
* For each point within a segment, the corresponding Sentinel 2 tile generally has a UTM projection that gives the smallest north alignment error. However, some small segments have been eliminated when they can be wholly merged into into a larger segment with another UTM zone projection, somewhat increasing the north alignment error.

Limitations:
* Near the poles the segmentation does not reach all the way to the north or south edges of the north or south-most Sentinel 2 tiles. This means that the segmentation is not usable for visualisations that need to show all the data near the poles, without modification of the segmentation

Technical notes:
* Segments are split at the antimeridian with id's appended by _0 and _1.

Files:
* `preferred_tiles.geojson` -- The segmentation as a GeoJSON. The properties:
    * `"id"`: Id of the segment, for example `"01CCV"` if there is a one-to-one correspondence between the segment and the Sentinel 2 tile of the same name, or `"01CDH_1"` if multiple segments point to the same tile `"01CDH"`.
    * `"tile_id"`: The Sentinel 2 tile, for example `"01CCV"`
    * `"epsg"`: The EPSG number of the Sentinel 2 tile, as a string, for example `"32701"`, corresponding to a UTM zone.
    * `"utm_area"`: The area of the segment, calculated with the vertices projected to the UTM coordinate system, as a number in square meters, for example `514730427.83726776`.

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
