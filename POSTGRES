# Setting Up PostgreSQL with Arches

To configure PostgreSQL for use with Arches, follow these steps:

1. Open a new terminal window separate from the one running the Arches environment.

2. Establish an SSH tunnel to your PostgreSQL server using the following command:

```bash
ssh -L 5432:localhost:5432 -N -i "atest.pem" ubuntu@ec2-15-237-62-130.eu-west-3.compute.amazonaws.com


```bash
chmod 400 atest.pem
```

Access the PostgreSQL command-line interface by entering:
css
Copy code
sudo -i -u postgres
psql
Create a new PostgreSQL user by executing the following SQL command:
sql
Copy code
CREATE USER newuser;
Set a password for the newly created user (replace 'London' with your desired password):
sql
Copy code
ALTER USER newuser WITH PASSWORD 'London2023';
Grant the necessary privileges to the user for PostgreSQL (superuser, createdb, createrole, replication, bypassrls) with this SQL command:
sql
Copy code
ALTER USER newuser WITH SUPERUSER CREATEDB CREATEROLE REPLICATION BYPASSRLS;
Ensure to replace any placeholders like file names and IP addresses with the actual values pertinent to your setup.
