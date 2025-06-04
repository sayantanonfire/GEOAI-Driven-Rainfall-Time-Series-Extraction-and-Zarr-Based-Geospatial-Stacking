README: GEOAI-Driven Rainfall Time Series Extraction and Zarr-Based Geospatial Stacking

📌 Project Title

High-Resolution Rainfall Time Series Extraction Using Centroid-Based Sampling from DEM and Zarr-Based Geospatial Data Stacking for Scalable GEOAI Applications

🌍 Project Summary

This workflow focuses on extracting long-term daily rainfall time series data at a specific point of interest using the centroid of a high-resolution DEM. The project implements automated stacking of multi-year NetCDF rainfall files into a Zarr store, facilitating efficient querying, scalability, and seamless integration into GEOAI pipelines.

📚 Key Objectives

Compute the geographical centroid of a DEM in projected coordinates and convert it to WGS84.

Extract daily rainfall values at this centroid from a set of NetCDF files spanning 30 years.

Store the extracted rainfall time series in a Zarr store using Xarray for scalability and future analytics.

Ensure reproducibility, automation, and modularity to support hydrological and AI-based geospatial research workflows.

🧱 Workflow Components

1. DEM Centroid Computation

Load a high-resolution DEM from a GeoTIFF or Zarr file.

Use the spatial resolution to compute the central pixel's row and column.

Extract the corresponding x/y coordinates in the projected CRS.

Use pyproj.Transformer to convert coordinates to EPSG:4326 (WGS84 lat/lon).

2. NetCDF Rainfall File Handling

Loop through a list of selected IMD gridded rainfall NetCDF files.

Dynamically handle key name differences (e.g., LATITUDE, LONGITUDE, RAINFALL).

Identify the nearest grid index to the DEM centroid.

Extract the rainfall values at that index across the time dimension.

Retrieve the time dimension and convert to pandas datetime for uniformity.

3. Data Assembly in Zarr Format

Flatten the list of daily rainfall arrays into one long array.

Flatten the corresponding time dimension to match.

Construct an xarray.DataArray and wrap in a Dataset.

Save the rainfall dataset as a .zarr file with time indexing.

📦 Output

A Zarr-based dataset: 2_Dynamic_rainfall_centroid_1994_2023.zarr

Variables: rainfall (time)

Time span: Daily data from 1994 to 2023

✅ Advantages of Using Zarr for Geospatial Stacking

Feature

Benefit

Scalability

Efficient handling of large, multi-dimensional datasets

Lazy Loading

Load only the needed chunks, saving memory and computation time

Reusability

Zarr stores are easily accessible across Python scripts and platforms

Web Compatibility

Cloud-native format suitable for distributed processing and web apps

Automation-Friendly

Seamlessly fits into programmatic pipelines for AI/ML

Compression

Reduced storage needs with built-in compression support

🧠 Notes on Positional Accuracy

The centroid computed from dem.tif, dem.zarr, and rioxarray-loaded arrays matched precisely after coordinate transformation.

This assures consistency in sampling points and maintains scientific integrity.

Always ensure CRS alignment (projected vs WGS84) to avoid misalignments during sampling.

🧑‍💻 Professional Considerations

Coordinate Reference Systems (CRS):

Always check if the DEM and NetCDF data are in the same CRS.

Use rioxarray and pyproj for reliable conversions.

Data Chunking and Performance:

When dealing with Zarr, configure chunk sizes appropriately for your analysis scale.

Over-chunking can slow down reads/writes.

Naming Consistency:

NetCDF files from different years or sources might use different key names. Add logic to standardize them.

Time Dimension Handling:

Convert NetCDF time to standard datetime using pandas.to_datetime().

Ensure time alignment across years before stacking.

Data Validation:

Print sample outputs while iterating over files.

Use assertions and error logging to catch silent extraction failures.

Reproducibility:

Use consistent paths, clear function naming, and modularize code.

Share .zarr store and centroid logic for other researchers to reproduce your work.

🧾 Sample Output

🌍 DEM Centroid in WGS84:
Longitude: 79.59326785593657
Latitude : 30.528382540462268

🔄 Processing: RF25_ind1994_rfp25.nc
✅ Extracted daily rainfall (first 5): [0. 0. 0. 0. 0.]
...
💾 Saved rainfall time series to: 2_Dynamic_rainfall_centroid_1994_2023.zarr

🔗 Tools & Libraries Used

xarray, rioxarray, zarr

pyproj, pandas, numpy

File formats: .tif, .zarr, .nc

📌 Final Note

This README reflects a complete integration of spatial and temporal data management within a reproducible GEOAI context. The Zarr-based approach allows scalable, performant, and future-proof workflows ready for cloud, notebooks, or AI applications.

Feel free to adapt, contribute, or cite this methodology in your hydrological, meteorological, or climate informatics research.

📧 Contact

For queries or collaboration, feel free to reach out via LinkedIn or email. Let’s build intelligent, open, and scalable GEOAI solutions together!

email - sayantanonfire@gmail.com
LinkedIn - https://www.linkedin.com/in/sayantan-mandal-36a296213/ 