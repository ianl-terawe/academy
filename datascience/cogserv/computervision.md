# Computer Vision 

## Object Detection and Classification 

To illustrate the challenge of computer vision, consider the image presented below from [this source](https://cloudblogs.microsoft.com/industry-blog/en-gb/health/2019/07/26/ai-medical-imaging-low-code/). Most would immediately recognize this as an ultrasound image (i.e., a sonogram ) of a human fetus in the womb. Whereas this is ‘obvious’ to humans, a combination of object detection and classification is required for this assessment to be made explicit via computer vision. From the right-side of the figure, it is evident that Azure Computer Vision has indeed identified the image as a medical one, and more specifically a sonogram. Through use of tags, additional details regarding detected objects are provided. In this case, for example, the additional detail conveyed via tags is quite impressive overall. As the confidence levels indicate,  there exists a 0.68 indication that the image is an X-ray – even though humans know this is clearly a sonogram. Clearly, there is room for improvement. 

![object detection and classification example](/datascience/cogserv/media/us_object_classification.png "object detection and classification example")

As the snippet of Python code below illustrates, it is merely the application of the `tag_image` method from the `computervision_client` object to the image URL of interest that is required to produce tags along the lines of those presented in the figure. 

```Python
'''
Tag an Image - remote
This example returns a tag (key word) for each thing in the image.
'''
print("===== Tag an image - remote =====")
# Call API with remote image
tags_result_remote = computervision_client.tag_image(remote_image_url )

# Print results with confidence score
print("Tags in the remote image: ")
if (len(tags_result_remote.tags) == 0):
    print("No tags detected.")
else:
    for tag in tags_result_remote.tags:
        print("'{}' with confidence {:.2f}%".format(tag.name, tag.confidence * 100))

```

Analogous application of prebuilt methods allows for the detection of objects, description of the image, and much more. Of course, use of such methods is enabled by importing Python modules; in this case, for computer vision:

```Python
from azure.cognitiveservices.vision.computervision import ComputerVisionClient
```

Python source code for this example can be found [here](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ComputerVision/ComputerVisionQuickstart.py) via GitHub. In addition to Python, Software Development Kits (SDKs) are available for Go, Java, .NET and Node.js.

## Limitations of General-Purpose Approaches

The above characterization is far from perfect. As a general-purpose service able to identify more than 10,000 objects, Azure Computer Vision provides a vantage point from which the journey towards medical imaging intelligence can be easily initiated with minimal effort. This applies more broadly to object detection and classification in general. 

## Segmenting Images 

To appreciate the challenge of segmenting medical images, consider the example of the brain tumor imaged via MRI in the figure below from [this source](http://emedicine.medscape.com/article/283252-overview). Using an acquisition mode (namely T1-weighted axial gadolinium, T1-gad) that serves to enhance its presence (in the upper left of the figure), a radiologist would report consistency with a developing glioblastoma multiforme (GBM) tumor in this MRI image. Using their expertise, the radiologist would characterize the tumor relative to the rest of the tissue in the brain – e.g., from a morphological perspective that places emphasis on the form of the tumor. By identifying the active rim of the GBM tumor, the first degree of segmentation is achieved – i.e., segmenting the region containing the tumor from the rest of the healthy brain. 

![image segementation example](https://raw.githubusercontent.com/ianl-terawe/academy/main/datascience/cogserv/media/mri_image_segmn.png "image segementation example")

To segment the tumor from the rest of the brain, classification needs to operate at the most granular of levels – namely that of the individual voxels that collectively comprise the MRI image. Whereas two-dimensional imagery may suffice some medical purposes (e.g., pregnancy assessments via ultrasound), locating GBM tumors in three dimensions demands that pixels be generalized to voxels – i.e., elements that represent an imaged volume in a spatial representation, as opposed to an area. Thus, the decidedly 3D human brain, is imaged via a collection of two-dimensional slices capable of dereferencing the third dimension. 

To codify the radiologist’s procedure then, the first degree of segmentation addresses the location of a voxel as being within or without the active rim of a GBM tumor.  Because ‘edge detection’ remains somewhat subjective, the ‘threshold value’ (τ) for voxels that delineate the active rim on a T1-gad mode MRI image are established by the radiologist during diagnosis. Segmentation to the first degree is captured through the ‘manual’ algorithm below: 

```bash
if T1gad ( v ) > τ
   then v is in active rim
   else v is not in active rim
```

Written in pseudocode, algorithms such as this establish the path forward from the perspective of image segmentation. In a second phase of segmentation, imagery derived from two additional acquisition modes is employed to further segment voxels that characterize the normal tissue (background), the active rim, from injured tissue. This is captured in the pseudocode below: 

```bash
if T1gad ( v ) > τ1
   if T1 ( v ) < τ2
      then v is in active rim
      else v is in background
   else FLAIR ( v ) > τ3
      then v is in necrotic core
      else v is in background
```

Thus, images can be systamtically segmented to the degree necessary. Ultimately, computers are able to 'see' the details _within_ images - just as humans do. 

<!--- could elaborate --->