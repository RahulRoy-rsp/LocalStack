## S3 Bucket
- An Amazon S3 bucket is a public cloud storage resource available in Amazon Web Services (AWS) Simple Storage Service (S3) platform.
- It provides object-based storage, where data is stored inside S3 buckets in distinct units called objects instead of files.
- Amazon S3 buckets are similar to file folders and can be used to store, retrieve, back up and access objects.
- Each object has three main components -- the object's content or data, a unique identifier for the object and the descriptive metadata, including the object's name, URL and size.

---

### Creating an S3 Bucket using CLI

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url=<aws_url> s3api create-bucket --bucket <bucket-name>
  ```

#### Explanation of the Flags
  - **`aws`**: This is the AWS CLI command. The AWS CLI is a unified tool to manage your AWS services.
  - **`--profile <profile_name>`**: Specifies the profile to use for the command. Profiles are defined in the AWS CLI configuration file, allowing you to use different sets of credentials and configurations.
  - **`--endpoint-url <aws_url>`**: Specifies the endpoint URL to use for the service. This is useful when you're working with LocalStack or other custom endpoints.
  - **`s3api`**: Specifies that the command will interact with the Amazon S3 service using the low-level S3 API commands.
  - **`create-bucket`**: The action to be performed, in this case, creating a new S3 bucket.
  - **`--bucket <bucket-name>`**: Specifies the name of the bucket to create.
    
#### Example
  ```bash
  aws --profile localstack --endpoint-url=http://localhost:4566 s3api create-bucket --bucket test-bucket-1
  ```
  - Above command creates a bucket named **`test-bucket-1`**

---

### Listing the buckets available

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3api list-buckets
  ```

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3api list-buckets
  ```
  - Above command will list down the buckets available.

---

### Uploading an object in an S3 Bucket

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 cp <local_file_path> s3://<bucket-name>/<object-key> --content-type '<mime-type>'
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `<local_file_path>`: The path to the local file you want to upload.
  - `<bucket-name>`: The name of the S3 bucket.
  - `<object-key>`: The key (path) for the object in the S3 bucket.
  - `--content-type '<mime-type>'`: Specifies the MIME type of the file being uploaded.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 cp sample_files/sample1.csv s3://test-bucket-1/test-data/sample1.csv --content-type 'text/csv'
  ```
  - Above commands uploads a file named `sample1.csv` (in `sample_files` folder present in your working directory) into an S3 bucket named `test-bucket-1`.
  - If the folder `test-data` is not present in the bucket then it will be created and the file will be saved as `sample1.csv`   

---

### Downloading an object from an S3 Bucket

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 cp s3://<bucket-name>/<object-key> <local_file_path> --content-type '<mime-type>'
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `<bucket-name>`: The name of the S3 bucket.
  - `<object-key>`: The key (path) for the object in the S3 bucket.
  - `<local_file_path>`: The path where the downloaded file will be saved.
  - `--content-type '<mime-type>'`: Specifies the MIME type of the file being downloaded.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 cp s3://test-bucket-1/test-data/sample1.csv downloads/sample-downloaded.csv --content-type 'text/csv'
  ```
  - Above commands downloads a file named `sample1.csv` from an S3 path: `s3://test-bucket-1/test-data/`
  - It will be stored in your local's working directories folder name `downloads` and the file will be saved as `sample-downloaded.csv`   

---

### Listing the objects in the bucket

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 ls s3://<bucket-name>/
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `ls`: It is used for listing objects. 
  - `<bucket-name>`: The name of the S3 bucket.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 ls s3://test-bucket-1/
  ```
    
---

### Listing the objects in the bucket's folder

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 ls s3://<bucket-name>/<object-key>
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `ls`: It is used for listing objects. 
  - `<bucket-name>`: The name of the S3 bucket.
  - `<object-key>`: The key (path) for the object in the S3 bucket.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 ls s3://test-bucket-1/first-test/
  ```

    

### Listing the objects from the bucket within all sub-folders

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 ls s3://<bucket-name>/ --recursive
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `ls`: It is used for listing objects. 
  - `<bucket-name>`: The name of the S3 bucket.
  - `recursive`: It specifies to fetch each and every folders present in the bucket.
 
#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 ls s3://test-bucket-1/ --recursive
  ```

---

### Deleting an present in an S3 bucket's folder

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3 rm s3://<bucket-name>/<object-key>
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `ls`: It is used for listing objects. 
  - `<bucket-name>`: The name of the S3 bucket.
  - `recursive`: It specifies to fetch each and every folders present in the bucket.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3 rm s3://test-bucket-1/first-test/sample1.json
  ```

---

### Deleting the bucket

#### Syntax
  ```bash
  aws --profile <profile_name> --endpoint-url <aws_url> s3spi delete-bucket <bucket-name>
  ```

#### Explanation of the Flags
  - `<profile_name>`: The profile to use from the AWS CLI configuration.
  - `<aws_url>`: The endpoint URL for the AWS service (LocalStack in this case).
  - `ls`: It is used for listing objects. 
  - `<bucket-name>`: The name of the S3 bucket.
  - `recursive`: It specifies to fetch each and every folders present in the bucket.

#### Example
  ```bash
  aws --profile localstack --endpoint-url http://localhost:4566 s3api delete-bucket --bucket test-bucket-1
  ```

---
