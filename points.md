```sql
COPY (SELECT
      id as gers_id,
     categories.primary AS category,
    addresses[1].freeform as street,
    addresses[1].locality as locality,
    sources[1].dataset as primary_source,
      geometry
  FROM read_parquet('s3://overturemaps-us-west-2/release/2024-10-23.0/theme=places/*/*')
  WHERE
      names.primary LIKE 'Wawa'
     AND  bbox.xmin BETWEEN -77.51 AND -73.2
     AND bbox.ymin BETWEEN 38.87 AND 41.45)
     TO 'wawa_places-philly-nj.geojson' WITH (FORMAT GDAL, DRIVER 'GeoJSON', SRS 'EPSG:4326');
```


| ![wawa in philly](philly-area-wawa.png) |
|:--:|
| *Philly <3 Wawa* |
