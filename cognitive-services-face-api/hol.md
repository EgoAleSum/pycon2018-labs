# Detect Emotions in an Image with the Cognitive Services API 

## Overview

Cognitive Service is a suite of APIs that allow you to take advantage of powerful algorithms to help you interpret and analyze graphics, text, and much more. 

In this lab, we'll be using the Azure Cognitive Services Face API and Python to determine which emotion a person is likely displaying in a particular photo. 

This lab will take approximately 5-10 minutes to complete, and requires only novice python knowledge.

You can try it on a photo of yourself or use any photo from the internet by providing the URL.

## Prerequisites

You'll need an API Key for the Face API. In this lab one is provided for you, but if you'd like to take the API for a spin at home, it's easy to get a free API key.

In the example below, we'll be using the `requests` library to make queries using a jupyter notebook, but you can just as easily run the example in a Python REPL. As an alternative, the Microsoft Face API also has a handy Python SDK that can be installed with `pip install cognitive_face`


## What's Covered in This Lab?

In this lab, you will:

* Select an image to use with the Face API
* Make a query to the API, providing the image
* Get the results of the query back in JSON format, showing which emotion is likely displayed in the image

## Part A: Set Up

Let's start by creating a new jupyter notebook. 

In windows, press start, then search for "Notebook". Once the notebook is open, select `New -> Python 3 Notebook` from the top right-hand side of the window. 

!IMAGE[Create Jupyter Notebook](images/create-notebook.png)

Next, enter the following code into the notebook, and select 'Run' from the toolbar.

!IMAGE[Run Jupyter Notebook](images/run-notebook.png)

Note that we'll be following the same format throughout this lab. Paste in the sample code, then run it. 

```python
import requests

api_key = 'YOUR_API_KEY'
api_url = 'https://westcentralus.api.cognitive.microsoft.com/face/v1.0'  # or your region, if different.
face_detect_endpoint_url = api_url + '/detect'
```

Next, let's select an image to run the face detection algorithm on. You can use an image of your own by providing the URL, or you can use one of the sample images included in the demo at the URLs below.

The sample images look like this:

| !IMAGE[Happy](images/happy.jpg) | !IMAGE[Surprised](images/surprised.jpg) | !IMAGE[Sad](images/sad.jpg) |
|:----------------------------------------------|:--------------------------------------------------|:--------------------------------------------|


```python
sad_image_url = 'https://i.imgur.com/RLSN9rx.jpg'
surprised_image_url = 'https://i.imgur.com/vEuLg5n.jpg'
happy_image_url = 'https://i.imgur.com/aegNK4W.jpg'

# specify your own image as image_url or use one of the sample images provided above
image_url = happy_image_url
```

In this code, we've specified our API Key, the API URL for the region we'll be using, the specific endpoint we want to hit (detect), and the URL of the image we want to run the detection algorithm on. 

## Part B: Configuration

Now we'll need to do a bit of configuration before we call the endpoint. The API key is passed in with the headers, and we're enumerating which attributes we want returned with the `returnFaceAttributes` property.

```python
headers = {
    'Ocp-Apim-Subscription-Key': 'b4a362ad13f74ef3b5befaa7561a068a'
}
params = {
    'returnFaceAttributes': 'emotion'
}
```
In this example, we're only interested in the `emotion` property, but there are lots of other attributes available. Such as: `age, gender, headPose, smile, facialHair, glasses, emotion, hair, makeup, occlusion, accessories, blur, exposure, noise`

To use them, you'd append these attributes as coma separated values to the `returnFaceAttributes` parameter.

## Part C: Make the Request

Now we have enough information to call the API and save the response JSON to an attribute named `faces`

```python
response = requests.post(face_detect_endpoint_url, params=params, headers=headers, json={'url': image_url})
faces = response.json()
```

## Part D: Examine the Response

Let's examine the JSON response.

```python
from pprint import pprint
print('Found {} faces in the photo.'.format(len(faces)))
pprint(response.json())
```

The response is a list of dictionaries, containing a record for each unique face. It contains information such as an ID for the face we've identified, and the bounding rectangle coordinates for the face in the image we provided. 

The data we're looking for is under the key of `faceAttribute -> emotion`. The API returns the likelihood of the image being classified as one of several emotions. The probabilities sum to 1, meaning to get the dominant emotion we'll need to retrieve the key with the highest value.

Let's try it!

```python
for index, face in enumerate(faces):
   detected_emotions = face['faceAttributes']['emotion']
   dominant_emotion = max(detected_emotions, key=detected_emotions.get)
   print('Face #{} has the dominant emotion of {}'.format(index, dominant_emotion))
```

## Conclusion

That's it! We've learned how fast and easy it is to classify an image by emotion. 
This lab covered just one facet of the Cognitive Services API. If you'd like to see more, try the other lab that showcases the text features of the Cognitive Services API.