# Point-to-box
> A set of models, tools, and tutorials for the automation of annotating individual objects in images.


This file will become your README and also the index of your documentation.

## Install

`pip install point_to_box`

## How to use

**WORK IN PROGRESS**

The library performs three major functions:

- converting COCO-style object detection images and annotations into point-to-box style images and annotations
- training prompted class-agnostic, single-object localization models
- providing access to models pretrained on COCO data

### Manipulating data

#### Converting data

The `point_to_box.data` module can transform COCO object-detection style images and annotations into point-to-box style images and annotations using a `ConversionDataset`

```python
#hide_output
dataset = data.ConversionDataset(data_path = SRC, anno_fname = ANNOS,
                                 dst_path = DST, img_size = 224)
```

A ConversionDataset can turn images with box annotations like this:


![png](docs/images/output_7_0.png)


Into individual images with point-to-box style annotations like this:


![png](docs/images/output_9_0.png)


The ConversionDataset class has a `convert` method to convert individual images one at a time as well as a `convert_all` method to process all (or a percentage) of the images.

```python
#hide_output
# dataset.convert(184791)
dataset.convert_all()
```

The `to_json()` method writes the new annotations to file and can split the data into training and validation partitions using the `pct` argument. If no percentage is specified the dataset remains unparitioned and is written to a single directory.

```python
#hide_output
dataset.to_json(pct = 0.2)
```

#### Using data

The `point_to_box.data` module contains a `PTBDataset` class designed in the PyTorch style so it can be used with the PyTorch `DataLoader` class.

```python
#hide_output
ptbdata = data.PTBDataset(
    root = DST,
    annos = DST/('individual_'+ANNOS),
    box_format = 'coco')

ptbloader = torch.utils.data.DataLoader(dataset = ptbdata, batch_size = 8)
```

Plotting a batch of images from our converted data let's us confirm that the cropping and box coordinate conversion works as we expect it to.


![png](docs/images/output_17_0.png)


### Training models
