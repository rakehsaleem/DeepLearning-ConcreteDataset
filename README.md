# Concrete Crack Detection dataset
This repository contains the dataset for the implementation of Keras MaskRCNN on concrete cracks. You can
[refer to this](https://github.com/fizyr/keras-maskrcnn) for training on custom dataset.

## Training on Your own Custom Dataset
For training on a [custom dataset], a CSV file can be used as a way to pass the data. See below for more details on the format of these
CSV files. To train using your CSV, run:

* Running directly from the repository:

`./keras_maskrcnn/bin/train.py csv /path/to/csv/file/containing/annotations /path/to/csv/file/containing/classes`

* Using the installed script:

`maskrcnn-train csv /path/to/csv/file/containing/annotations /path/to/csv/file/containing/classes`

## CSV datasets

The **`CSVGenerator`** provides an easy way to define your own datasets. It uses two CSV files: one file containing annotations and one file
containing a class name to ID mapping. The annotations were done using **`MATLAB`** image labeler for pixel wise annotations.

### Annotations format
The CSV file with annotations should contain one annotation per line. Images with multiple bounding boxes should use one row per bounding
box. Note that indexing for pixel values starts at 0. The expected format of each line is:

`path/to/image.jpg,x1,y1,x2,y2,class_name,/path/to/mask.png`

Some images may not contain any labeled objects. To add these images to the dataset as negative examples, add an annotation where **`x1`**,
**`y1`**, **`x2`**, **`y2`**, **`class_name`** and **`mask`** are all empty:

`path/to/image.jpg,,,,,,`

A full example:

`/data/imgs/img_001.jpg,837,346,981,456,cow,/data/masks/img_001_001.png`
`/data/imgs/img_002.jpg,215,312,279,391,cat,/data/masks/img_002_001.png`
`/data/imgs/img_002.jpg,22,5,89,84,bird,/data/masks/img_002_002.png`
`/data/imgs/img_003.jpg,,,,,,`

This defines a dataset with 3 images. **`img_001.jpg`** contains a cow. **`img_002.jpg`** contains a cat and a bird. **`img_003.jpg`** contains no
interesting objects/animals.

### Class mapping format
The class name to ID mapping file should contain one mapping per line. Each line should use the following format:

`class_name,id`

Indexing for classes starts at 0. Do not include a background class as it is implicit. As in my case, I have focused on 1 class to
differentiate the cracks only so my class mapping has only 1 category.

For example:

`crack,0`
