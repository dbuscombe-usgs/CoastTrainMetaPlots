# đĻ CoastTrain Metadata Plots
[![Last Commit](https://img.shields.io/github/last-commit/dbuscombe-usgs/CoastTrainMetaPlots)](
https://github.com/dbuscombe-usgs/CoastTrainMetaPlots/commits/main)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/dbuscombe-usgs/CoastTrainMetaPlots/graphs/commit-activity)
[![Wiki](https://img.shields.io/badge/wiki-documentation-forestgreen)](https://github.com/dbuscombe-usgs/CoastTrainMetaPlots/wiki)
![GitHub](https://img.shields.io/github/license/dbuscombe-usgs/CoastTrainMetaPlots)
[![Wiki](https://img.shields.io/badge/discussion-active-forestgreen)](https://github.com/dbuscombe-usgs/CoastTrainMetaPlots/discussions)

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

## đ Highlights
- jupyter notebooks for visualizing Coast Train data and metadata
- scripts for computing inter-labeler agreement and make montage figures
- works with [Doodler](https://github.com/Doodleverse/dash_doodler), and [Segmentation Gym](https://github.com/Doodleverse/segmentation_gym)
- models trained using some Coast Train version 1 data sets are included in [Segmentation Zoo](https://github.com/Doodleverse/segmentation_zoo)

## âšī¸ Overview
This repository contains jupyter notebooks and python scripts to create the analyses and plots in Buscombe et al. (in prep) "'Coast Train', a 1.2 Billion Pixel Human-Labeled Dataset for Data-Driven Classification of Coastal Environments", in review. 

Note that this repository contains code only to recreate the plots in the aforementioned paper, and also to provide a programmatic way to query and search the dataset for custom applications. For details about how to access the Coast Train version 1 data themselves, please refer to the [Coast Train website](https://dbuscombe-usgs.github.io/CoastTrain/docs/Version%201:%20March%202022/data) which contains details about where to download and how to unpack the data using companion program [Doodler](https://github.com/Doodleverse/dash_doodler) 

### âī¸ Authors

Package maintainers:
* [@dbuscombe-usgs](https://github.com/dbuscombe-usgs)


## âŦī¸ Installation

### Download 

```
git clone --depth 1 https://github.com/dbuscombe-usgs/CoastTrainMetaPlots.git
```

### Conda environment 

In the terminal:

```
conda env create --file env/coasttrain.yml
```

when it is installed (may take a while), you can activate it like this:

```
conda activate coasttrain
```

### Doodler conda environment 
We also advise creating the [Doodler](https://github.com/dbuscombe-usgs/dash_doodler) conda environment to run the programs. See the [installation instructions](https://github.com/dbuscombe-usgs/dash_doodler#%EF%B8%8F-installation)


## đ Usage

### Metadata
The metadata files are the same as those provided in the official data release but are included here for convenience. Please refer to the [Coast Train website](https://dbuscombe-usgs.github.io/CoastTrain/docs/Version%201:%20March%202022/data) which contains details about where to download and how to unpack the data using companion program [Doodler](https://github.com/Doodleverse/dash_doodler). The csv files containing the following fields


| Variable   |      Description   |
|----------|:-------------:|
| âannotation_image_filenameâ |  npz format file containing the label data archive|
| âclasses_array â |  names of possible classes in this dataset|
| âclasses_integerâ |  one integer per element in âclasses_arrayâ|
| âclasses_present_integerâ |  Image used by the Doodler program. This is the first 3 bands of âorig_imageâ|
| âclasses_present_arrayâ |  one integer per element in âclasses_present_arrayâ|
| âpen_widthâ |  final width in pixels of pen used to annotate|
| âCRF_thetaâ, âCRF_muâ , âCRF_downsample_factorâ, âClassifier_downsample_factorâ, âprob_of_unary_potentialâ, ânum_of_scalesâ  |  internal classifier hyperparameters used by the Doodler program. |
| ânum_classesâ |  number of possible classes in this dataset|
| âdoodle_spatial_densityâ  |  proportion of the image annotated|
| âacc_georefâ |  accuracy in meters of the specification of âXMin,  XMax â and âYMin ,  YMaxâ  |
| âepsgâ |  EPSG code of the projected coordinate system âCRSâ|
| âyear , month, dayâ |  time variables|
| âhour, minute, secondâ |  time variables|
| âXMin,  XMax â |  minimum and maximum Easting of image footprint|
| âYMin ,  YMaxâ   |  minimum and maximum Northing of image footprint|
| âLonMin, LonMaxâ  |  minimum and maximum Longitude (WGS84) of image footprint|
| âLatMin. LatMaxâ   |  minimum and maximum Latitude (WGS84) of image footprint|
| âCRSâ | the projected coordinate system description relating to âXMin,  XMax â and âYMin ,  YMaxâ  |
| âpx_size_mâ  |  horizontal size of pixel in meters|
| âImageHeightPxâ , âImageWidthPxâ, âImageBandsâ |  Number of pixels in horizontal dimensions X and Y, and the number of bands (always 3)|


### Notebooks 
Notebooks that read metadata files in the `metadata` folder can be run by launching a jupyter server in your terminal

```
cd notebooks
jupyter notebook
```

#### plot_class_distribution.ipynb

Allows analysis of the class-image distributions for each data record in turn and overall. Generates the following plots:

* plots/NumLabel_all_datarecords_per_superlabel.png
* plots/Num_images_per_datarecord_containing_superclass.png
* plots/Num_images_per_datarecord_containing_class.png

#### plot_geographic_distribution.ipynb

Allows analysis of the geographic-image distributions for each data record in turn and overall. Generates the following plots:

* plots/Map_satellite_imagery_folium.png
* plots/All_imagery_by_lat_and_lon.png

#### plot_user_distribution.ipynb

Allows analysis of the anonymized labeler-image distributions for each data record in turn and overall. Generates the following plots:

* plots/Label_all_million_pixels_datarecords_per_ID.png
* plots/Label_per_datarecord_per_ID.png
* plots/Label_all_datarecords_per_ID.png
* plots/Million_pixels_vs_percentage_doodled.png
* plots/agreement_stats_coasttrain_naip_s2.png

#### plot_image_locations.ipynb
This notebook simply allows you to visualize where each image is located on a map, one by one


### Scripts
Scripts for computing inter-labeler agreement and make montage figures are run from the command line and require modification to point the paths to the locations where you have downloaded the Coast Train npz files to on your local filesystem.

#### labeler_agreement.py

```
cd scripts 
python labeler_agreement.py
```

generates the following plots
* script_plots/agreement_stats_coasttrain_naip_s2.png
* script_plots/agreement_stats_coasttrain_naip_s2_IOU.png

#### plot_montage.py

```
cd scripts 
python plot_montage.py
```

Produces a montage of example imagery, labels, and overlay masks for each of the datasets, generating the following figures

* script_plots/example_coasttrain_naip.png
* script_plots/example_coasttrain_naip6class.png
* script_plots/example_coasttrain_quads.png
* script_plots/example_coasttrain_madeira.png
* script_plots/example_coasttrain_dauphin.png
* script_plots/example_coasttrain_sandwich.png
* script_plots/example_coasttrain_s2.png
* script_plots/example_coasttrain_s2_4class.png
* script_plots/example_coasttrain_l8.png
* script_plots/example_coasttrain_l8elwha.png

#### plot_montage_remapped.py

```
cd scripts 
python plot_montage_remapped.py
```

Produces a montage of example imagery, labels, and overlay masks for each of the datasets remapped into 7 superclasses, generating the following figures

* script_plots/example_coasttrain_naip_remapped.png
* script_plots/example_coasttrain_naip6class_remapped.png
* script_plots/example_coasttrain_quads_remapped.png
* script_plots/example_coasttrain_madeira_remapped.png
* script_plots/example_coasttrain_dauphin_remapped.png
* script_plots/example_coasttrain_s2_remapped.png
* script_plots/example_coasttrain_s2_4class_remapped.png
* script_plots/example_coasttrain_l8elwha_remapped.png
* script_plots/example_coasttrain_l8_remapped.png
* script_plots/example_coasttrain_sandwich_remapped.png

## :fishing_pole_and_fish: Generating remapped classes

You may use the [Doodler](https://github.com/Doodleverse/dash_doodler) utility `gen_remapped_images_and_labels.py` with the provided config .json format files in the `remap_config_files` folder. When prompted `Select file containing super class names and class aliases`, select one of the provided config (json) files. For each of the npz files in the dataset that the config file describes, the program will create remapped label images with the suffix `_remap_label.jpg`, as well as the images themselves and semi-transparent overlays showing the colorized mask.

