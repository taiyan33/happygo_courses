# happygo_courses
Materials and scripts for Happygo courses.

## Integrating Machine Learning APIs

List the authenticated and active account:
```
gcloud auth list
```
List the current project id:
```
gcloud config list project
```

### Service Account

1. Create service-account
```
gcloud iam service-accounts create NAME
```
2. Generate and download service-account key
```
gcloud iam service-accounts keys create FILE_NAME.json --iam-account NAME@PROJECT_ID.iam.gserviceaccount.com
```


### Set service account
1. Print current directory
```
pwd
```
2. Set environment variable (temporary)
```
export GOOGLE_APPLICATION_CREDENTIALS=PATH_TO_FILE/FILE_NAME.json
```
3. Set environment variable (permanent)
```
Vim ~/.bashrc
```
```
export GOOGLE_APPLICATION_CREDENTIALS=PATH_TO_FILE/FILE_NAME.json
```
4. Check environment variable
```
echo $GOOGLE_APPLICATION_CREDENTIALS
```


### Cloud Vision API
1. Install Python client for Cloud Vision
```
pip install --upgrade google-cloud-vision --user
```
2. Download code sample detect.py 
```
curl https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/vision/cloud-client/detect/detect.py -o vision.py
```
3. Use the API to get labels
```
python vision.py labels-uri gs://ml-api-codelab/birds.jpg
```

The image analyzed is [here](https://storage.googleapis.com/ml-api-codelab/birds.jpg). 


### Cloud Speech API
1. Install Python client for Cloud Speech-to-Text
```
pip install --upgrade google-cloud-speech
```
2. Download code sample transcribe.py
```
curl https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/speech/cloud-client/transcribe.py -o speech2text.py
```
3. Use the API to get labels
```
python speech2text.py gs://ml-api-codelab/tr-ostrich.wav
```

The audio file analyzed is [here](https://storage.googleapis.com/ml-api-codelab/tr-ostrich.wav). 


#### Error!

google.api_core.exceptions.InvalidArgument: 400 sample_rate_hertz (16000) in RecognitionConfig must either be omitted or match the value in the WAV header ( 22050).

1. Open speech2text.py 
2. Go to tanscribe_gcs()
3. Delete encoding and sample_hertz_rate from RecognitionConfig()
4. Change the language code to ’tr-TR’
```
config = types.RecognitionConfig(language_code='tr-TR')
```


### Cloud Translation API
1. Install Python client for Cloud Translation
```
pip install --upgrade google-cloud-translate
```
2. Download code sample snippets.py 
```
curl https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/translate/cloud-client/snippets.py -o translate.py
```
3. Use the API to get labels
```
python translate.py translate-text en '你有沒有帶外套'
```

The translation should be "Do you have a jacket?".


### Cloud Natural Language
1. Install Python client for Cloud Translation
```
pip install --upgrade google-cloud-language
```
2. Download code sample snippets.py 
```
curl https://raw.githubusercontent.com/GoogleCloudPlatform/python-docs-samples/master/language/cloud-client/v1/snippets.py -o natural_language.py
```
3. Use the API to get labels
```
python natural_language.py entities-text 'where did you leave my bike'
```

The API should identify "bike" as an entity.


### Cloud Video Intelligence 

#### Service Account

1. Create service-account
```
gcloud iam service-accounts create NAME
```
2. Generate and download service-account key
```
gcloud iam service-accounts keys create FILE_NAME.json --iam-account NAME@PROJECT_ID.iam.gserviceaccount.com
```

#### Set up authorization

1. Authenticate your service account
```
gcloud auth activate-service-account --key-file FILE_NAME.json
```
2. Obtain an authorization token key
```
gcloud auth print-access-token
```

#### Create a request file

Use the editor of your choice (nano, vi, etc.) to create a JSON request file.
```
{
   "inputUri":"gs://cloud-ml-sandbox/video/chicago.mp4",
   "features": [
       "LABEL_DETECTION"
   ]
}
```
#### Make an annotate video request

1. Use curl to make a videos:annotate request
2. Replace the ACCESS_TOKEN
```
curl -s -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer ACCESS_TOKEN' \
    'https://videointelligence.googleapis.com/v1/videos:annotate' \
    -d @request.json
```

Output:
```
{  
  "name": "asia-east1.4977238832208428291"
}
```
#### Make an annotate video request

1. Replace the ACCESS_TOKEN
2. Replace the OPERATION_NAME with the name you just received.
```
curl -s -H 'Content-Type: application/json' \
    -H 'Authorization: Bearer ACCESS_TOKEN' \
    'https://videointelligence.googleapis.com/v1/operations/OPERATION_NAME'
```

#### Try another video...

Use the editor of your choice (nano, vi, etc.) to edit the JSON file.
```
{
   "inputUri":"gs://demomaker/cat.mp4",
   "features": [
       "LABEL_DETECTION"
   ]
}
```

## AutoML Vision
1. Enable the AutoML API.
2. Setting up Google Cloud project

#### Prepare training data

1. Create an environment variable with the name of your bucket
```
export BUCKET=YOUR_BUCKET_NAME
```
2. Use gsutil  to copy the training images into your bucket
```
gsutil -m cp -r gs://automl-codelab-clouds/* gs://${BUCKET}
```

#### Create dataset

1. Copy the file to your Cloud Shell instance
```
gsutil cp gs://automl-codelab-metadata/data.csv .
```
2. Update the CSV with the files in your project
```
sed -i -e "s/placeholder/${BUCKET}/g" ./data.csv
```
3. Upload this file to your Cloud Storage bucket
```
gsutil cp ./data.csv gs://${BUCKET}
```
4. Create dataset on AutoML UI.

#### Predict

Use the images in /vision_test_images/ to test your model.



## AutoML NLP

1. Create GCS bucket.
```
gsutil mb -p PROJECT_ID \
	-c regional	\
	-l us-central1	\
	gs://$PROJECT_ID-lcm/
```
2. Create an environment variable with the name of your bucket
```
export BUCKET=YOUR_BUCKET_NAME
```
3. Use gsutil to copy the training data into your bucket
```
gsutil -m cp gs://cloudmile-demo-lcm/happiness.csv gs://${BUCKET}
```
4. Create dataset through Web UI (Select file gs://$BUCKET-lcm/happiness.csv)

5. Start training

6. Test your model with the following text:
'A strong taste of hazelnut and orange.'








