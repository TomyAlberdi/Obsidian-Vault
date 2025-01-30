Created: 2024-09-22 15:44
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[Cloud]]
-- -
## Database + Backend AWS Deploy
### Components
- **RDS** for database.
- **EC2** for backend.
- **S3 Bucket** for storage (Optional).
### Make sure RDS & EC2 are in the same VPC and security group:
#### Modify the RDS Security Group:
1. Go to the EC2 Dashboard and click on Security Groups under Network & Security on the left-hand menu.
2. Locate the security group used by the RDS instance and click on its Group ID to open the details.
#### Add Inbound Rule for MySQL/Aurora:
1. In the Inbound rules tab, click Edit inbound rules.
2. Click Add rule.
3. Set the Type to MySQL/Aurora.
4. Set the Protocol to TCP and Port Range to 3306.
5. In the Source field, select Custom and enter the security group ID of the EC2 instance. Alternatively, you can enter the EC2 instance’s private IP address if you prefer.
6. Click Save rules.
### SSH tunneling for localhost database access:
`ssh -i D:/Proyectos/ns-key-pair.pem -N -L 3333:database-1.cle28k2aumpd.sa-east-1.rds.amazonaws.com:3306 ec2-user@18.230.192.254 -v`

* ```-i D:/Proyectos/ns-key-pair.pem```: Specifies the private key to use for authentication.
* ```-N```: Instructs SSH not to execute a remote command. Useful for port forwarding.
* ```-L 3333:database-1.cle28k2aumpd.sa-east-1.rds.amazonaws.com:3306```: Local port forwarding. Forwards local port 3333 to the RDS instance at port 3306.
* ```ec2-user@18.230.192.254```: The EC2 instance you are SSHing into.
* ```-v```: Enables verbose mode for debugging.

Terminal connection: ```mysql -h 127.0.0.1 -P 3333 -u admin -p```.