# Detect Emotions in an Image with the Cognitive Services API 

## Overview

Azure Cognitive Services is a suite of APIs that allow you to take advantage of powerful Machine Learning algorithms without becoming an expert.

In this lab, we'll be using the Azure Cognitive Services [Face API](https://docs.microsoft.com/en-us/azure/cognitive-services/face/overview) and Python to predict which emotion a person is displaying in a particular photo. 

This lab will take approximately 5-10 minutes to complete, and requires only novice Python knowledge.

## Prerequisites

Using the Face API requires a key, which is provided later on in this lab.

To create a free key of your own, go to [https://portal.azure.com](https://portal.azure.com), select the Face API and follow the instructions to create your Face API key. Then use the endpoint and the key from the portal.

In the example below, we'll be using the `requests` library to make queries using a Jupyter Notebook.

## What's Covered in This Lab?

In this lab, you will:

* Select an image with a face
* Send the selected image's URL to the Face API
* Parse the JSON response to get the predicted emotion of the face(s) in the image

## Part A: Set Up

Let's start by creating a new Jupyter Notebook. 

Press start or click on the bottom left area 'Type here to search', then search for "Notebook" and select `Jupyter Notebook`. Once the notebook is open, select `New -> Notebook: Python 3 ` from the top right-hand side of the window. 

!IMAGE[Create Jupyter Notebook](images/create-notebook.png)

Next, enter the following code into the notebook, and select 'Run' from the toolbar or use the keyboard shortcut `shift + enter`

!IMAGE[Run Jupyter Notebook](images/run-notebook.png)

Note that we'll be following the same format throughout this lab. Paste in the sample code, then run it. 

If you created your own key for the API, update `api_key` and `api_url` with the values from the Azure Portal.

```python
import requests

api_key = 'YOUR_API_KEY'
api_url = 'https://eastus2.api.cognitive.microsoft.com/face/v1.0'  # or your region, if different.
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

Now we'll need to do a bit of configuration before we call the endpoint. This API key is passed in with the headers, and then we will enumerate which attributes we want returned with the `returnFaceAttributes` property.

```python
headers = {'Ocp-Apim-Subscription-Key': '72f5dda62fd74d11a842f33f730702a6'}
params = {'returnFaceAttributes': 'emotion'}
```

In this example, we're only interested in the `emotion` property, but there are lots of other attributes available. Such as: `age`, `gender`, `headPose`, `smile`, `facialHair`, `glasses`, `hair`, `makeup`, `occlusion`, `accessories`, `blur`, `exposure`, `noise`

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
print('Found {} faces in the photo.'.format(len(faces)))
response.json()
```

The response is a list of dictionaries, containing a record for each unique face. It contains information such as an ID for the face we've identified, and the bounding rectangle coordinates for the face in the image we provided. 

The data we're looking for is under the key of `faceAttribute -> emotion`. The API returns the probability that the face in the image is displaying a particular emotion. The emotion with the highest probability will have the value closest to 1, meaning to get the dominant emotion we'll need to retrieve the key with the highest value.

Let's try it!

```python
for index, face in enumerate(faces):
   detected_emotions = face['faceAttributes']['emotion']
   dominant_emotion = max(detected_emotions, key=detected_emotions.get)
   print('Face #{} has the dominant emotion of {}'.format(index, dominant_emotion))
```

## Conclusion

That's it! We've learned how fast and easy it is to classify an image by emotion. 
This lab covered just one facet of the Cognitive Services API. If you'd try more Cognitive Services, feel free to play with the demos at https://aidemos.microsoft.com/ to see what else is possible with these services.