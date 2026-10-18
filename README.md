# Geospatial Data Visualization with Python (Geoplotlib)

A data science project exploring interactive geospatial data visualization with
the **Geoplotlib** library, built as part of the CISC7204 Data Science and Data
Visualization course (Suggested Exercise 08).

## Problem / Research Question

How can interactive map visualizations help us understand spatial patterns in
real-world datasets? Specifically, this project examines:

1. How are wildlife poaching incidents distributed across Tanzania?
2. How do US states compare in terms of land area (CENSUSAREA)?
3. How do major world cities cluster geographically, and what spatial structure
   emerges when we filter cities by country and by name pattern?

## Dataset Source and Usage Permissions

| Dataset | Source | Permissions | In this repo |
|---|---|---|---|
| `poaching_points_cleaned.csv` | Course tutorial material (CISC7204, based on publicly reported poaching incident records) | Educational use, provided by course instructor | ✅ shipped in `Datasets/` |
| `us_states.json` | US Census Bureau state boundaries & attributes (via course tutorial) | Public domain / educational use | ❌ course material (used in Exercise 8.02) |
| `world_cities_pop.csv` | GeoNames world cities database (population > 0), subset provided by course | Open data (GeoNames), educational use | ❌ course material (164 MB, used in Activity 8.01) |
| `flight_tracking.csv` | Course sample flight tracking records | Educational use, provided by course instructor | ❌ course material (used in Exercise 8.04) |

No passwords, API keys, or personal data are included in this repository.

## Methods and Tools Used

- **Python 3.13** (Anaconda distribution)
- **pandas / NumPy / SciPy** — data cleaning, manipulation, and spatial
  geometry (Delaunay triangulation, Voronoi tessellation)
- **Geoplotlib 0.3.2** — interactive map rendering (dot, hist, voronoi,
  choropleth, and custom animated layers)
- **pyglet 1.5.31** — windowing/rendering backend for Geoplotlib
- **Pillow (PIL)** — custom tile processing (e.g., darkmatter tile inversion)
- **Jupyter Notebook / JupyterLab** — literate analysis environment

## Key Findings and One Limitation

**Findings:**
- Poaching incidents in the study dataset are strongly clustered in the
  central–western region of Tanzania (villages such as Igurusi, Chimala,
  Mbeya), rather than being uniformly distributed — clearly visible with the
  dot and histogram layers in `MC659782_Exercise8.01.ipynb`.
- A choropleth of US states by land area (CENSUSAREA) shows large states such
  as Texas dominating the color scale by area, a good example of how a single
  attribute can drive a color map.
- Delaunay triangulation over European cities (population > 100,000) reveals
  dense connectivity clusters around Germany and the UK, and filtering cities
  by starting letter (e.g., "Z") produces clean interactive point maps.

**Limitation:**
- Map tile rendering depends on external tile servers (OpenStreetMap FR
  humanitarian tiles were used); offline execution requires a local tile
  cache, and the "darkmatter" style is an approximate inversion of standard
  tiles rather than the original CartoDB style.

## Instructions for Running the Analysis

```bash
# 1. Create the environment (Anaconda Python 3.x recommended)
conda create -n geoplot python=3.13 -y
conda activate geoplot

# 2. Install dependencies
#    Note: PyPI's geoplotlib sdist still ships the deprecated "use_2to3"
#    setup flag, so install it from source after removing that line:
pip install pyglet==1.5.31 pandas numpy scipy pillow jupyter
git clone https://github.com/andrea-cristina/geoplotlib  # or pip download geoplotlib==0.3.2 --no-binary :all:
#    remove `use_2to3 = True` from setup.py, then:
pip install . --no-build-isolation

# 3. Launch Jupyter and run the main showcase notebook (from this repo root):
jupyter notebook MC659782_Exercise8.01.ipynb
```

The `Datasets/poaching_points_cleaned.csv` file is included in this repository,
and the notebook reads it via `Datasets/poaching_points_cleaned.csv`. Maps are
saved as PNG files in the notebook outputs; the key visualizations are also
stored under `visualizations/`.

> The other notebooks of the full course project (Exercise 8.02–8.04,
> Activity 8.01–8.02) require the course-provided datasets listed in the table
> above; the three showcase visualizations produced by the wider project are
> included in `visualizations/` for reference.
