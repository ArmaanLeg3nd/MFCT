# MFCT

MFCT - Detection of Pneumonia from Chest CT using Advanced Deep Learning Methodologies

Dataset Link: [Download from Kaggle](https://www.kaggle.com/datasets/anaselmasry/covid19normalpneumonia-ct-images?select=pneumonia_CT)

## Dataset Preparation

### Raw Dataset Preparation

1. Download the dataset from the above link.
2. Create a directory named `Datasets` in the root directory of the project.
3. Extract the dataset to the `Datasets` directory and rename the extracted directory to `Dataset_O`.

```bash
MFCT
├── Datasets
│   ├── Dataset_O
```

### Dataset Creation

The following steps are performed to create a large unlabelled dataset and a small labelled dataset from the original dataset.

1. First 500 images from each class are selected and copied to a new directory named `Dataset_S` in the same sub-directory structure as `Dataset_O`. Also apply data preprocessing steps.

2. Exclude the first 500 images from each class and copy the remaining images to a new directory named `Dataset_L`. Also apply data preprocessing and augmentation steps.

### Data Preprocessing

1. Resize the images to 224x224 pixels.
2. Sharpen(Enhance) the images.

### Data Augmentation

The following data augmentation techniques are applied to the images in `Dataset_L`.

#### Geometric Transformations

1. Horizontal Flip
2. Translation
3. Random Scaling

#### Intensity Transformations

1. Gaussian Noise
2. Contrast Adjustment
3. Brightness Adjustment
4. Gamma Correction

#### Other Transformations

1. Elastic Deformation
2. Gaussian Blur
3. Salt and Pepper Noise

## Metadata Structure

The metadata for `Dataset_L` includes detailed information about the augmentations applied to each image in the dataset. This information is stored in a JSON file named `augmentation_metadata.json`, located in the `.\Dataset` directory of the project.

### Metadata File Location

```bash
.\Dataset\augmentation_metadata.json
```

### JSON Structure

The metadata is organized as a dictionary where each key is an image name and each value is another dictionary that specifies the transformations applied to that image. The structure is as follows:

```json
{
    "image_name": {
        "transformation_1_name": "type",
        "transformation_2_name": "type"
    }
}
```

### Example

An example entry in the augmentation_metadata.json file might look like this:

```json
{
    "204 (10)_5981.jpg": {
        "gaussian_blur": "other",
        "horizontal_flip": "geometric"
    },
    "204 (11)_5982.jpg": {
        "horizontal_flip": "geometric",
        "gauss_noise": "noise",
        "elastic_transform": "other",
        "random_gamma": "color"
    },
}
```

### Field Descriptions

- `image_name`: The name of the image file in the dataset.
- `transformation_name`: The name of the transformation applied to the image. It can be one of the following:
  - `horizontal_flip`
  - `shift_scale_rotate`
  - `gauss_noise`
  - `gaussian_blur`
  - `brightness_contrast`
  - `random_gamma`
  - `elastic_transform`
  - `gaussian_blur`
- `type`: The category of the transformation. It can be one of the following:
  - `geometric`
  - `color`
  - `noise`
  - `other`
