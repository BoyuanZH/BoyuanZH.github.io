---
layout:     post
title:      "Setup XGBoost-friendly Environment on Cloud Computing Instance"
subtitle:   "AWS and GCP."
date:       2017-09-01
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - Machine Learning
    - Cloud Computing
    - Study Notes
---

>This post was written when I was dealing with kaggle competition [NY Taxi Trip Duration](https://www.kaggle.com/c/nyc-taxi-trip-duration).

Traing XGBoost can be time-consuming especially when your are tuning the hyper-parameters using cross validation, since multiple experiments are required. 

Unlike NeuroNet, which can be speed up efficiently using GPU, XGBoost training on GPU is still not very optimistic. 

However, it still can be useful if you can utilize the compute engines with higher confirmation, which are provided by cloud computing services, like Google Cloud Platform (GCP) and Amazon Web Service (AWS).

I built XGBoost-friendly environment on both GCP and AWS instances and report the steps below.

#### Step 1. Create a new instance.
Operating System: Linux. (Debian/Ubuntu)

Other configuration depends on tasks.

#### Step 2. Connect to the instance.

###### Option : Connect AWS Instance

AWS I choose to connect the instance through my mac terminal ssh.

```
chmod 400 /path/my-key-pair.pem
ssh -i /path/my-key-pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com -o StrictHostKeyChecking=no
```
> `ec2-user` may be replaced by your user tag.
> 
> `/path/my-key-pair.pem` is the path where you store the key pair.
> 
> `-o StrictHostKeyChecking=no` is for host-authentification.

###### Option : Connect GCP Instance

GCP provides ssh connectiong through browser, which is super easy to access.

#### Step 3. Install required packages.

Packages include git, numpy, pandas, scipy, xgboost, etc..
For convinience I just write down the bash script here.

```
#!/bin/bash
echo "This is a shell script for setting up a remote compute engine- debian"
sudo apt-get install git python python-setuptools
sudo easy_install pip
sudo apt-get install python-dev python-numpy python-scipy python-matplotlib python-pandas
sudo pip install --upgrade pandas sklearn
sudo pip install seaborn
sudo apt-get install g++ gfortran
sudo apt-get install libatlas-base-dev
sudo apt-get install make
echo "Python and packages needed for xgboost are installed"

# setup xgboost
git clone --recursive https://github.com/dmlc/xgboost.git
cd xgboost
make
cd python-package/
sudo python setup.py install

```

#### Step 4. Upload dataset

In my practice, I upload the dataset onto GCP storage bucket.

This can be convenient if you are using GCP instance, just use `gsutil` to download from your bucket, for example:

```
gsutil ls gs://my-awesome-bucket/*
gsutil cp gs://my-awesome-bucket/cloud-storage-logo.png Desktop
### copy folders
gsutil cp -r gs://my-awesome-bucket/cloud-storage-logo.png Desktop
```

On AWS instance, just use `wget` to download from the link:

> first make sure tour bucket is publicly available.

```
wget http://blablabla.cvs
```

