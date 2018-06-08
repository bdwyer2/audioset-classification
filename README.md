# Audio Classification using Keras and Jupyter Notebooks

In this developer code pattern, we first create a Deep Learning model to classify audio embeddings. We train the model on IBM Deep Learning as a Service (DLaaS) platform and then perform inference/evaluation on IBM Watson Studio. 

The model will use audio embeddings generated by the VGG-ish model as an input and generate output probabilities/scores for 527 classes. For the purposes of illustrating the concept and exposing a developer to the features on IBM Cloud platforms, we use Google's Audioset data where the embeddings have been pre-processed and available readily.  However, a developer can leverage this model to create their own custom audio classifier trained on their own audio embeddings/data.

When the reader has completed this Code Pattern, they will understand how to:

* Setup an IBM Cloud object storage bucket and upload the training data to the cloud.
* Upload a Deep Learning model to IBM DLaaS for training.
* Integrate the object storage buckets into IBM Watson Studio.
* Perform inference on an evaluation dataset using Jupyter Notebooks over IBM Watson Studio.

## Flow

## Included Components
* [IBM Cloud Object Storage](https://www.ibm.com/cloud/): insert description here
* [IBM Deep Learning as a Service](https://www.ibm.com/cloud/): insert description here
* [Watson Studio](https://www.ibm.com/cloud/watson-studio): insert description here 
* [Jupyter Notebooks](http://jupyter.org/): An open source web application that allows you to create and share documents that contain live code, equations, visualizations, and explanatory text.
* [Keras](https://keras.io/): The Python Deep Learning library.
* [Tensorflow](https://www.tensorflow.org/): An open-source software library for Machine Intelligence.

## Featured Technologies

* [Cloud](https://www.ibm.com/developerworks/learn/cloud/): Accessing computer and information technology resources through the Internet.
* [Data Science](https://medium.com/ibm-data-science-experience/): Systems and scientific methods to analyze structured and unstructured data in order to extract knowledge and insights.
* [Artificial Intelligence](https://www.ibm.com/developerworks/learn/cognitive/index.html):Artificial intelligence can be applied to disparate solution spaces to deliver disruptive technologies.
* [Python](https://www.python.org/): Python is a programming language that lets you work more quickly and integrate your systems more effectively.

# Prerequisites

1. Setup cloud object storage and AWS command line tools.
2. Create accounts on IBM Cloud and Watson Studio.


### Setup an IBM Cloud Object Storage (COS) account
- Create an IBM Cloud Object Storage account if you don't have one (https://www.ibm.com/cloud/storage)
- Create credentials for either reading and writing or just reading
	- From the bluemix console page (https://console.bluemix.net/dashboard/apps/), choose `Cloud Object Storage`
	- On the left side, click the `service credentials`
	- Click on the `new credentials` button to create new credentials
	- In the `Add New Credentials` popup, use this parameter `{"HMAC":true}` in the `Add Inline Configuration...`
	- When you create the credentials, copy the `access_key_id` and `secret_access_key` values.
	- Make a note of the endpoint url
		- On the left side of the window, click on `Endpoint`
		- Copy the relevant public or private endpoint. [I choose the us-geo private endpoint].
- In addition setup your [AWS S3 command line](https://aws.amazon.com/cli/) which can be used to create buckets and/or add files to COS.
   - Export `AWS_ACCESS_KEY_ID` with your COS `access_key_id` and `AWS_SECRET_ACCESS_KEY` with your COS `secret_access_key`

### Setup IBM CLI & ML CLI

- Install [IBM Cloud CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started)
  - Login using `bx login` or `bx login --sso` if within IBM
- Install [ML CLI Plugin](https://dataplatform.ibm.com/docs/content/analyze-data/ml_dlaas_environment.html)
  - After install, check if there is any plugins that need update
    - `bx plugin update`
  - Make sure to setup the various environment variables correctly:
    - `ML_INSTANCE`, `ML_USERNAME`, `ML_PASSWORD`, `ML_ENV`

# Steps

The steps can be broadly classified into the following topics:

1. Clone the repository.
2. Upload training data to cloud object storage.
3. Setup and upload model on DLaaS to train.
4. Upload evaluation notebook to Watson Studio.
5. Run evaluation on Watson Studio.

Note: If you want to perform inference with pre-trained weights, skip to step 4 directly. 

## 1. Clone the repository

Clone this repository and change into the new directory:

```
$ git clone https://github.com/IBM/audioset-classification
$ cd audioset-classification
```

A few things to mention about the contents of the repository:

* [audio_classify.zip](audioset_classify.zip): This is the core training code we will be running on IBM Cloud. 
* [audioset_classify](audioset_classify/): The training code for reference. We will use the first .zip file to upload this code to the cloud.
* [training-runs.yml](training-runs.yml) This file is required to perform the training on IBM cloud. It is used to setup training metdata and connection information.
* [audioclassify_inference.ipynb](audioclassify_inference.ipynb) This is the notebook we will be using to perform inference after training. 

## 2. Upload training data to the cloud






