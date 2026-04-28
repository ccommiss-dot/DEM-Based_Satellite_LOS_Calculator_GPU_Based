# GNSS / Satellite Line-of-Sight & SAR Analysis Pipeline

## Welcome to the DEM-Based Satellite LOS Calculator! This tool computes satellite visibility and Search & Rescue (SAR) metrics (like Maximum Continuous Blackout Time) over complex terrain using massive GPU acceleration.

## 📖 Overview

This pipeline is designed for high-performance, complex-terrain satellite line-of-sight analysis. It uses a custom CUDA-fused GPU ray-tracing engine to simulate thousands of satellite passes over digital elevation models (DEMs), calculating precise signal blockages and communication windows caused by physical topography (the "False Horizon" effect).

## ✨ Key Features

Ultra-Fast Compute: Uses CuPy and Numba to run millions of ray-tracing operations in parallel on NVIDIA GPUs, achieving a 1000x speedup over standard CPU models.

Multi-Constellation Support: Simulates Starlink, Globalstar, Iridium, and custom CelesTrak ephemeris (TLE) data.

SAR Metrics: Calculates Maximum Continuous Blackout Time (MCBT) and identifies the "Golden Window" for optimal temporary communication.

GIS Integration: Exports tactical GeoTIFF rasters and comprehensive CSV point clouds for use in QGIS, ArcGIS, or ATAK.

Interactive Visualizations: Generates HTML-based Folium heatmaps and high-resolution poster graphics.

## ⚙️ How It Works

Environment Setup: Connects to a cloud GPU and installs required spatial/satellite orbital libraries.

Data Loading: Ingests high-resolution WGS 84 Digital Elevation Models (DEM) and local GPX trail data.

Grid & Horizon: Builds a 3D point grid across the terrain and computes local azimuthal/elevation horizon blockage angles.

Simulation: Simulates satellite orbits over several days, converting global ECEF coordinates to local ENU frames to determine true physical line-of-sight coverage.

Visualization & Export: Generates interactive maps, high-res charts, and tactical GeoTIFFs.

## 🚀 Instructions

To run this project interactively:

Open the notebook in a Jupyter environment with GPU access (e.g., Google Colab with a T4 or higher GPU runtime).

Run the environment verification cell to ensure sufficient RAM and VRAM.

Choose whether to run in Demo Mode (using pre-loaded sample data) or Custom Mode (uploading your own DEM/GPX files).

Execute the notebook sequentially to generate the analysis maps and exports.

## 📁 Outputs

Generated files are organized into standard directories for easy integration:

gis_exports/: Master CSVs and Quick Rasters.

gnss_analysis/: Tactical GeoTIFFs formatted for professional GIS software.

urop_poster_assets/: High-resolution charts, skyplots, and cross-section profiles.

## 💡 Project Background & AI Usage (Codex Creator Challenge)

This project was inspired by a personal hiking emergency on Mt. Baldy in 2024, where my consumer satellite device failed to connect because sheer canyon walls blocked the signal. To map these invisible dead-zones, I initially built a CPU-based model, which proved far too slow for regional analysis.

Lacking formal computer science training, I utilized generative AI as a collaborative learning tool to bridge my knowledge gaps. AI helped me understand complex geodesic mathematics and transition my codebase to a parallel NVIDIA GPU architecture (CUDA/C++), fundamentally transforming this from a slow conceptual script into a highly scalable, life-saving predictive tool.
