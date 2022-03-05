# Udacity

> Cloud DevOps Engineer Nanodegree, Completed April 15, 2020

Project: Jenkins Pipelines on AWS

Required:

1. AWS CLI

Steps Taken:

1. Create a group called `jenkins` to add the IAM user `jenkins`.
    - Permissions
        - AmazonEC2FullAccess
        - AmazonS3FullAccess
        - AmazonVPCFullAccess
    - Create an IAM user called 'jenkins' to be granted access to AWS EC2 instance
2. Log into the AWS Console with the new user `jenkins`
    - Create a ssh key pair (chmod 400 *.pem)
    - Deploy an AWS EC2 Instance (Ubuntu)
        - Create a Security Group
            - Make sure TCP Port 8080 and TCP Port 22 is open
3. Install and configure Jenkins on AWS EC2 Instance
    - Launch the Jenkins website at `http://<IP>:8080` and follow the instructions to obtain the password.
        - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
        - Select `Install Suggested Plugins` to quickly finish the configuration.
        - Create first admin user `jenkins-admin:sTGkyFt4JW6Cud5`
    - Install the required plugins
        - Head to **Manage Jenkins** -> **Manage Plugins** -> Search under **Available** -> Blue Ocean -> Install without restarts
        - Head back to **Manage Plugins** and search under **Available** for Pipeline: AWS Steps and Download Now and Install after restart
4. Create a GitHub repository to store the code (skip if already created)
    - Create `index.html` and `Jenkinsfile`
    - Commit the code and push to the Git repository.
    - Copy and paste the Git url and authenticate with login.
5. Apply the AWS credentials in Jenkins
    - Select gear icon besides the project name, this will take you back to the original Jenkins website
    - Select **Credential** on the left side, and select **global** and select from the drop-down menu `AWS Credentials` (make sure that Jenkins has been restarted for this option to show up.)
6. Create an AWS S3 Bucket
    - Ensure that **Block Public Access Settings for this bucket** is unchecked
    - Agree to the acknowledgement
    - Select the bucket's name and head to **Permissions**
    - Edit **Bucket Policy**
7. Create the pipeline for AWS
8. Add another stage in the pipeline
    - Install `tidy` which is a linter to lint the example html file.

```bash
sudo apt update -y && sudo apt upgrade -y
sudo apt install openjdk-11-jdk-headless -y

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update -y && sudo apt install jenkins
