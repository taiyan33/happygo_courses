# happygo_courses
Materials and scripts for Happygo courses.

  ```
  └─happygo_courses
    │
    ├─ml_api_intro
    │      data
    │      xxx.py
    │      course.pdf
    │
    └─automl_intro
           data
           xxx.py
           course.pdf

  ```

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
curl 
https://raw.githubusercontent.com/GoogleCloudPlatform/python-
docs-samples/master/vision/cloud-client/detect/detect.py -o vision.py
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
curl 
https://raw.githubusercontent.com/GoogleCloudPlatform/python-
docs-samples/master/speech/cloud-client/transcribe.py -o speech2text.py
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
curl 
https://raw.githubusercontent.com/GoogleCloudPlatform/python-
docs-samples/master/translate/cloud-client/snippets.py -o translate.py
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









