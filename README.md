# GCP-Big-Data-ML
Notes for the Google Cloud Platform Big Data and Machine Learning Fundamentals course.

https://www.coursera.org/learn/gcp-big-data-ml-fundamentals/home/welcome

https://console.cloud.google.com

## 1. Google Cloud Architecture

    -----------------------------------------
            2. Big Data/ML Products
    -----------------------------------------
     1. Compute Power | Storage | Networking
    -----------------------------------------
               0. Security
    -----------------------------------------


-2. Abstract away scaling, infrastructure

-1. Process, store, and deliver pipelines, ML models, etc.

-0. Auth

## 2. Creating a VM on Compute Engine

### 2.1 Setting up the VM

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

### 2.2 Sample earthquake data

After installing git, we can pull down the data from our repo:

`git clone https://www.github.com/GoogleCloudPlatform/training-data-analyst`

Course materials are in:

`training-data-analyst/courses/bdml_fundamentals`

Go to the Earthquake sample in `earthquakevm`.

The `ingest.sh` shell script contains the script to ingest data (`less ingest.sh`). This script basically just deletes existing data and then `wget`s a new CSV file containing the data.

Now, `transform.py` contains a Python script to parse the CSV file and create a PNG from it using `matplotlib` (
[matplotlib notes](https://nbviewer.jupyter.org/github/pekoto/MyJupyterNotes/blob/master/Python%20for%20Data%20Analysis.ipynb)).

([File details](https://github.com/GoogleCloudPlatform/datalab-samples/blob/master/basemap/earthquakes.ipynb))

Run `./install_missing.sh` to get the missing Python libraries, and run the scripts mentioned above to get the CSV and generate the image.

### 2.3 Transferring the data to bucket storage

Now, since we have generated the image. Let's get it off the VM and delete the VM.

To do this, we need to create some storage:
Storage > Storage > Browser > Create Bucket

Now, to view our bucket, we can use:

`gsutil ls gs://[bucketname]` (hence why bucket names need to be globally unique)

To copy out data to the bucket, we can use:

`gsutil cp earthquakes.* gs://[bucketname]`

### 2.4 Stopping/deleting the VM

So now we're finished with our VM, we can either:

__STOP__
Stop the machine. You will still pay for the disk, but not the processing power.

__DELETE__
Delete the machine. You won't pay for anything, but obviously you will lose all of the data.

### 2.5 Viewing the assets

Now, we want to make our assets in storage publically available.
To do this:
Select Files > Permissions > Add Members > `allUsers` > Grant `Storage Object Viewer` role.

Now, you can use the public link to [view your assets](https://storage.googleapis.com/earthquakeg/earthquakes.htm).
