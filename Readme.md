# DATS 6450: Cloud Computing (AWS)

This repository contains all assignments and projects for the DATS 6450 course, focusing on cloud computing principles and practical application with Amazon Web Services (AWS).

## 📚 Table of Contents

* [Assignment 1: Create an AWS Account](#-assignment-1-create-an-aws-account)
* [Assignment 2: Practice IAM](#-assignment-2-practice-iam)
* [Assignment 3: VPC Wizard](#-assignment-3-vpc-wizard)
* [Assignment 4: Storage with CLI](#-assignment-4-storage-with-cli)
* [Assignment 5: EC2 Compute & Data Analysis](#-assignment-5-ec2-compute--data-analysis)
* [Assignment 6: Elastic Load Balancer (ELB)](#-assignment-6-elastic-load-balancer-elb)
* [Assignment 7: RDS Database Assignment](#-assignment-7-rds-database-assignment)
* [Assignment 9: Disaster Recovery](#-assignment-9-disaster-recovery-snapshots--amis)
* [Final Project: Part A (Proposal)](#-final-project-part-a-proposal)
* [Final Project: Part B (Implementation)](#-final-project-part-b-implementation)
* [In-Class Exercise: RDS Database Setup](#-in-class-exercise-rds-database-setup)

---

## 🏛️ Assignment 1: Create an AWS Account

You must create an AWS account to do homeworks and hand-on tutorials.
*(No submission required for this step)*

---

## 🔒 Assignment 2: Practice IAM

* Create 2 users, **S3TestUser** and **EC2TestUser**, with strong passwords.
* Generate an access key for each user and save them.
* Attach `AmazonS3FullAccess` to **S3TestUser**.
* Create a user group, **EC2TestGroup**.
* Attach `AmazonEC2FullAccess` to this group.
* Add **EC2TestUser** to this group.
* Create a role name, **EC2Describe**, and attach `AmazonEC2ReadOnlyAccess` to this role.

**Testing:**
1.  Login as **S3TestUser** and try to manipulate EC2 services.
2.  Then, create a bucket (`<classname><yourlastname><yourfirstname>`) in the `us-east-1` region, and upload a simple file into that bucket.
3.  Finally, login as **EC2TestUser** and try to access the file you uploaded before.

> **Deliverable:**
> Provide a Word file with a table where the 1st column contains your actions and the 2nd column provides screenshots of the screens.

---

## 🌐 Assignment 3: VPC Wizard

*Attached File: `Create VPC with MySQL client and server-v2.pdf`*

You will create a VPC with public and private subnets using the AWS Console VPC Wizard.
* Deploy an EC2 instance in the **public subnet** and install the MySQL client.
* Deploy an EC2 instance in the **private subnet** and install the MySQL Server.
* Log in to your MySQL server from the EC2 instance deployed in the public subnet.

The attached tutorial provides a step-by-step procedure. However, you should also search AWS documentation to address any issues you find.

---

## 🗂️ Assignment 4: Storage with CLI

In this assignment, you will use EC2, S3, and Boto.

1.  Using the AWS console or AWS CLI, create an S3 bucket in `us-east-1`.
2.  Launch an EC2 (public subnet) into your VPC (`us-east-1`). Make sure that ports **22 (SSH)**, **443 (used by Boto)**, and **8888 (used by Jupyter)** are open.
3.  SSH to your EC2 using the following command:
    ```bash
    ssh -L localhost:8888:localhost:8888 -i your_pem_key.pem ec2-user@the_pubic_ip_address_of_your_ec2
    ```
4.  Download baby names from US Social Security Administrations into your EC2.
    * Link: [https://www.ssa.gov/oact/babynames/limits.html](https://www.ssa.gov/oact/babynames/limits.html)
5.  Unzip the `names.zip` file into a directory (e.g., `babynames`).
6.  Using the S3 bucket you created, mount it as a directory in your EC2 (e.g., `ssn`).
    * You can follow instructions from [GeekForGeeks: Mount AWS S3 Bucket on Amazon EC2](https://www.geeksforgeeks.org/cloud-computing/mount-aws-s3-bucket-on-amazon-ec2-instance/).
7.  Move baby name files to your mounted local folder (e.g., `ssn`).
8.  Using Boto, write a Python program that lists the files in the S3 bucket.

---

## 💻 Assignment 5: EC2 Compute & Data Analysis

*Attached File: `Python for Data Analysis.pdf`*

Using what you have done in the previous assignment, you will create an EC2 (or re-use the EC2 you created) and analyze the baby names data.

1.  Launch an EC2 instance in the default VPC. Make sure you have enabled the public address.
2.  Log in to your EC2 via SSH, establishing a tunnel for Jupyter:
    ```bash
    ssh -L localhost:8888:localhost:8888 -i your_pem_key.pem ec2-user@the_pubic_ip_address_of_your_ec2
    ```
3.  Update the OS: `sudo yum update`
4