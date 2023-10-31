# baysor2vpt

Small script to convert [Baysor](https://github.com/kharchenkolab/Baysor) cell segmentations into a format that is compatible with Vizgen's segmentation pipeline [vpt](https://github.com/Vizgen/vizgen-postprocessing)

## Usage

```python baysor2vizgen.py --input segmentation_polygons.geojson --output myfile.parquet```

shapely, geopandas, pandas and vpt cli need to be installed.

Takes 5 minutes to run for me for 150,000 cell dataset
