import pandas as pd
from shapely.geometry import Polygon
from shapely.geometry import shape 
import argparse
import subprocess
import geopandas as gpd
import os

parser = argparse.ArgumentParser()
parser.add_argument('--input', type=str, required=True)
parser.add_argument('--output', type=str, required=True)
parser.add_argument('--geocolumn', type=str, required=False, default='geometries')
args = parser.parse_args()

df = pd.read_json(args.input)

df['geometries'] = df[args.geocolumn].apply(lambda x: x if len(x['coordinates'][0]) >= 4 else None)

print(f"Removing {len(df.loc[df['geometries'].isnull()])} geometries with less than 4 points")
df = df.dropna(subset=['geometries'])

df['geometry'] = df['geometries'].apply(lambda x: Polygon(x['coordinates'][0]))
gdf = gpd.GeoDataFrame(df, geometry='geometry')
gdf.to_file(f"temp.geojson", driver='GeoJSON')

command = f"vpt convert-geometry --input-boundaries temp.geojson --output-boundaries {args.output}"

result = subprocess.run(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)

# Check the result
if result.returncode == 0:
    print("Conversion successful.")
    os.remove("temp.geojson")
else:
    print("Error executing vpt tool.")
    print("Error output:\n", result.stderr)
