[README_WRF_SMN_ARG_Downloader.md](https://github.com/user-attachments/files/29340950/README_WRF_SMN_ARG_Downloader.md)
# WRF SMN ARG Downloader

Python downloader for deterministic WRF forecast NetCDF files produced by Argentina's Servicio Meteorologico Nacional (SMN). The script automatically selects the current UTC model cycle, clears previous files, and downloads both hourly and daily-integrated forecast outputs.

## Objective

Automate the download of SMN Argentina WRF deterministic forecast files.

The script:

- Detects the current UTC date and hour.
- Selects the `00Z` run before 12 UTC and the `12Z` run from 12 UTC onward.
- Deletes previous `.nc` files from the output directory.
- Downloads hourly forecast files from `000` to `071`.
- Downloads 24-hour integrated forecast files from `000` to `002`.
- Saves all files in `Descarga/Archivos/`.

## Repository Structure

```text
WRF_SMN_ARG_Downloader/
└── Descarga/
    ├── Descarga_AUTO_WRF_DET_SMN_AR_4km.py
    └── Archivos/
        └── WRFDETAR_01H_20240402_12_000.nc
```

## Data Source

The downloader uses the public SMN Argentina WRF S3 bucket:

```text
https://smn-ar-wrf.s3.amazonaws.com/DATA/WRF/DET/
```

Hourly forecast URL pattern:

```text
https://smn-ar-wrf.s3.amazonaws.com/DATA/WRF/DET/YYYY/MM/DD/HH/WRFDETAR_01H_YYYYMMDD_HH_FFF.nc
```

Daily integrated forecast URL pattern:

```text
https://smn-ar-wrf.s3.amazonaws.com/DATA/WRF/DET/YYYY/MM/DD/HH/WRFDETAR_24H_YYYYMMDD_HH_FFF.nc
```

## Technologies Used

- Python 3
- requests

## Installation

Clone the repository:

```bash
git clone https://github.com/fabriciolopretto/WRF_SMN_ARG_Downloader.git
cd WRF_SMN_ARG_Downloader/Descarga
```

Install dependencies:

```bash
pip install requests
```

## Usage

Run:

```bash
python Descarga_AUTO_WRF_DET_SMN_AR_4km.py
```

Downloaded files will be saved to:

```text
Descarga/Archivos/
```

## Notes

The script removes all existing `.nc` files in `Descarga/Archivos/` before downloading the new run.

The selected cycle depends on the current UTC time. If the latest SMN run is not yet available, some files may not download correctly.

