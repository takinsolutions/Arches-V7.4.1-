Setting Up Arches 7.4.1 on AWS EC2 Instance

Prerequisites

An AWS EC2 instance running Ubuntu.
An SSH key pair (.pem file) associated with the EC2 instance.
Basic knowledge of the AWS console.
Step 1: Download the .pem File

1.1. After creating an EC2 instance on AWS, download the associated .pem key file.

1.2. Save the .pem file to a local directory of your choice.

1.3. Open a terminal and navigate to the directory containing the .pem file.

1.4. Change the file permissions to ensure it's secure:

bash
Copy code
chmod 400 your-key.pem
Verify the permissions using:

bash
Copy code
ls -l your-key.pem
Step 2: Establish a Remote Connection

2.1. Replace your-key.pem with the actual name of your AWS key file.

2.2. Replace your-instance-ip with the public IP address of your AWS instance.

bash
Copy code
ssh -i "your-key.pem" ubuntu@your-instance-ip
Step 3: Setup Arches Environment

3.1. Download the Arches installation script:

bash
Copy code
wget https://raw.githubusercontent.com/archesproject/arches/stable/7.4.0/arches/install/ubuntu_setup.sh
3.2. Execute the script:

bash
Copy code
source ./ubuntu_setup.sh
Step 4: Create a Virtual Environment

bash
Copy code
python3 -m venv ENV
source ENV/bin/activate
Step 5: Verify Python Version

bash
Copy code
python
Step 6: Update Pip

bash
Copy code
python -m pip install --upgrade pip
Step 7: Install Arches

bash
Copy code
pip install arches
Step 8: Create a New Arches Project

bash
Copy code
arches-project create my_project
cd my_project
Step 9: Setup the Database

bash
Copy code
python manage.py setup_db
Step 10: Edit Allowed Hosts

10.1. Open the request.py file:

bash
Copy code
nano ~/ENV/lib/python3.10/site-packages/django/http/request.py
10.2. Locate the line that says allowed_hosts and modify it:

python
Copy code
allowed_hosts = ['.localhost', '127.0.0.1', '[::1]', '*']
10.3. Save and exit the file.

Step 11: Run the Development Server

bash
Copy code
cd ~
cd my_project
python3 manage.py runserver your-instance-ip:8000
Step 12: Access the Arches Application

Open your web browser and navigate to:

plaintext
Copy code
http://your-instance-ip:8000/
Setting Up PostgreSQL with Arches 7.4.1

Step 1: SSH Tunnel to PostgreSQL

1.1. Open a new terminal separate from your Arches environment.

1.2. Create an SSH tunnel to the PostgreSQL database:

bash
Copy code
ssh -L 5432:localhost:5432 -N -i "your-key.pem" ubuntu@your-instance-ip
Step 2: PostgreSQL Commands

2.1. Switch to the PostgreSQL user:

bash
Copy code
sudo -i -u postgres
2.2. Start the PostgreSQL command-line interface:

bash
Copy code
psql
2.3. Create a new PostgreSQL user:

sql
Copy code
CREATE USER newuser;
2.4. Set a password for the new user:

sql
Copy code
ALTER USER newuser WITH PASSWORD 'your-password';
2.5. Grant necessary privileges to the user:

sql
Copy code
ALTER USER newuser WITH SUPERUSER CREATEDB CREATEROLE REPLICATION BYPASSRLS;
This README provides clear, step-by-step instructions for setting up Arches 7.4.1 and PostgreSQL on an AWS EC2 instance. Make sure to replace placeholders like your-key.pem and your-instance-ip with your actual values.

By following these instructions, you can efficiently set up your development environment for Arches 7.4.1 and PostgreSQL on AWS.
