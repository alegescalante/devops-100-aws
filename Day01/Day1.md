100 Days of AWS Cloud — Day 1
Vijaya Rama Raju Kalidindi
Vijaya Rama Raju Kalidindi

Follow
3 min read
·
Dec 11, 2025





Starting the KodeKloud 100 Days of Cloud — AWS journey is exciting because each day reinforces a fundamental cloud concept through small, practical tasks.

On Day 1, we begin with one of the most basic yet essential building blocks in AWS: Key Pairs.

This task asks you to:

Create a key pair named devops-kp
Use RSA as the key type
Create it in us-east-1
Use the provided AWS credentials
Before we jump into the steps, let’s understand why key pairs exist and where they fit into the bigger AWS picture.

What is an EC2 Key Pair?

An EC2 Key Pair is a secure login mechanism that allows you to connect to your EC2 instances.
It consists of two parts:

Public Key — Stored by AWS automatically

Private Key — Downloaded by you and used to authenticate SSH connections

Think of it like a lock and key:

AWS installs the lock (public key) on the EC2 instance

You keep the key (private key)

Only someone with that private key can log in

This ensures a secure connection without exposing passwords that could be brute-forced.

Why RSA?
AWS supports multiple key types now (RSA, ED25519).
For this task, you must use RSA, which is:

Widely supported across all operating systems
Compatible with both older and modern SSH clients
The default choice for most production servers
Day: 1 Task Overview
Goal:
Create a key pair named devops-kp, type RSA, in us-east-1.

You will learn two methods:

AWS Management Console (UI) — Beginner-friendly
AWS CLI — Ideal for automation and real DevOps workflows
1. Creating the Key Pair via AWS Console (UI)
Step 1: Log in to the AWS Console
Use the credentials provided (via showcreds command on your AWS client host).

Step 2: Switch to the Correct Region
Top-right corner → Select N. Virginia (us-east-1)
Most AWS services are region-specific, including EC2 key pairs.

Step 3: Go to EC2 Service
Search for EC2
In the left navigation pane → click Key Pairs
Press enter or click to view image in full size

AWS Home Page
Step 4: Create the Key Pair
Click Create key pair

Fill the fields:

Name: devops-kp
Key pair type: RSA
Private key format.pem (recommended for Linux)

Become a Medium member
Click Create key pair.

Press enter or click to view image in full size

create key pair
Step 5: Save Your File
A file named devops-kp.pem will automatically download.

This is your private key.
Keep it securely — AWS never provides it again.

2. Creating the Key Pair via AWS CLI
Using CLI is an important skill for DevOps engineers because:

It automates repetitive tasks
It’s used in CI/CD pipelines
It integrates seamlessly with IaC tools (Terraform / CloudFormation)
Before running commands, configure credentials:

Step 1: Configure AWS CLI
aws configure
Enter:

AWS Access Key
AWS Secret Key
Region: us-east-1
Output: json
Step 2: Create the Key Pair
aws ec2 create-key-pair \
  --key-name devops-kp \
  --key-type rsa \
  --region us-east-1 \
  --query 'KeyMaterial' \
  --output text > devops-kp.pem
This command:

Creates the key pair
Retrieves only the private key
Saves it into devops-kp.pem
Step 3: Fix Permissions (Linux/Mac)
chmod 400 devops-kp.pem
This ensures SSH doesn’t reject the key due to open permissions.

Quick Verification
To confirm the key pair exists:

aws ec2 describe-key-pairs --key-name devops-kp --region us-east-1
You should see output containing:

"KeyName": "devops-kp",
"KeyType": "rsa"
Summary
On Day 1, you learned:

What EC2 key pairs are and why they matter
Why RSA is commonly used
How to create a key pair using both the AWS Console and CLI
How region selection impacts AWS resources
This foundational concept will be used throughout your EC2, VPC, and SSH-based tasks in the coming days.

Day 1 Completed!
You now have your first AWS resource created programmatically and via UI — a great start to the 100 days journey.
