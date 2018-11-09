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

### Set sewrvice account
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

### Vision API
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


