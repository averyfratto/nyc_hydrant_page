# NYC Hydrant Density Map

This project maps fire hydrants across New York City's neighborhoods. Click a neighborhood to see its hydrant count and the values behind its color, and hover to outline it.

### Why normalize?

A raw hydrant count mostly shows which neighborhoods are big or densely built. To compare neighborhoods fairly, each map divides the hydrant count by a different measure of size.

| Map | Normalizing variable | Formula | What it tells you |
|---|---|---|---|
| **Hydrants per km²** | Neighborhood land area | hydrants ÷ neighborhood area (km²) | How tightly hydrants are spread across the ground, regardless of what's built there |
| **Hydrants per building** | Number of buildings | hydrants ÷ building count | How many hydrants serve each building. This reflects coverage of the things that need protecting. |
| **Hydrants per km² of building area** | Total building footprint | hydrants ÷ building footprint area (km²) | Hydrants relative to the ground actually covered by buildings. This separates built-up areas from open space. |

### How to read the maps

- Darker colors mean higher values. Each map has its own color scale and legend, so colors aren't comparable across maps.
- The legend uses fixed class breaks rather than a continuous scale.
- Parks, cemeteries, and other neighborhoods with few or no buildings can show zero or very high values, especially on the two building-based maps. Treat those as artifacts of the denominator, not as meaningful patterns.

## The question

Where is hydrant coverage densest in NYC, and which neighborhoods are underserved relative to their area?

## The data

- **NYC Neighborhoods.** 262 polygons (Source: [NYC Open Data](https://opendata.cityofnewyork.us))
- **NYC Fire Hydrants.** 109,725 points (Source: [NYC Open Data](https://opendata.cityofnewyork.us))
- **NYC Building Footprints.** 1.08 M points (Source: https://data.cityofnewyork.us/City-Government/BUILDING/5zhs-2jue/about_data)

## The technology choices

- **MapLibre GL JS** for rendering. Open-source, no vendor lock-in, same API as Mapbox GL JS.
- **PMTiles** for the data layer. One file, no tile server, hosted alongside `index.html` on GitHub Pages.
- **tippecanoe** for tile generation. Polygon recipe with shared-border detection for clean rendering at all zooms.
- **GitHub Pages** for hosting. Free, fast, no infrastructure to maintain.

Total monthly cost: $0. Total servers running: 0.

## How to reproduce

Requires GDAL, tippecanoe, and a tiny local web server.

```bash
git clone https://github.com/{your-username}/nyc-hydrant-map.git
cd nyc-hydrant-map

# Place your PP2 output here:
#   data/raw/hydrant_density.parquet

# Rebuild the .pmtiles
./convert.sh

# Test locally
python3 -m http.server 8000
# open http://localhost:8000
```

## What I learned

The hardest part of this project was learning about structuring and designing html files. More then just making sure a map loads/is correct, what makes a site intuitive? Easy to understand? Engaging? Learning about all the different ways you get creative with fonts, backgrounds, designs, and themes was really fun- but also challenging. In the future, I want to learn more aobut building multiple connecting pages, and having more embedded content. 

## Stack

- MapLibre GL JS 4.5.2
- PMTiles 3.2.0
- tippecanoe (felt fork)
- GitHub Pages
