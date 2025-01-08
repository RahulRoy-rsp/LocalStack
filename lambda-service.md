# AWS Lambda

---

### Steps for creating a lambda function

1. Create the python file in your working directory
2. Create the zip file out of the python file
3. Run the command for creating the lambda function.
4. Invoke the lambda function using a command.

### Demo Lambda Function creation
1. Create a folder `lambda-in-localstack` in your system.
2. Create a sample python file named `sample-lambda-function`
    ```python
    def lambda_handler(event, context):
        try:
            print("Lambda Function invoked.")
            return {
                'statusCode': 200,
                'body': 'Lambda function using localstack'
            }
        except Exception as e:
            return e
    ```
3. Create a zip file from the python file, you can create it using **PowerShell**
  - Open  Powershell and go to the directory where the python file is stored.
  - **General Syntax**:
    ```bash
    Compress-Archive -Path <the-source-python-file-path> -DestinationPath <zip-file-path>/<function-name>.zip
    ```
  - **As per our demo**:
    ```bash
    Compress-Archive -Path sample-lambda-function.py -DestinationPath lambda_handler.zip
    ```
4. Create the lambda function in LocalStack's AWS Console
  - **General Syntax**:
    ```bash
    aws --profile localstack --endpoint-url=<localstack's-url> lambda create-function --function-name <function-name> --runtime <python-version> --role arn:aws:iam::000000000000:role/irrelevant --handler <py-file-name>.<zip-folder-name> --zip-file fileb://<zip-file>
    ```
  - **As per our demo**:
    ```bash
    aws --profile localstack --endpoint-url=http://localhost:4566 lambda create-function --function-name test-lambda-function-1 --runtime python3.8 --role arn:aws:iam::000000000000:role/irrelevant --handler lambda_function.lambda_handler --zip-file fileb://sample_files/function1.zip
    ```
      
