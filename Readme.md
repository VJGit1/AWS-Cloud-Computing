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
* [Assignment 9: Disaster Recovery](#-assignment-9-disaster-recovery)
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
4.  Create a virtual environment:
    ```bash
    cd ~/
    mkdir ec2_assignement
    cd ec2_assignement
    python3 -m venv venv
    source venv/bin/activate
    ```
5.  Install required packages:
    ```bash
    pip install pandas
    pip install jupyter
    pip install matplotlib
    ```
6.  Launch Jupyter Notebook: `jupyter notebook`
    * Open the URL provided in your local laptop's browser.
7.  Download the SSA names data:
    ```bash
    wget [https://www.ssa.gov/oact/babynames/names.zip](https://www.ssa.gov/oact/babynames/names.zip)
    ```
8.  Follow the instructions in the attached PDF and perform all required analyses.
    * Tutorial: [https://www.youtube.com/watch?v=pp04EEkp4m8](https://www.youtube.com/watch?v=pp04EEkp4m8)

---

## ⚖️ Assignment 6: Elastic Load Balancer (ELB)

* [Reference Video](https://youtu.be/Ar5prfTlI-k)

1.  Reuse your VPC configuration or use the Default VPC.
2.  Launch 2 EC2s in 2 different Availability Zones (AZs) and install, start, and enable Apache.
3.  Create a Target Group and add these 2 EC2s.
4.  Create an Application Load Balancer (e.g., `MyElb`) and ensure the 2 EC2s are part of the target group.
5.  Access the ELB via the web.
6.  Stop one EC2 and access the ELB again.
7.  Stop the second EC2 and access the ELB again.
8.  Describe the results.

---

## 🗃️ Assignment 7: RDS Database Assignment

*Attached File: `Python for Data Analysis.pdf`*

You will load the SSA baby names data into a relational database.
* Data Source: [https://www.ssa.gov/oact/babynames/names.zip](https://www.ssa.gov/oact/babynames/names.zip)
* The data format is `Name,Sex,Frequency`, e.g.:
    ```
    Mary,F,7065
    Anna,F,2604
    Emma,F,2003
    ```

**Requirements:**
1.  Create a VPC (or use an existing one) with 2 Public and 2 Private Subnets. Ensure public subnets assign public IPs.
    * `Pub1` and `Priv1` can be in the same AZ.
    * `Pub2` and `Priv2` must be in a different AZ.
2.  Create a security group `SgClientTier` with ports **22**, **80**, and **8888** open to the internet.
3.  Create a security group `SgDbTier` for the database.
    * This SG must have the DB port open (e.g., **3306**).
    * It must accept requests from `SgClientTier`. (Set the source as the ID of the `SgClientTier` security group).
4.  Create a private, highly available RDS database instance.
5.  Create an EC2 instance in a public subnet to act as a client.
6.  Download the `names.zip` file to the EC2 instance (or use S3).
7.  Connect to your RDS database and create a table to hold the information (e.g., `Name`, `Gender`, `Frequency`, `Year`).
8.  Write a script to parse the `yobXXXX.txt` files and populate the database. The year is in the filename.
9.  Write a Python program to generate a graph showing the total births by gender and year.

> **Deliverables (Screenshots):**
> * Your RDS database in the AWS console.
> * The tables in your database.
> * Data populated in your database (e.Example: a `SELECT` query).
> * The final generated graph.

* Reference: [AWS RDS Tutorial](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MariaDB.html)

---

## 🔄 Assignment 9: Disaster Recovery

You will create a simple Disaster Recovery (DR) solution.

**On the `us-east-1` (East Coast) Region:**
1.  Create an EC2 instance and install Apache (ensure it starts on boot).
2.  Create a snapshot of this EC2's volume.
3.  Create an Amazon Machine Image (AMI) from the snapshot.
4.  Copy that AMI to the `us-west-1` (West Coast) region, let's call it `WCR`.

**On the `us-west-1` (West Coast) Region:**
1.  Create a new EC2 instance from the AMI you copied.
2.  Launch the instance.
3.  Log in to the instance and access Apache to verify it's working.

> **Deliverable:**
> Submit a Word file with a two-column table.
> * **Column 1:** Your action.
> * **Column 2:** The result (with screenshots).
> Provide enough detail for the TA to assess your assignment.

---

## 🚀 Final Project: Part A (Proposal)

Students will work in groups to develop a data science project that leverages AWS Cloud Services.

**Assignment:**
Develop a presentation (5-15 min video + slide deck) covering:
1.  **Project Definition:**
    * Scope of the project.
    * Features to be implemented.
    * Data sources.
    * Expected outcomes.
2.  **Project Architecture:**
    * Logical architecture diagram indicating AWS services used (VPC, EC2, S3, RDS, etc.).
    * Data flow diagram (how data is ingested, cleaned, processed, and released).

* [AWS Architecture Icons](https.aws.amazon.com/architecture/icons/)
* [AWS Architecture Whitepapers/Examples](https://aws.amazon.com/whitepapers/?whitepapers-main.sort-by=item.additionalFields.sortDate&whitepapers-main.sort-order=desc&awsf.whitepapers-content-type=content-type%23arch-diagram)

---

## 🏆 Final Project: Part B (Implementation)

This is the implementation and final presentation of your project.

**Grading Components:**
* Presentation
* Demo
* Project Architecture

**Requirements:**
1.  **Project Implementation:** Demonstrate your solution in action, showing cloud services, inputs, and outputs.
2.  **Project Presentation:** Present your project (in-person or video) covering all aspects from Part A plus your final results.
3.  **GitHub:** All project artifacts (code, presentations, etc.) must be uploaded to GitHub.
4.  **Submission:** Submit the video and presentation slides.

---

## ✏️ In-Class Exercise: RDS Database Setup

* Use the AWS Tutorial: [Create and Connect to a MariaDB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.CreatingConnecting.MariaDB.html)
* Create a database client (EC2) and a database server (MySQL or MariaDB using the AWS RDS service).