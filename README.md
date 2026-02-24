# mapas-looker
Optimized TopoJSON files of Brazilian municipalities for high-performance choropleth maps in Google Looker Studio via Vega-Lite. Solves rendering issues by mapping geometries directly to IBGE codes.

# Optimized Brazil Municipalities TopoJSON for Looker Studio

This repository hosts optimized **TopoJSON** geometry files for Brazilian municipalities (5,570 cities).

It is designed to be used with **Vega-Lite** visualizations in **Google Looker Studio**, bypassing the limitations of the native Google Maps chart (such as slow rendering and inaccurate city matching by name).

## 🚀 Features

* **Lightweight:** Geometries simplified using the Douglas-Peucker algorithm to ensure fast rendering in web dashboards without losing essential shape details.
* **Accurate:** Mapped using the official **IBGE Code** (7 digits or 6 digits), ensuring 100% fill rate for choropleth maps.
* **Ready for Production:** Formatted specifically for the Vega-Lite "lookup" transform.

## 🛠️ Usage in Looker Studio

1.  Add a **Vega-Lite** chart to your report.
2.  Use the raw URL of the JSON file in this repo.
3.  Configure the `lookup` transformation to match your dataset's IBGE code with the TopoJSON ID.

### Example Vega-Lite Configuration

```json
{
  "$schema": "[https://vega.github.io/schema/vega-lite/v5.json](https://vega.github.io/schema/vega-lite/v5.json)",
  "data": {
    "url": "[https://raw.githubusercontent.com/YOUR_USERNAME/REPO_NAME/main/br_municipios_otimizado.json](https://raw.githubusercontent.com/YOUR_USERNAME/REPO_NAME/main/br_municipios_otimizado.json)",
    "format": {"type": "topojson", "feature": "municipios"}
  },
  "transform": [
    {
      "lookup": "properties.id",
      "from": {
        "data": {"name": "values"},
        "key": "YOUR_DATASET_IBGE_CODE_FIELD",
        "fields": ["METRIC_FIELD", "CITY_NAME_FIELD"]
      }
    }
  ],
  "mark": {"type": "geoshape", "stroke": "white", "strokeWidth": 0.5},
  "encoding": {
    "color": {"field": "METRIC_FIELD", "type": "quantitative"}
  }
}
