
# Final Project: Public transport density function

Presentation https://prezi.com/p/edit/vaukrenb6waj/


Chapter 1: Import
This chapter sets up the environment by installing necessary libraries for the project, such as owslib, pyproj, geojson, ratelimit, diskcache, tqdm, selenium, and branca. These libraries provide functionality for web feature services, geographic data processing, geocoding, caching, progress bars, web scraping, and colormap creation. Additionally, this chapter mounts Google Drive to access and store data persistently.

Chapter 2: Functions
This chapter defines various functions used throughout the project. Here's a breakdown:

Map Manipulation: add_point_to_map adds markers to a Folium map, while add_shape_to_map adds isochrone polygons to the map.
Data Acquisition: get_berlin_population_density fetches population density data for Berlin using web feature services (owslib). This function is memoized using cache.memoize() to store and reuse results, improving performance. get_coordinates uses geocoding to convert addresses to latitude and longitude.
Isochrone Generation: generate_shape and generate_shape_fast generate isochrones using the TravelTime API. generate_iso_from_input and generate_iso_from_input_fast provide user interfaces to call these functions with address input.
Data Processing: add_centroid_coordinates adds columns with centroid coordinates to a GeoDataFrame. add_is_within_column adds a column to indicate whether points are within a specified polygon.
Visualization: create_population_density_map creates a choropleth map visualizing population density. create_map_with_shapes_and_points displays shapes (isochrones) and points on a map. display_grid_on_map, display_grid_bbox, display_grid_on_map_with_intensity, and display_grid_on_map_with_intensity2 visualize grids, bounding boxes, and heatmaps for reachable population data.
Reachable Population Analysis: pop_reachable calculates the total population reachable within a given time from a location. It integrates isochrone generation, population data filtering, and map visualization. rate_limited_pop_reachable wraps pop_reachable to apply rate limiting and prevent exceeding API call limits.
Grid Generation: generate_grid_coordinates creates a grid of coordinates centered on a specific location, useful for analyzing population reachability over a defined area.
Data Summarization: create_reachable_population_histogram creates histograms of reachable population data for insights into the distribution of reachability.
Chapter 3: Initialize once for Berlin population data
This chapter initializes the population density data for Berlin by calling get_berlin_population_density and adding centroid coordinates using add_centroid_coordinates. These steps are performed once to prepare data for subsequent analysis and visualizations.

Chapter 4: Testing by running Code
This chapter demonstrates the functionalities of the defined functions. It includes examples of:

Generating isochrones using generate_iso_from_input.
Examining isochrone shapes and coordinate systems.
Calculating shapes within isochrones using add_is_within_column.
Creating maps with isochrones and population points.
Calculating reachable populations using pop_reachable with the IronHack location as an example.
Visualizing maps and data with isochrones, population points, grids, bounding boxes, and heatmaps.

Chapter 5: Grid and Heatmap Display
This chapter focuses on generating and visualizing a grid of points along with heatmap representations of population reachability. It includes the following steps:

Defining a grid generation function (generate_grid_coordinates) for creating a grid of points.
Displaying the grid on a map using display_grid_on_map.
Creating a heatmap showing population density using display_grid_on_map_with_intensity.
Generating a normalized heatmap where the intensity represents standard deviations from the mean with display_grid_on_map_with_intensity2.
Generating a histogram visualization of reachable population data with create_reachable_population_histogram.
