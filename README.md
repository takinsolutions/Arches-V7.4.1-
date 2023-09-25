# Arches V7.4.1 

<p align="justify">
Welcome to the Arches V7.4.1 installation guide!<br>
  
<div>
This guide provides comprehensive instructions for setting up the Arches ontological database on an AWS EC2 instance. Arches is a powerful web-based database platform designed for creating and managing archives and information. This file's sole purpose is to help end users install the latest version of the ontological database called Arches.
</div><br>For a more detailed explanation of the installation process, please review the document below:
</br>

</p>



## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Before we start](#before-we-start)
- [Getting started](#getting-started)
  - [Step 1: Download the .pem File](#step-1-download-the-pem-file)
  - [Step 2: Establish a Remote Connection](#step-2-establish-a-remote-connection)
  - [Step 3: Setup Arches Environment](#step-3-setup-arches-environment)
  - [Step 4: Create a Virtual Environment](#step-4-create-a-virtual-environment)
  - [Step 5: Verify Python Version](#step-5-verify-python-version)
  - [Step 6: Update Pip](#step-6-update-pip)
  - [Step 7: Install Arches](#step-7-install-arches)
  - [Step 8: Create a New Arches Project](#step-8-create-a-new-arches-project)
  - [Step 9: Setup the Database](#step-9-setup-the-database)
  - [Step 10: Edit Allowed Hosts](#step-10-edit-allowed-hosts)
  - [Step 11: Run the Development Server](#step-11-run-the-development-server)
  - [Step 12: Access the Arches Application](#step-12-access-the-arches-application)
- [Setting Up PostgreSQL with Arches](#setting-up-postgresql-with-arches)
  - [Step 1: SSH Tunnel to PostgreSQL](#step-1-ssh-tunnel-to-postgresql)
  - [Step 2: PostgreSQL Commands](#step-2-postgresql-commands)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)


## Introduction

<p align="justify">
Arches V7.4.1 Installation Guide

Greetings and welcome to the Arches V7.4.1 installation guide! Our aim is to furnish you with detailed instructions for configuring the Arches ontological database on an AWS EC2 instance. Arches stands as a robust web-based database platform, purpose-built for the creation and effective management of archives and information.

Within this README file, you'll find a comprehensive, step-by-step walkthrough that guarantees a hassle-free installation experience for Arches. Whether you're just beginning your journey with Arches or seeking to enhance your current setup, rest assured, we've got your back.

The guide covers the following key steps:

1. **Preparing Your Environment**: Learn how to configure and secure your AWS EC2 instance to ensure a successful installation.

2. **Establishing a Secure Connection**: Connect to your AWS instance securely using SSH, granting you remote access to your environment.

3. **Installing Arches**: Download and install the latest version of Arches, including all necessary dependencies.

4. **Creating a Virtual Environment**: Set up a virtual environment to manage your Arches project effortlessly.

5. **Database Configuration**: Configure the database for your Arches project, allowing you to store and retrieve data efficiently.

6. **Fine-Tuning Arches**: Learn how to customize your Arches environment and optimize it for your specific needs.

7. **Starting Your Arches Project**: Initialize a new Arches project and set it up for your use case.

8. **Accessing Your Arches Application**: Discover how to access your Arches web application and begin working with your data.
   
</p> 

## PrerequisitesPrerequisites

Before you begin the installation of Arches V7.4.1 on your AWS EC2 instance, ensure that you have the following prerequisites in place:

1. AWS Account
* You should have an active AWS account with appropriate permissions to create and manage EC2 instances.

2. AWS EC2 Instance
* Create an AWS EC2 instance with the following considerations:
* Choose an EC2 instance type that aligns with your expected workload and performance requirements.
* Configure security groups and network settings to allow SSH access to your instance.
* Ensure that your instance has sufficient storage space to accommodate the Arches installation and any data you plan to manage.

4. SSH Client
* Have an SSH client installed on your local machine. 
* Most Unix-based systems (Linux, macOS) have SSH pre-installed. For Windows, you can use tools like PuTTY or Windows Subsystem for Linux (WSL).

5. .pem File
* After creating your EC2 instance, you will receive a .pem file that serves as the private key for accessing the instance. Make sure you download and save this file securely.

6. Python 3
* Python 3 should be installed on your local machine. You can check your Python version by running python3 --version in your terminal.
7. Git (Optional)
* While not strictly required, having Git installed on your local machine can be useful for managing your Arches project and obtaining the installation script from the Arches repository.

8. Basic Knowledge of AWS
* A fundamental understanding of AWS services, especially EC2, will be beneficial for configuring your instance and understanding the AWS environment.

9. AWS CLI (Optional)
* The AWS Command Line Interface (CLI) can be handy for configuring AWS settings, but it's optional for this installation.
* Please ensure that you have these prerequisites in place before proceeding with the Arches installation. Once you've verified these prerequisites, you can start following the installation steps 
 outlined in the guide.

## Before we start

To start the installation process, follow the instructions in the sections provided below. Each step is accompanied by detailed explanations and commands to ensure a successful setup.

**Note**: It's important to replace any placeholders, such as `your-key.pem` or `your-instance-ip`, with your actual AWS instance information for a seamless experience.

Now, let's dive into the installation process and get Arches up and running on your AWS EC2 instance!

> **Next:** Proceed to [Step 1: Preparing Your Environment](#step-1-preparing-your-environment).

## Getting Started

### Downloading the AWS EC2 Instance

Before you can begin using Arches on your local machine, you need to set up an AWS EC2 instance and acquire the necessary files.

### 1.1. Create an AWS EC2 Instance

Start by creating an AWS EC2 instance tailored to your requirements. Ensure you choose the appropriate instance type and configurations for your specific use case.

### 1.2. Download the .pem File

Once your EC2 instance is created, you will receive a .pem file. This file is crucial for securely connecting to your EC2 instance.

### 1.3. Save the .pem File

After downloading, save the .pem file to a directory on your local machine, and make note of the directory's path, as it will be needed shortly.

### 1.4. Set File Permissions

Open your terminal and navigate to the directory where the .pem file is located using the `cd` command. For example, if your username is "Alex," you can navigate using `cd /users/Alex`. To enhance security, limit access to the .pem file by executing the following command:

```bash
chmod 400 atest.pem
```
This command adjusts the file's permissions so that only the file's owner has read permissions. To confirm this change, run:

```
ls -l atest.pem
```
You should observe the updated file permissions.

## Establishing a Remote Connection
With the .pem file and correct permissions in place, you can now establish a secure remote connection to your AWS EC2 instance.

### 2.1. SSH Connection

Utilize the SSH (Secure Shell) command to connect to your instance. Replace <i>"atest.pem"</i>  with the actual name of your .pem file, and "ubuntu@ec2-15-237-62-130.eu-west-3.compute.amazonaws.com" with the actual IP address or domain name of your AWS instance. The command should resemble like this: 

```
ssh -i "atest.pem" ubuntu@ec2-15-237-62-130.eu-west-3.compute.amazonaws.com
```
## 3. Setting Up the Arches Environment
Now that you have established remote access to your AWS instance, it's time to configure the environment for Arches.

### 3.1. Downloading the Setup Script

Execute the following command to download the Arches setup script from the official repository:
```
wget https://raw.githubusercontent.com/archesproject/arches/stable/7.4.0/arches/install/ubuntu_setup.sh
```

### 3.2. Executing the Setup Script

After downloading the script, create a file called "ubuntu_setup.sh" by running:
```
source ./ubuntu_setup.sh
```
This script automates the installation of all necessary dependencies and applications for Arches.

## 4. Creating a Virtual Environment
To manage your Arches project efficiently, it's recommended to create a virtual environment.

### 4.1. Create a Virtual Environment

Use the following command to create a new virtual environment named "ENV":
```
python3 -m venv ENV
```
### 4.2. Activate the Virtual Environment

Activate the virtual environment using the command:
```
source ENV/bin/activate
```
## 5. Verifying Python Version and Update Pip

### 5.1. Check Python Version

Confirm the Python version installed on your AWS instance by running:
```
python
```
This command will display the Python version.

### 5.2. Updating Pip

Ensure that Pip, the Python package manager, is up to date:
```
python -m pip install --upgrade pip
```

## 6. Installing Arches

### 6.1. Install Arches

Use the following command to install the latest stable release of Arches:
```
pip install arches
```

## 7. Creating an Arches Project

### 7.1. Create an Arches Project

Kickstart a new Arches project by running:
```
arches-project create my_project
```

## 8. Setting Up the Database
To store and manage data within Arches, it's essential to set up the database.

### 8.1. Change Directory to Your Project

Navigate to your project directory using:
```
cd my_project
```
### 8.2. Database Setup

Create the database itself by executing:
```
python manage.py setup_db
```

## 9. Configuring Allowed Hosts
#### 9.1. Edit Allowed Hosts

Navigate to the following directory:

```
cd ENV/lib/python3.10/site-packages/django/http
```

In this directory, open the <i>"request.py"</i> file using a text editor.
Locate the line that defines "Allowed Hosts" and edit it to include all the ports. Change this line:
```
allowed_hosts = settings.ALLOWED_HOSTS
```
to:

```
allowed_hosts = settings.ALLOWED_HOSTS + ['*']
```
This addition allows traffic to be transported through all available ports.
Save your changes and exit the text editor.
Return to the Project Directory

```
cd ~
cd my_project
```
## 10 Start the Development Server

Run the following command to initiate the Arches development server:
```
python3 manage.py runserver ec2-15-237-62-130.eu-west-3.compute.amazonaws.com:8000
```
!!! IMPORTANT !!! <br>
Don't forget to replace the name of the server given above with the actual name and IP Address of your AWS Instance

## 11. Accessing the Arches Application

### 11.1. Open a Web Browser

Launch your web browser and navigate to:

```
http://ec2-15-237-62-130.eu-west-3.compute.amazonaws.com:8000/
```

This URL provides access to your Arches web application.
This concludes the setup process for Arches on your AWS EC2 instance. 
You are now ready to utilize and develop with Arches.



## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


