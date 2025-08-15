# preferred-tile
A global segmentation where each segment specifies a Sentinel 2 tile from which to read data for any point within the segment. Some properties of the segmentation:
* The segmentation is in WGS84 but can be reprojected to any other coordinate system. No seam artifacts will be introduced by the reprojection.
* For each point within a segment, the specified Sentinel 2 tile has data for at least a (roughly) 10 km x 10 km patch centered at that point.
* For each point within a segment, the specified Sentinel 2 tile generally has a UTM projection that gives the smallest north alignment error. In rare cases, a small and redundant segment is eliminated by merging it into a larger segment that specifies an overlapping Sentinel 2 tile, slightly increasing the north alignment error within the eliminated segment.

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