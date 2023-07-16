# Jenkins Pipeline: Push Artifact to S3

This repository contains an example Jenkins pipeline script that demonstrates how to build a Java Maven project, generate an artifact, and push it to an Amazon S3 bucket using the AWS CLI.

## Prerequisites

- Jenkins installed and configured
- AWS CLI installed on the Jenkins machine or container
- Git installed on the Jenkins machine or container
- Maven installed on the Jenkins machine or container (configured as "Maven-Tool" in Jenkins)
- IAM role with necessary permissions to access the S3 bucket

## Jenkins Setup

1. Install and configure Jenkins following the official [Jenkins Installation Guide](https://www.jenkins.io/doc/book/installing/).
2. Ensure that Jenkins has the necessary plugins installed:
   - Git plugin: Allows Jenkins to interact with Git repositories.
   - AWS CLI plugin: Integrates the AWS CLI into Jenkins for AWS-related operations.
   - Pipeline plugin: Enables Jenkins Pipeline support.
3. Install and configure the AWS CLI on the Jenkins machine or container. Refer to the official [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html) for detailed instructions.
4. Install and configure the Maven tool in Jenkins:
   - Go to Jenkins Dashboard > Manage Jenkins > Global Tool Configuration.
   - Locate the 'Maven' section and add a new Maven installation.
   - Provide the necessary details such as the name, MAVEN_HOME, and version.

## IAM Role Setup

1. Create an IAM role in your AWS account with the necessary permissions to access the S3 bucket.
   - Go to the IAM service in the AWS Management Console.
   - Click on "Roles" in the left navigation pane.
   - Click on "Create Role".
   - Select the service that will use this role (e.g., EC2).
   - Choose the permissions policies required for your use case (e.g., AmazonS3FullAccess).
   - Add any additional policies based on your specific requirements.
   - Provide a name for the role and click on "Create Role".
2. Attach the IAM role to the Jenkins EC2 instance or ECS container where Jenkins is running.
   - For EC2:
     - Go to the EC2 service in the AWS Management Console.
     - Select the Jenkins instance.
     - Click on "Actions" > "Instance Settings" > "Attach/Replace IAM Role".
     - Select the IAM role you created and click on "Apply".
   - For ECS:
     - Go to the ECS service in the AWS Management Console.
     - Select the Jenkins task definition.
     - Click on the "Task Roles" section.
     - Click on "Edit".
     - Select the IAM role you created and click on "Save".

## Pipeline Steps

1. Checkout: Clones the Git repository containing the Java Maven project.
2. Build: Performs a Maven build to compile and package the project.
3. Push to S3: Copies the generated JAR file to the specified S3 bucket using the AWS CLI.

## Usage

1. Create a new pipeline job in Jenkins.
2. Configure the pipeline to use the Jenkinsfile included in this repository.
3. Update the Jenkinsfile:
   - Adjust the Git repository URL in the `git` step.
   - Modify the S3 bucket name in the `aws s3 cp` command.
   - Customize any additional build steps as needed.
4. Save the Jenkins pipeline job configuration.
5. Run the pipeline job to trigger the build and artifact push to S3.
