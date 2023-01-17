# Was zu tun:

- [ ] find a way to select the models, namely a way to choose the models to test
- [ ] Find a way to test the models by reading training time for number of epoch (from 1 to 20). Do not use the timing from fastai, but calculate it your self
- [ ] Collect everything in a dictionary and save it as txt file
- [ ] Plot everything in a nice way. Basically, do some data visualization



# RAW cars dataset

This repository contains 225 RAW images of scenes containing cars.

A description of the repo directories follows:

## RAW_converted
The original RAW images have been scaled to [0, 255] from their original scale of [0, 1023] and converted to the lossless PNG image format. This reduces their size and make circulation feasible. 

The edge pixels have been deleted, for they are removed by the ISP in the processed images. The ISP does so because these pixels do not receive enough illumination.

## ISP_processed
The image signal processed images can be found in ISP_processed directory. These images are in JPG format.

## Annotations
The annotations for the images can be found in annotations.xls

The image number is given in the imageFilename column and the coordinates for bounding boxes are given in coords_i columns.
A consecutive quadruple of coords columns forms a single bounding box, and has the following format:

box = [top_left_x, top_left_y, box_height, box_width]

# Original RAW images
For experimentation purposes, the original RAW images have been uploaded in a google drive and are available at the following link: https://goo.gl/vqSvdE

These images have been converted to the lossless TIFF format. Since .tiff images can be directly processed by any modern vision library, this will allow increased productivity.

# Results
Using an off-the-shelf faster-RCNN network, we are able to achieve the following accuracies:

| Image Format | Accuracy |
| --- | --- |
| Original RAW images in the converted format | 36.13% |
| RAW images with gamma compression and pixel binning | 95.04% |
| JPG images | 97.16% |

### Notes on detection results
- Gamma compression follows the Adobe-98 standard.
- Binning window used is 30x30.
- An object is said to have been detected if the determined bounding box's overlap with the ground truth box is > 40%.
