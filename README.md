A repository that will help you understand how to leverage some AWS services for free.
---

# What is LocalStack?

- LocalStack is an open-source project that allows you to run AWS services locally on your machine.
- It's designed to help developers develop and test their AWS applications without needing to connect to the actual AWS cloud.
- This can save time and money, as well as simplify the development process.

### Key Features of LocalStack:

1. **Emulates AWS Services**: LocalStack supports a wide range of AWS services, including S3, DynamoDB, Lambda, Kinesis, SQS, SNS, and more.
2. **Local Development**: You can develop and test your applications locally, which speeds up the development cycle and reduces the need for cloud resources.
3. **Cost-Effective**: By running AWS services locally, you avoid incurring unnecessary AWS costs during development and testing.
4. **Simplified Testing**: LocalStack allows you to test complex cloud architectures and integrations without dealing with cloud provisioning or network latency.
5. **Isolated Environment**: It provides an isolated environment for testing, which helps in identifying and fixing issues early in the development process.

---

### Steps to Start
There are multiple ways you can start using LocalStack. I'm showing you to implement using Docker, so that it will not interfere with your local system.

1. Download and Install Docker desktop [Follow this](https://github.com/RahulRoy-rsp/Kafka_On_Docker/tree/main#steps-to-download-install--configure-docker-on-windows-os)
2. Create a folder where you will be working. Let's say `LocalStack-Implementation`
3. Create a virtual environment in your folder. (I created virtual environment named `lstack`)
     ```bash
     python -m venv <env_name>
     ```
4. Activate the environment
     ```bash
     <env-name>\Scripts\activate
     ```
5. Install AWS CLI in your system. (There are multiple ways to do this, I prefered this one)
   ```bash
     msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
   ```
6. Verify installation. (open terminal and enter the below command)
   ```bash
     aws --version
   ```
    - If you face any errors like `'aws' is not recognized as an internal or external command`
    - Then, enter the following command: `where /R c:\ aws`
    - It returns the path where AWS CLI is installed, copy the path.
    - Now, go to Environment Variables in your windows settings and add the above path so that the system will be able to use the path for AWS.
    - Restart the system and again try to verify the installation `aws --version`
7. Configure AWS credentials. (I used profile_name as localstack) This profile will be used for interacting with the AWS Services.
   ```bash
     aws configure --profile <profile_name>
   ```
     - It will prompt you to enter some values as follows:
       - **AWS Access Key ID [None]**: *test*
       - **AWS Secret Access Key [None]**: *test*
       - **Default region name [None]**: *us-east-1*
       - **Default output format [None]**: *json*
     - I entered as shown above
8. Create a docker-compose file which contains the localstack's service. [Refer this](https://github.com/RahulRoy-rsp/LocalStack/blob/main/docker-compose.yml)
9. Start the container
   ```bash
     docker-compose up -d
   ```
 10. Verify if the localstack's container is up and running: `docker ps`.
11. You have succesfully configured the localstack setup on your machine.
    - You can list down the services available.
      ```bash
        curl http://localhost:4566/_localstack/health
      ```
