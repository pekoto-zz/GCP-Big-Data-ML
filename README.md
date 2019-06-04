# GCP-Big-Data-ML
Notes for the Google Cloud Platform Big Data and Machine Learning Fundamentals course.

https://www.coursera.org/learn/gcp-big-data-ml-fundamentals/home/welcome

## 1. Google Cloud Architecture

    -----------------------------------------
            2. Big Data/ML Products
    -----------------------------------------
     1. Compute Power | Storage | Networking
    -----------------------------------------
               0. Security
    -----------------------------------------

                
0. Auth
1. Process, store, and deliver pipelines, ML models, etc.
2. Abstract away scaling, infrastructure

## 2. Creating a VM on Compute Engine

1. https://cloud.google.com
2. Compute --> Compute Engine --> VM Instances
3. Create a new VM
3.1 Allow full access to cloud APIs
3.2 Since we will access the VM through SSH, we don't need to allow HTTP or HTTPS traffic
4. Click SSH to connect

At this stage, the new VM has no software.

We can just install stuff like normal:

`sudo apt-get install git`

(APT: advanced package tool, package manager)

After installing git, we can pull down the data from our repo:

`git clone https://www.github.com/GoogleCloudPlatform/training-data-analyst`

Course materials are in:

`training-data-analyst/courses/bdml_fundamentals`

Go to the Earthquake sample in `earthquakevm`.

The `ingest.sh` shell script contains the script to ingest data (`less ingest.sh`). This script basically just deletes existing data and then `wget`s a new CSV file containing the data.

Now, `transform.py` contains a Python script to parse the CSV file and create a PNG from it using `matplotlib` (
[matplotlib notes](https://nbviewer.jupyter.org/github/pekoto/MyJupyterNotes/blob/master/Python%20for%20Data%20Analysis.ipynb)).
