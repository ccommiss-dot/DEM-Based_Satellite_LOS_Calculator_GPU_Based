#GNSS / Satellite Line-of-Sight & SAR Analysis Pipeline
##Welcome to the DEM-Based Satellite LOS Calculator! This tool computes satellite visibility and Search & Rescue (SAR) metrics (like Maximum Continuous Blackout Time) over complex terrain using GPU acceleration.

#Overview
This pipeline is designed for high-performance, complex-terrain satellite line-of-sight analysis. It uses a custom CUDA-fused GPU ray-tracing engine to simulate thousands of satellite passes over digital elevation models, calculating precise signal blockages and communication windows.

#Key Features
Ultra-Fast Compute: Uses CuPy and Numba to run millions of ray-tracing operations on NVIDIA GPUs.
Multi-Constellation Support: Simulates Starlink, Globalstar, Iridium, and custom CelesTrak ephemeris data.
SAR Metrics: Calculates Maximum Continuous Blackout Time (MCBT) and the "Golden Window" for optimal communication.
GIS Integration: Exports tactical GeoTIFF rasters and comprehensive CSV point clouds for use in QGIS, ArcGIS, or ATAK.
Interactive Visualizations: Generates HTML-based Folium heatmaps and high-resolution poster graphics.
#How It Works
Environment Setup: Connects to a GPU and installs required spatial/satellite libraries.
Data Loading: Ingests Digital Elevation Models (DEM) and GPX trail data.
Grid & Horizon: Builds a 3D point grid across the terrain and computes horizon blockage angles.
Simulation: Simulates satellite orbits over several days to determine true line-of-sight coverage.
Visualization & Export: Generates interactive maps, high-res charts, and tactical GeoTIFFs.
#Instructions
Open the notebook in a Jupyter environment with GPU access (e.g., Google Colab with a T4 GPU runtime).
Run the environment verification cell to ensure sufficient RAM and VRAM.
Choose whether to run in Demo Mode (using sample data) or Custom Mode (using your own DEM/GPX files).
Execute the notebook sequentially to generate the analysis maps and exports.
#Outputs
Generated files are organized into standard directories:

gis_exports: Master CSVs and Quick Rasters.
gnss_analysis: Tactical GeoTIFFs for GIS software.
urop_poster_assets: High-resolution charts, skyplots, and cross-section profiles.
