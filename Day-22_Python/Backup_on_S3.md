# Created python script to backup on S3 bucket using Boto3 module

## 1. Created script to create S3 bucket
```
"""
This is a script to take backup from local to AWS S3
boto3:- Used to perform AWS tasks using python
"""

import boto3

s3 = boto3.resource("s3")

def show_buckets(s3): # Define the function
    for bucket in s3.buckets.all(): # Iterate the list
        print(bucket.name)

def create_bucket(s3): 
    s3.create_bucket(Bucket="amir-with-python",
                     CreateBucketConfiguration={
                         'LocationConstraint': 'ap-south-1',
                     },)
    print("Bucket created successfully")

# Call the function
#show_buckets(s3)
create_bucket(s3)

```
<img width="1273" height="714" alt="image" src="https://github.com/user-attachments/assets/e7f0c29f-2334-4f69-9d0e-0409040359b6" />
<img width="1227" height="380" alt="image" src="https://github.com/user-attachments/assets/d7f86b17-1384-4cce-a95b-d311777f5775" />


------

## 2. Created script to upload the file
```
"""
This is a script to take backup from local to AWS S3
boto3:- Used to perform AWS tasks using python
"""

import boto3

s3 = boto3.resource("s3")

def show_buckets(s3): # Define the function
    for bucket in s3.buckets.all(): # Iterate the list
        print(bucket.name)

def create_bucket(s3,bucket_name,region): 
    s3.create_bucket(Bucket=bucket_name,
                     CreateBucketConfiguration={
                         'LocationConstraint': region,
                     },)
    print("Bucket created successfully")

def upload_backup(s3,file_name,bucket_name,key_name): # Define the function

    data = open (file_name, 'rb') # Will read in binary before uploading
    s3.Bucket(bucket_name).put_object(Key=key_name, Body=data)
    print("Backup Uploaded Successfully")


bucket_name = "amir-with-python"
region = "ap-south-1"

# Call the function
#show_buckets(s3)
#create_bucket(s3)
file_name = r"C:\Users\111685\OneDrive - Arrow Electronics, Inc\Study Material\Devops Study\Python\backup\backup_2025-11-26..zip"
upload_backup(s3,file_name,bucket_name,"my-backup.zip")
```

<img width="1215" height="912" alt="image" src="https://github.com/user-attachments/assets/8c372f8b-2428-4f8c-a8c2-2d89703ff243" />

