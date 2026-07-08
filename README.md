# Berlin Public Transport Accessibility Analysis

> How well does Berlin's public transport actually serve its population? An isochrone-based analysis revealing over- and under-served areas of the city.

<!-- TODO: Wähle deine beste Heatmap und passe den Dateinamen an -->
![Normalized reachability heatmap of Berlin](heatmap_20250306_191746.png)

*Heatmap intensity shows standard deviations from the mean reachable population — blue areas are well connected, red areas are underserved.*

## What it does

For a grid of points across Berlin, this notebook computes **how many people can reach each point within a given travel time** using public transport. Comparing reachable population against local population density reveals which neighborhoods are over- or under-served by the ÖPNV network.

Final outputs: interactive Folium maps, normalized heatmaps, and histograms of the reachable-population distribution.

## Pipeline

1. **Population data** — Berlin population density fetched via WFS (`owslib`) from Berlin's open geodata portal, processed as a GeoDataFrame with centroid coordinates
2. **Isochrones** — travel-time polygons generated per grid point via the TravelTime API (geocoding for address input)
3. **Spatial join** — point-in-polygon tests mark which population cells fall inside each isochrone
4. **Grid & aggregation** — regular coordinate grid over Berlin; reachable population computed per point, with rate limiting and on-disk memoization to respect API limits
5. **Visualization** — choropleth maps, grid overlays, intensity heatmaps (raw and normalized), histograms

## Tech stack

`Python` · `GeoPandas` · `Folium` · `owslib` (WFS) · `TravelTime API` · `pyproj` / `geojson` · `diskcache` (memoization) · `ratelimit` · `branca` · `Selenium` (map export) · `tqdm`

## Key results

<!-- TODO: 2–3 Sätze mit deinen konkreten Erkenntnissen eintragen, z. B.:
"Within a 20-minute travel window, inner-city districts reach up to X people, while parts of [Bezirk] fall more than 2 standard deviations below the city mean." -->

## Run it yourself

1. Clone the repo and open `isochrone_mapping.ipynb`
2. Get a free [TravelTime API](https://traveltime.com/) key and set your `APP_ID` / `API_KEY`
3. Install dependencies:

```bash
pip install geopandas folium owslib pyproj geojson ratelimit diskcache tqdm selenium branca
```

API responses are cached in `cachedir/`, so re-runs are fast and stay within rate limits.

## Slides

📊 [Project presentation (Prezi)](TODO-VIEW-LINK-EINFUEGEN)

<!-- WICHTIG: Der bisherige Link (prezi.com/p/edit/...) ist ein Bearbeiten-Link und funktioniert
     für Außenstehende nicht. In Prezi auf "Präsentieren/Teilen" gehen und den View-Link kopieren. -->

## About

Final project of the **Ironhack Data Analytics Bootcamp** (Berlin, 2025).

Built by **Clemens Fritzen** — mechanical engineer (M.Sc., RWTH Aachen) working at the intersection of manufacturing and data. [LinkedIn](https://de.linkedin.com/in/clemens-fritzen)
