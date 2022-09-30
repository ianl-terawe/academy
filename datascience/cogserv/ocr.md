# Read printed and handwritten text

Install the client library.

You can install the client library with:

```bash
pip install --upgrade azure-cognitiveservices-vision-computervision
```

Also install the Pillow library.

```bash
pip install pillow
```

Create a new Python application

Create a new Python `file—quickstart-file.py`, for example. Then open it in your preferred editor or IDE.

Find the key and endpoint from your Workspace. 

<!--- reword below --->

Go to the Azure portal. If the Computer Vision resource you created in the Prerequisites section deployed successfully, click the Go to Resource button under Next Steps. You can find your key and endpoint in the resource's key and endpoint page, under resource management.

Replace the contents of the `quickstart-file.py` with the following code:

```Python
from azure.cognitiveservices.vision.computervision import ComputerVisionClient
from azure.cognitiveservices.vision.computervision.models import OperationStatusCodes
from azure.cognitiveservices.vision.computervision.models import VisualFeatureTypes
from msrest.authentication import CognitiveServicesCredentials

from array import array
import os
from PIL import Image
import sys
import time

'''
Authenticate
Authenticates your credentials and creates a client.
'''
subscription_key = "PASTE_YOUR_COMPUTER_VISION_SUBSCRIPTION_KEY_HERE"
endpoint = "PASTE_YOUR_COMPUTER_VISION_ENDPOINT_HERE"

computervision_client = ComputerVisionClient(endpoint, CognitiveServicesCredentials(subscription_key))
'''
END - Authenticate
'''

'''
OCR: Read File using the Read API, extract text - remote
This example will extract text in an image, then print results, line by line.
This API call can also extract handwriting style text (not shown).
'''
print("===== Read File - remote =====")
# Get an image with text
read_image_url = "https://raw.githubusercontent.com/MicrosoftDocs/azure-docs/master/articles/cognitive-services/Computer-vision/Images/readsample.jpg"

# Call API with URL and raw response (allows you to get the operation location)
read_response = computervision_client.read(read_image_url,  raw=True)

# Get the operation location (URL with an ID at the end) from the response
read_operation_location = read_response.headers["Operation-Location"]
# Grab the ID from the URL
operation_id = read_operation_location.split("/")[-1]

# Call the "GET" API and wait for it to retrieve the results 
while True:
    read_result = computervision_client.get_read_result(operation_id)
    if read_result.status not in ['notStarted', 'running']:
        break
    time.sleep(1)

# Print the detected text, line by line
if read_result.status == OperationStatusCodes.succeeded:
    for text_result in read_result.analyze_result.read_results:
        for line in text_result.lines:
            print(line.text)
            print(line.bounding_box)
print()
'''
END - Read File - remote
'''

print("End of Computer Vision quickstart.")
```

Paste your key and endpoint into the code where indicated. Your Computer Vision endpoint has the form `https://<your_computer_vision_resource_name>.cognitiveservices.azure.com/`.

As an optional step, see How to specify the model version. For example, to explicitly specify the latest GA model, edit the read statement as shown. Skipping the parameter or using "latest" automatically uses the most recent GA model.

```bash
   # Call API with URL and raw response (allows you to get the operation location)
   read_response = computervision_client.read(read_image_url,  raw=True, model_version="2022-04-30")
```

Run the application with the python command on your quickstart file.

`python quickstart-file.py`

An example of the output to exopect:

```T
===== Read File - remote =====
The quick brown fox jumps
[38.0, 650.0, 2572.0, 699.0, 2570.0, 854.0, 37.0, 815.0]
Over
[184.0, 1053.0, 508.0, 1044.0, 510.0, 1123.0, 184.0, 1128.0]
the lazy dog!
[639.0, 1011.0, 1976.0, 1026.0, 1974.0, 1158.0, 637.0, 1141.0]

End of Computer Vision quickstart.
```