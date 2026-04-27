# DEM-Based Satellite Line-of-Sight (LOS) Calculator — GPU Accelerated

A GPU-accelerated tool for computing satellite **Line-of-Sight (LOS)** visibility over terrain using **Digital Elevation Models (DEMs)**. Built to run entirely in **Google Colab** with CUDA support, making it accessible without any local GPU hardware.

---

## 📌 Overview

This project determines whether a point on the Earth's surface has an unobstructed line-of-sight to a satellite, taking into account the terrain elevation between the observer and the satellite's sub-satellite point. Calculations are massively parallelized using GPU compute (CUDA via CuPy/Numba), enabling rapid LOS analysis over large geographic areas.

**Key capabilities:**
- Load and process GeoTIFF DEM files (SRTM, ALOS, Copernicus, etc.)
- Compute satellite positions from Two-Line Element (TLE) sets using `sgp4`
- Determine LOS visibility for an entire DEM grid in seconds (GPU-accelerated)
- Visualize results as coverage maps overlaid on the terrain

---

## 🗂️ Repository Structure

```
DEM-Based_Satellite_LOS_Calculator_GPU_Based/
├── notebooks/
│   └── DEM_Satellite_LOS_GPU.ipynb   # Main Google Colab notebook
├── data/
│   └── README.md                     # Instructions for obtaining DEM files
├── requirements.txt                  # Python dependencies
├── LICENSE
└── README.md
```

---

## 🚀 Quick Start (Google Colab)

1. Open the notebook in Google Colab:

   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ccommiss-dot/DEM-Based_Satellite_LOS_Calculator_GPU_Based/blob/main/notebooks/DEM_Satellite_LOS_GPU.ipynb)

2. In Colab, go to **Runtime → Change runtime type** and select **GPU** (T4 recommended).

3. Follow the cells in the notebook:
   - Upload your DEM file (`.tif` / `.hgt`) or use one of the download scripts provided.
   - Configure the satellite TLE and observation parameters.
   - Run the GPU-accelerated LOS calculation.
   - View and export the resulting coverage map.

---

## 🌍 DEM Data

The calculator accepts standard raster DEM formats:

| Source | Resolution | Format | Free? |
|---|---|---|---|
| [SRTM (NASA)](https://www2.jpl.nasa.gov/srtm/) | 30 m / 90 m | `.hgt` / GeoTIFF | ✅ |
| [ALOS World 3D (JAXA)](https://www.eorc.jaxa.jp/ALOS/en/dataset/aw3d30/aw3d30_e.htm) | 30 m | GeoTIFF | ✅ |
| [Copernicus DEM (ESA)](https://spacedata.copernicus.eu/collections/copernicus-digital-elevation-model) | 30 m | GeoTIFF | ✅ |

See [`data/README.md`](data/README.md) for detailed download instructions.

> **Note:** Large DEM files (> 100 MB) are not stored in this repository. See `data/README.md` for guidance on obtaining and placing them correctly.

---

## ⚙️ Dependencies

Install all dependencies with:

```bash
pip install -r requirements.txt
```

| Package | Purpose |
|---|---|
| `numpy` | Array math |
| `cupy-cuda12x` | GPU array compute (CUDA 12.x) |
| `rasterio` | Read/write GeoTIFF DEM files |
| `pyproj` | Coordinate reference system transforms |
| `sgp4` | Satellite position from TLE |
| `matplotlib` | Visualization |
| `tqdm` | Progress bars |

> If you are running on a machine with a different CUDA version, replace `cupy-cuda12x` with the matching variant (e.g., `cupy-cuda11x`). On CPU-only machines, the notebook falls back to NumPy automatically.

---

## 🛰️ How It Works

```
 TLE (satellite orbit)
        │
        ▼
  sgp4 propagator  ──►  Satellite XYZ position (ECI → ECEF → LLA)
                                │
        DEM GeoTIFF             │
        │                       │
        ▼                       ▼
  Elevation grid  ──►  GPU LOS ray-march kernel
                                │
                                ▼
                     Visibility boolean grid
                                │
                                ▼
                     Coverage map (PNG / GeoTIFF)
```

The core LOS kernel walks along the great-circle path between each ground pixel and the satellite position, sampling the DEM at regular intervals, and checks whether any terrain elevation exceeds the ray height at that point.

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.