# SHREC2025
SHREC 2025: Protein Shape Classification
https://shrec2025.drugdesign.fr/


## Environment Setup
We recommend using conda to create a clean and reproducible environment.

### 1. Create Environment from environment.yml
```bash
conda env create -f environment.yml
conda activate shrec2025
pip3 install -r requirements.txt
```
This will install all necessary packages specified in the YAML file.


### 2. Prepare data
The data can be downloaded by following steps.

```bash
curl -o data/train_set_vtk.tar.gz https://shrec2025.drugdesign.fr/files/train_set_vtk.tar.gz
curl -o data/train_set.csv https://shrec2025.drugdesign.fr/files/train_set.csv
curl -o data/test_set_vtk.tar.gz https://shrec2025.drugdesign.fr/files/test_set_vtk.tar.gz
curl -o data/test_set.csv https://shrec2025.drugdesign.fr/files/test_set.csv

mkdir -p data/train_set
tar -xzf data/train_set_vtk.tar.gz -C data/train_set
mkdir -p data/test_set
tar -xzf data/test_set_vtk.tar.gz -C data/test_set
```

## Run the method

### 1. calculate 3DZD
```bash
# for all train_set, do
mkdir -p output/train_set/
python3 vtk2zd.py data/train_set/8ugd_8:R:3U_model1.vtk output/train_set/8ugd_8:R:3U_model1
#
# for all test_set, do
mkdir -p output/test_set/
python3 vtk2zd.py data/test_set/2320.vtk output/test_set/2320

```

### 2. calculate volume
```bash
python3 calc_volume.py data/train_set.csv output/train_set/ > output/train_set_volume.csv
python3 calc_volume.py data/test_set.csv output/test_set/ > output/test_set_volume.csv
```

### 3. run notebook
You can now run `make_predictions.ipynb`. It will generate `test_predictions.csv` and `test_class_distance_matrix.csv`.

