# DEM Data Files

This directory is where you place your DEM (Digital Elevation Model) raster files before running the notebook.

## Supported Formats

| Format | Extension | Notes |
|---|---|---|
| GeoTIFF | `.tif` / `.tiff` | Preferred — supports embedded CRS metadata |
| SRTM HGT | `.hgt` | 1° × 1° tiles; filename encodes corner coordinate (e.g., `N48E012.hgt`) |

## Recommended Free Data Sources

### 1. SRTM (30 m / 90 m) — NASA / USGS
- **Portal:** <https://earthexplorer.usgs.gov/>
- Sign in (free account), select your area, choose *SRTM 1 Arc-Second Global* or *SRTM 3 Arc-Second Global*, and download tiles.
- Alternatively use the direct FTP mirror:
  ```
  https://e4ftl01.cr.usgs.gov/MEASURES/SRTMGL1.003/2000.02.11/
  ```

### 2. Copernicus DEM (30 m) — ESA
- **Portal:** <https://browser.dataspace.copernicus.eu/>
- Free registration required. Choose *Copernicus DEM GLO-30*.

### 3. ALOS World 3D (30 m) — JAXA
- **Portal:** <https://www.eorc.jaxa.jp/ALOS/en/dataset/aw3d30/aw3d30_e.htm>
- Free registration required.

### 4. OpenTopography (easy API)
```bash
# Example: download 1°×1° SRTM tile via OpenTopography API
curl "https://portal.opentopography.org/API/globaldem?demtype=SRTMGL1&south=48&north=49&west=12&east=13&outputFormat=GTiff&API_Key=<YOUR_KEY>" \
     -o data/dem_N48E012.tif
```

## File Naming Convention

The notebook looks for DEM files matching the pattern `data/*.tif` or `data/*.hgt`. You can also pass an explicit path as a configuration variable at the top of the notebook.

## ⚠️ Git LFS / Large Files

DEM tiles are typically 25 MB – 1 GB each. They are excluded from this repository via `.gitignore`. If you want to version-control your DEM files, consider [Git LFS](https://git-lfs.com/):

```bash
git lfs install
git lfs track "data/*.tif" "data/*.hgt"
git add .gitattributes
```
