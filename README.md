
# AWS Lambda Function Image Uplaod to S3 Bucket by Python : 

### Step 1:  Import Lib to Lambda Function json, boto3,base64,uuid

```
import json,boto3
from botocore.client import Config
import base64
import uuid

```

### Step 2 : create s3 instance of boto3 client

```
s3 = boto3.client("s3")

```

### Step 3 : Get base64 encoded image and convert to byte

```
image_64_encode = b"/9j/4AAQSkZJRgABAQEBLAEsAAD/4QGARXhpZgAAS"
```

### Step 4: Decode image from encoded data

```
image_64_decode = base64.decodebytes(image_64_encode)

```

### Step 5: Set AWS Access and Secret key to boto3 resource

```
s3 = boto3.resource(
    's3',
    aws_access_key_id="ENTER_AWS_ACCESS_KEY",
    aws_secret_access_key="ENTER_AWS_SECRET_KEY",
    config=Config(signature_version="s3v4")
)

```

### Step 6: Full Example of file upload see lambda_function.py



```
s3 = boto3.client("s3")
image_64_encode = b"/9j/4AAQSkZJRgABAQEBLAEsAAD/4QGARXhp"

image_64_decode = base64.decodebytes(image_64_encode)

file_type = ".jpg"
file_uuid = uuid.uuid4().hex
filename = file_uuid + file_type
BUCKET_NAME = "eatz-lib"

s3 = boto3.resource(
    's3',
    aws_access_key_id="ENTER_AWS_ACCESS_KEY",
    aws_secret_access_key="ENTER_AWS_SECRET_KEY",
    config=Config(signature_version="s3v4")
)
s3.Bucket(BUCKET_NAME).put_object(Key=filename, Body=image_64_decode)

```




