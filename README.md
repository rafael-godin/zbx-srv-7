# zbx-srv-7
Zabbix server 7.0 LTS

# Initial configuration (Secrets and variables)
Set up your database credentials and network before starting the deploy.

1. Create Secrets
Add the "secrets/" directory to the ".gitignore" to avoid leaking credentials.
Create the directory and the credential files.

# Secrets directory

$ mkdir -p secrets

# Add database user

$ echo "db_user" > secrets/postgre_user.txt

# Add database password

$ echo "db_password" > secrets/postgre_password.txt

# Update permission

$ chmod 600 secrets/postgre_user.txt
$ chmod 600 secrets/postgre_password.txt

2. External database configuration
Update the "docker-compose.yaml" with the databse host IP address or FQDN

environment:
  - DB_SERVER_HOST=db_host_ip_address
  - DB_SERVER_PORT=5432

3. Scripts directory (Opcional): Create it locally if you use external scripts or custom alerts (Telegram integration, AWS SNS, etc.)

$ mkdir -p scripts/alertscripts scripts/externalscripts

4. Run the deployment

$ docker-compose up -d

5. Run the "status" and "logs" command to check the deployment status and the application logs.

$ docker status "container_name"
$ docker-compose logs --tail=100 -f "container_name"

🌐 Interfac Web Access
Zabbix frontend will be available on port 80 of the host:

URL: http://<web-server-host-ip-address>/
