# Berlin Public Transport Accessibility Analysis

> How well does Berlin's public transport actually serve its population? An isochrone-based analysis revealing over- and under-served areas of the city.

![Normalized reachability heatmap of Berlin](heatmap_main.jpg)

*Heatmap intensity shows standard deviations from the mean reachable population — blue areas are well connected, red areas are underserved.*

## What it does

For a grid of points across Berlin, this notebook computes **how many people can reach each point within a given travel time** using public transport. Comparing reachable population against local population density reveals which neighborhoods are over- or under-served by the ÖPNV network.

Final outputs: interactive Folium maps, normalized heatmaps, and histograms of the reachable-population distribution.

## Key results

- Built on the full Berlin population raster: **3.88 million inhabitants** (2023 data via Berlin Open Data WFS)
- Final analysis grid: **28,900 points at 200 m spacing**, covering a ~34 × 34 km area centred on Brandenburger Tor
- Within **25 minutes by public transport**, well-connected locations reach **300,000+ people** — while poorly connected grid points reach only a few hundred: a spread of three orders of magnitude across the city
- The final map compares each location's 25-minute transit reach against its 25-minute **walking** reach, exposing where the network genuinely adds accessibility and where it leaves neighborhoods behind

## Pipeline

1. **Population data** — Berlin population density fetched via WFS (`owslib`) from Berlin's open geodata portal, processed as a GeoDataFrame with centroid coordinates
2. **Isochrones** — travel-time polygons generated per grid point via the TravelTime API (geocoding for address input)
3. **Spatial join** — point-in-polygon tests mark which population cells fall inside each isochrone
4. **Grid & aggregation** — regular coordinate grid over Berlin; reachable population computed per point, with rate limiting and on-disk memoization to respect API limits
5. **Visualization** — choropleth maps, grid overlays, intensity heatmaps (raw and normalized), histograms

## Tech stack

`Python` · `GeoPandas` · `Folium` · `owslib` (WFS) · `TravelTime API` · `pyproj` / `geojson` · `diskcache` (memoization) · `ratelimit` · `branca` · `Selenium` (map export) · `tqdm`

## Run it yourself

1. Clone the repo and open `Isochrone_Mapping (2).ipynb`
2. Get a free [TravelTime API](https://traveltime.com/) key and set your `APP_ID` / `API_KEY`
3. Install dependencies:

```bash
pip install geopandas folium owslib pyproj geojson ratelimit diskcache tqdm selenium branca
```

API responses are cached in `cachedir/`, so re-runs are fast and stay within rate limits.

## About

Final project of the **Ironhack Data Analytics Bootcamp** (Berlin, 2025).

Built by **Clemens Fritzen** — mechanical engineer (M.Sc., RWTH Aachen) working at the intersection of manufacturing and data. [LinkedIn](https://de.linkedin.com/in/clemens-fritzen)
