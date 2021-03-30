# Point-to-box
> A set of models, tools, and tutorials for the automation of annotating individual objects in images.


This file will become your README and also the index of your documentation.

## Install

`pip install point_to_box`

## How to use

**WORK IN PROGRESS**

### The data module:

The `point_to_box.data` module can transform COCO object-detection style images and annotations into point-to-box style images and annotations using a `ConversionDataset`

```python
dataset = data.ConversionDataset(data_path = SRC, 
                                 anno_fname = ANNOS,
                                 dst_path = DST,
                                 img_size = 224)
```

    loading annotations into memory...
    Done (t=0.58s)
    creating index...
    index created!


A ConversionDataset can turn images with box annotations like this:


![png](docs/images/output_7_0.png)


Into individual images with point-to-box style annotations like this:


![png](docs/images/output_9_0.png)


The ConversionDataset class has a `convert` method to convert individual images as well as a `convert_all` method to process all the images in the annotation file.
