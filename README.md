# baysor2vzg

Small script to convert [Baysor](https://github.com/kharchenkolab/Baysor) cell segmentations into a format that is compatible with Vizgen's segmentation pipeline [vpt](https://github.com/Vizgen/vizgen-postprocessing)

## Usage

python baysor2vizgen.py --input baysor_output.json --output myfile.parquet

shapely, geopandas, pandas and vpt cli need to be installed.
