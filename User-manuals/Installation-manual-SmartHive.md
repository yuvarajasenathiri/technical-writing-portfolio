# SmartHive installation manual

- Version: 1.0
- Last updated: May 2026
- Applies to: SmartHive Cloud and SmartHive Self-Hosted

---

## Table of contents

1.  [Introduction](#introduction)
	  - [Who this manual is for](#who-this-manual-is-for)
      - [Deployment options](#deployment-options)
      - [How to use this manual](#how-to-use-this-manual)
      - [Related documentation](#related-documentation)
2.  [System requirements](#system-requirements)
      - [Cloud requirements](#cloud-requirements)
      - [Self-hosted requirements](#self-hosted-requirements)
3.  [Cloud deployment](#cloud-deployment)
      - [Create your SmartHive account](#create-your-SmartHive-account)
      - [Configure your workspace](#configure-your-workspace)
      - [Set up your domain](#set-up-your-domain)
      - [Connect your support channels](#connect-your-support-channels)
      - [Invite your team](#invite-your-team)
4.  [Self-hosted deployment](#self-hosted-deployment)
      - [Before you begin](#before-you-begin)
      - [Install on Linux](#install-on-linux)
      - [Install on Windows Server](#install-on-windows-server)
      - [Configure the database](#configure-the-database)
      - [Configure environment variables](#configure-environment-variables)
      - [Start SmartHive services](#start-SmartHive-services)
      - [Verify the installation](#verify-the-installation)
5.  [Post-installation setup](#post-installation-setup)
      - [Configure SSL](#configure-ssl)
      - [Set up email](#set-up-email)
      - [Configure single sign-on](#configure-single-sign-on)
      - [Set up backups](#set-up-backups)
6.  [Upgrade SmartHive](#upgrade-SmartHive)
      - [Upgrade a cloud deployment](#upgrade-a-cloud-deployment)
      - [Upgrade a self-hosted deployment](#upgrade-a-self-hosted-deployment)
7.   [Uninstall SmartHive](#uninstall-SmartHive)
      - [Delete a cloud workspace](#delete-a-cloud-workspace)
      - [Uninstall from Linux](#uninstall-from-linux)
      - [Uninstall from Windows Server](#uninstall-from-windows-server)
8.   [Troubleshooting](#troubleshooting)

---

## Introduction

### Who this manual is for

This manual is for system administrators and developers who deploy, configure, and maintain SmartHive for their organization.

You should be familiar with:

- Basic server administration (Linux or Windows Server)
- Command-line interfaces
- Database management (PostgreSQL)
- Network configuration and DNS management

If you're an end user, see the [User-manual-SmartHive](./User-manuals/User-manual-SmartHive.md) to set up your account after your admin deploys SmartHive.

### Deployment options

SmartHive supports two deployment models:

| Deployment | Description | Best for |
|---|---|---|
| Cloud | SmartHive hosts and manages the infrastructure. You access SmartHive through a browser or mobile app. | Teams that want a fast setup with no infrastructure overhead |
| Self-hosted | You deploy SmartHive on your own servers. You control the infrastructure, data, and configuration. | Organizations with data residency requirements, security policies, or custom infrastructure needs |

Both deployment models provide the same SmartHive features. The difference is who manages the infrastructure.

### How to use this manual

- To set up SmartHive Cloud, follow [Cloud deployment](#cloud-deployment).
- To set up SmartHive Self-Hosted, review [System requirements](#system-requirements), and then follow [Self-hosted deployment](#self-hosted-deployment).
- For all deployments, complete [Post-installation setup](#post-installation-setup).

### Related documentation

| Document | Description |
|---|---|
| [SmartHive User manual](User-manual-SmartHive.md) | End-to-end manual for support agents and team leads |
| [SmartHive Developer's manual](./Developer-onboarding-docs/API-overview-SmartHive-Projects.md) | Technical manual for developers who build on SmartHive |
| [SmartHive API Documentation](./API-references/API-references-SmartHive-Projects.md) | Complete reference for the SmartHive API |
| [Victa Release Notes](./Release-notes/Victa-4.2-release-notes.md) | Summary of changes in each SmartHive release |

---

## System requirements

### Cloud requirements

SmartHive Cloud doesn't require server infrastructure. The devices that access SmartHive must meet the following requirements.

#### Web app

| Requirement | Minimum |
|---|---|
| Browser | Google Chrome 110 or later, Mozilla Firefox 110 or later, Microsoft Edge 110 or later, or Safari 16 or later |
| Internet connection | 5 Mbps or faster |
| Screen resolution | 1280 x 720 or higher |

#### Mobile app

| Requirement | iOS | Android |
|---|---|---|
| Operating system | iOS 16.0 or later | Android 11.0 or later |
| Storage | 200 MB of free space | 200 MB of free space |
| Internet connection | 4G LTE or Wi-Fi | 4G LTE or Wi-Fi |

### Self-hosted requirements

#### Server requirements

| Component | Minimum | Recommended |
|---|---|---|
| CPU | 4 cores | 8 cores |
| RAM | 8 GB | 16 GB |
| Storage | 50 GB SSD | 200 GB SSD |
| Operating system | Ubuntu 20.04 LTS or Windows Server 2019 | Ubuntu 22.04 LTS or Windows Server 2022 |

#### Software dependencies

| Dependency | Version |
|---|---|
| Node.js | 18.x or later |
| PostgreSQL | 14.x or later |
| Redis | 7.x or later |
| Nginx | 1.22 or later |
| Docker (optional) | 24.x or later |

> **Note:** On Windows Server, use Memurai, a Redis-compatible server for Windows, in place of Redis.

#### Network requirements

| Requirement | Details |
|---|---|
| Inbound ports | 80 (HTTP) and 443 (HTTPS) |
| Outbound ports | 25, 465, and 587 (email), and 443 (HTTPS for external services) |
| DNS | A valid domain name that points to your server |

> **Important:** SmartHive requires a publicly accessible domain name and a valid SSL certificate for production deployments. Don't deploy SmartHive in production without SSL.

---

## Cloud deployment

### Create your SmartHive account

1. Go to [https://SmartHive.io/signup](https://SmartHive.io/signup).
2. Enter your work email address, and then select **Get started**.
3. Check your inbox for the verification email from SmartHive, and then select **Verify email**.
4. On the account setup page, enter:
   - Your full name
   - Your company name
   - A password with at least 12 characters, including one uppercase letter, one number, and one special character
5. Select **Create account**.

### Configure your workspace

After you create your account, the setup wizard starts.

1. Enter a workspace name. This is the internal name that your team sees.
2. Enter a subdomain for your SmartHive instance (for example, `acmesupport.SmartHive.io`). You can change it later.
3. Select your time zone. SmartHive uses the time zone for service level agreement (SLA) calculations, report scheduling, and time stamps.
4. Select a subscription plan. You can start with a 14-day free trial.
5. Select **Finish setup**.

SmartHive creates your workspace and opens the admin dashboard.

### Set up your domain

By default, you can access your SmartHive instance at `yourworkspace.SmartHive.io`. To use a custom domain (for example, `support.yourcompany.com`):

1. Select **Settings** > **Workspace** > **Custom domain**.
2. Enter your custom domain, and then select **Save**.
3. SmartHive displays two DNS records for domain verification: a CNAME record and a TXT record.
4. Sign in to your DNS provider, and add both records.
5. Return to SmartHive, and then select **Verify domain**.

> **Note:** DNS changes can take up to 48 hours to propagate. SmartHive sends you an email when verification is complete.

### Connect your support channels

SmartHive receives cases from email, live chat, web forms, and phone. Connect at least one channel before you invite your team.

#### Email

1. Select **Settings** > **Channels** > **Email**.
2. Select **Add email channel**.
3. Enter a name for the channel (for example, `Support`) and the email address you want to use (for example, `support@yourcompany.com`).
4. Follow the on-screen instructions to set up email forwarding from your email provider to SmartHive.
5. Select **Verify and save**.

#### Live chat

1. Select **Settings** > **Channels** > **Live chat**.
2. Select **Add live chat**.
3. Set the chat widget's appearance, operating hours, and greeting message.
4. Select **Save**.
5. Copy the embed code, and add it to the `<head>` section of your website.

#### Web form

1. Select **Settings** > **Channels** > **Web form**.
2. Select **Create form**.
3. Set the form fields, subject, and default assignee.
4. Select **Save**.
5. Copy the form URL or embed code, and add the form to your website.

### Invite your team

1. Select **Settings** > **Users and permissions**.
2. Select **Invite users**.
3. Enter the email addresses of the team members you want to invite.
4. Assign a role to each user: **Admin**, **Team Lead**, **Agent**, or **Viewer**.
5. Select **Send invitations**.

SmartHive sends an invitation email to each person. Invitation links expire after 72 hours.

---

## Self-hosted deployment

### Before you begin

Before you install SmartHive, make sure that:

- Your server meets the [system requirements](#self-hosted-requirements).
- You have root or sudo access on the server.
- You have a domain name with DNS that points to your server.
- You have an SSL certificate for your domain.
- PostgreSQL, Redis, and Node.js are installed, or you're ready to install them.

> **Warning:** Don't install SmartHive on a production server that's already running other services without first consulting your infrastructure team. SmartHive requires dedicated ports 80 and 443.

### Install on Linux

These instructions apply to Ubuntu 20.04 LTS and Ubuntu 22.04 LTS.

1. Update your system:

   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. Install the dependencies:

   ```bash
   sudo apt install -y curl git nginx postgresql postgresql-contrib redis-server
   ```

3. Install Node.js 18.x:

   ```bash
   curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
   sudo apt install -y nodejs
   ```

4. Verify that Node.js and npm are installed:

   ```bash
   node --version
   npm --version
   ```

5. Download SmartHive:

   ```bash
   cd /opt
   sudo git clone https://github.com/SmartHive/SmartHive.git
   cd SmartHive
   ```

6. Install the SmartHive dependencies:

   ```bash
   sudo npm install --omit=dev
   ```

7. Create the SmartHive system user:

   ```bash
   sudo useradd --system --shell /bin/false SmartHive
   sudo chown -R SmartHive:SmartHive /opt/SmartHive
   ```

### Install on Windows Server

These instructions apply to Windows Server 2019 and Windows Server 2022.

1. Download and install Node.js 18.x from [https://nodejs.org](https://nodejs.org). Select version 18.x.
2. Download and install PostgreSQL 14 from [https://www.postgresql.org/download/windows](https://www.postgresql.org/download/windows).
3. Download and install Memurai, a Redis-compatible server for Windows, from [https://www.memurai.com/get-memurai](https://www.memurai.com/get-memurai).
4. Open PowerShell, and verify that Node.js and npm are installed:

   ```powershell
   node --version
   npm --version
   ```

5. Open PowerShell as an administrator, and download SmartHive:

   ```powershell
   cd C:\
   git clone https://github.com/SmartHive/SmartHive.git
   cd SmartHive
   ```

6. Install the SmartHive dependencies:

   ```powershell
   npm install --omit=dev
   ```

### Configure the database

> **Important:** In the following commands, replace `your_password` with a strong, unique password. Store the password securely. You need it when you configure environment variables.

#### Linux

1. Switch to the PostgreSQL user:

   ```bash
   sudo -i -u postgres
   ```

2. Open the PostgreSQL prompt:

   ```bash
   psql
   ```

3. Create the SmartHive database and user:

   ```sql
   CREATE DATABASE SmartHive;
   CREATE USER SmartHiveuser WITH ENCRYPTED PASSWORD 'your_password';
   GRANT ALL PRIVILEGES ON DATABASE SmartHive TO SmartHiveuser;
   \q
   ```

4. Exit the PostgreSQL user session:

   ```bash
   exit
   ```

#### Windows Server

1. Open pgAdmin (installed with PostgreSQL).
2. Connect to your PostgreSQL server.
3. Right-click **Databases**, and then select **Create** > **Database**.
4. Name the database `SmartHive`, and then select **Save**.
5. Open **Query Tool**, and run:

   ```sql
   CREATE USER SmartHiveuser WITH ENCRYPTED PASSWORD 'your_password';
   GRANT ALL PRIVILEGES ON DATABASE SmartHive TO SmartHiveuser;
   ```

### Configure environment variables

SmartHive uses a `.env` file for all configuration. Copy the example file, and then edit the copy.

#### Linux

1. Copy the example file, and open the copy in an editor:

   ```bash
   sudo cp /opt/SmartHive/.env.example /opt/SmartHive/.env
   sudo nano /opt/SmartHive/.env
   ```

#### Windows Server

1. Copy the example file, and open the copy in an editor:

   ```powershell
   Copy-Item C:\SmartHive\.env.example C:\SmartHive\.env
   notepad C:\SmartHive\.env
   ```

#### Set the variables

Update the following variables in the `.env` file, and then save and close the file.

| Variable | Description | Example |
|---|---|---|
| `APP_URL` | The full URL of your SmartHive instance | `https://support.yourcompany.com` |
| `APP_PORT` | The port that SmartHive runs on | `3000` |
| `DB_HOST` | The PostgreSQL server host | `localhost` |
| `DB_PORT` | The PostgreSQL port | `5432` |
| `DB_NAME` | The database name | `SmartHive` |
| `DB_USER` | The database user name | `SmartHiveuser` |
| `DB_PASSWORD` | The database password | `your_password` |
| `REDIS_HOST` | The Redis server host | `localhost` |
| `REDIS_PORT` | The Redis port | `6379` |
| `SECRET_KEY` | A random secret key for session encryption | Generate the key by running `openssl rand -hex 32` |
| `MAIL_FROM` | The email address that SmartHive sends mail from | `support@yourcompany.com` |
| `MAIL_HOST` | Your SMTP server host | `smtp.yourcompany.com` |
| `MAIL_PORT` | Your SMTP server port | `587` |
| `MAIL_USER` | Your SMTP user name | `support@yourcompany.com` |
| `MAIL_PASSWORD` | Your SMTP password | `your_mail_password` |

### Start SmartHive services

#### Linux

1. Initialize the database:

   ```bash
   cd /opt/SmartHive
   sudo -u SmartHive npm run db:migrate
   ```

2. Create a systemd service file:

   ```bash
   sudo nano /etc/systemd/system/SmartHive.service
   ```

3. Add the following content to the file:

   ```ini
   [Unit]
   Description=SmartHive
   After=network.target postgresql.service redis-server.service

   [Service]
   Type=simple
   User=SmartHive
   WorkingDirectory=/opt/SmartHive
   ExecStart=/usr/bin/node server.js
   Restart=on-failure
   RestartSec=10
   StandardOutput=syslog
   StandardError=syslog
   SyslogIdentifier=SmartHive

   [Install]
   WantedBy=multi-user.target
   ```

4. Set SmartHive to start at boot, and then start the service:

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable SmartHive
   sudo systemctl start SmartHive
   ```

5. Create the Nginx configuration file to set up Nginx as a reverse proxy:

   ```bash
   sudo nano /etc/nginx/sites-available/SmartHive
   ```

6. Add the following configuration to the file:

   ```nginx
   server {
       listen 80;
       server_name support.yourcompany.com;

       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

7. Link the configuration into the enabled sites, test it, and restart Nginx:

   ```bash
   sudo ln -s /etc/nginx/sites-available/SmartHive /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl restart nginx
   ```

#### Windows Server

1. Initialize the database:

   ```powershell
   npm run db:migrate
   ```

2. Install SmartHive as a Windows service by using NSSM:

   ```powershell
   nssm install SmartHive "C:\Program Files\nodejs\node.exe" "C:\SmartHive\server.js"
   nssm set SmartHive AppDirectory C:\SmartHive
   nssm start SmartHive
   ```

3. Download Nginx 1.22 or later for Windows from [https://nginx.org/en/download.html](https://nginx.org/en/download.html), and extract it to `C:\nginx`.
4. Open `C:\nginx\conf\nginx.conf` in an editor, and replace its contents with the following configuration:

   ```nginx
   events {}

   http {
       server {
           listen 80;
           server_name support.yourcompany.com;

           location / {
               proxy_pass http://localhost:3000;
               proxy_http_version 1.1;
               proxy_set_header Upgrade $http_upgrade;
               proxy_set_header Connection 'upgrade';
               proxy_set_header Host $host;
               proxy_set_header X-Real-IP $remote_addr;
               proxy_cache_bypass $http_upgrade;
           }
       }
   }
   ```

5. Test the configuration, and then install Nginx as a Windows service by using NSSM:

   ```powershell
   cd C:\nginx
   .\nginx.exe -t
   nssm install Nginx "C:\nginx\nginx.exe"
   nssm set Nginx AppDirectory C:\nginx
   nssm start Nginx
   ```

### Verify the installation

After you start SmartHive, verify that it's running correctly.

1. Open a browser, and go to your SmartHive URL (for example, `http://support.yourcompany.com`).
2. Confirm that the SmartHive sign-in page appears.
3. Sign in with the default admin credentials:
   - Email: `admin@SmartHive.local`
   - Password: `SmartHive@Admin123`
4. Check the service status.

   On Linux, run:

   ```bash
   sudo systemctl status SmartHive
   ```

   On Windows Server, run:

   ```powershell
   nssm status SmartHive
   nssm status Nginx
   ```

> **Important:** Change the default admin password immediately after you sign in for the first time. Select **Profile settings** > **Change password**.

---

## Post-installation setup

### Configure SSL

> **Important:** SSL is required for all production deployments. Don't skip this step.

#### Linux (Let's Encrypt)

1. Install Certbot:

   ```bash
   sudo apt install -y certbot python3-certbot-nginx
   ```

2. Get an SSL certificate:

   ```bash
   sudo certbot --nginx -d support.yourcompany.com
   ```

3. Follow the prompts. Certbot configures Nginx to use the certificate and sets up automatic renewal.
4. Verify automatic renewal:

   ```bash
   sudo certbot renew --dry-run
   ```

#### Windows Server

1. Get an SSL certificate from your preferred certificate authority. Save the certificate file and private key file to `C:\nginx\ssl`.
2. Open `C:\nginx\conf\nginx.conf` in an editor, and replace the `server` block with the following configuration. Change the file names to match your certificate files.

   ```nginx
   server {
       listen 80;
       server_name support.yourcompany.com;
       return 301 https://$host$request_uri;
   }

   server {
       listen 443 ssl;
       server_name support.yourcompany.com;

       ssl_certificate C:/nginx/ssl/support.yourcompany.com.crt;
       ssl_certificate_key C:/nginx/ssl/support.yourcompany.com.key;

       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

3. Test the configuration, and then restart Nginx:

   ```powershell
   cd C:\nginx
   .\nginx.exe -t
   nssm restart Nginx
   ```

### Set up email

SmartHive sends email for case notifications, invitations, and password resets.

1. Sign in to SmartHive as an admin.
2. Select **Settings** > **Email** > **SMTP configuration**.
3. Enter your SMTP server details:

   | Field | Description |
   |---|---|
   | **SMTP host** | Your SMTP server address |
   | **SMTP port** | Typically 587 (TLS) or 465 (SSL) |
   | **Username** | Your SMTP authentication user name |
   | **Password** | Your SMTP authentication password |
   | **From address** | The email address that SmartHive sends mail from |
   | **From name** | The display name for outgoing email (for example, `SmartHive Support`) |
   | **Encryption** | TLS or SSL |

4. Select **Send test email** to verify the configuration.
5. Select **Save**.

### Configure single sign-on

With single sign-on (SSO), your team members can sign in to SmartHive by using their existing company credentials. SmartHive supports SSO through SAML 2.0 and OAuth 2.0. This section describes how to configure SAML 2.0.

> **Important:** Test SSO in a separate browser session before you turn it on. If SSO is misconfigured and you turn it on, you might be locked out of SmartHive.

#### SAML 2.0

1. Select **Settings** > **Security** > **Single sign-on**.
2. Select **SAML 2.0**.
3. Copy the **SmartHive ACS URL** and **Entity ID**, and give them to your identity provider (for example, Okta, Microsoft Entra ID, or Google Workspace).
4. Enter the following details from your identity provider:

   | Field | Description |
   |---|---|
   | **SSO URL** | The SAML SSO URL from your identity provider |
   | **Entity ID** | The entity ID from your identity provider |
   | **Certificate** | The X.509 certificate from your identity provider |

5. Select **Test configuration** to verify that SSO works.
6. Select **Enable SSO**.

### Set up backups

For self-hosted deployments, set up regular backups of your SmartHive database.

#### Database backup (Linux)

1. Create the backup script file:

   ```bash
   sudo nano /opt/SmartHive/scripts/backup.sh
   ```

2. Add the following content to the file:

   ```bash
   #!/bin/bash
   BACKUP_DIR="/var/backups/SmartHive"
   DATE=$(date +%Y%m%d_%H%M%S)
   mkdir -p "$BACKUP_DIR"
   sudo -u postgres pg_dump SmartHive | gzip > "$BACKUP_DIR/SmartHive_$DATE.sql.gz"
   find "$BACKUP_DIR" -name "*.sql.gz" -mtime +30 -delete
   ```

   The script runs `pg_dump` as the `postgres` user, so it doesn't prompt for a password. The script also deletes backups that are older than 30 days.

3. Make the script executable, and open the crontab:

   ```bash
   sudo chmod +x /opt/SmartHive/scripts/backup.sh
   sudo crontab -e
   ```

4. Add the following line to run the backup every day at 2:00 AM:

   ```
   0 2 * * * /opt/SmartHive/scripts/backup.sh
   ```

#### Database backup (Windows Server)

> **Important:** The backup script contains the database password. Restrict access to the script to administrators.

1. Create the backup script file:

   ```powershell
   New-Item -ItemType Directory -Force C:\SmartHive\scripts
   notepad C:\SmartHive\scripts\backup.ps1
   ```

2. Add the following content to the file. Replace `your_password` with the password that you set for `SmartHiveuser`.

   ```powershell
   $BackupDir = "C:\Backups\SmartHive"
   $Date = Get-Date -Format "yyyyMMdd_HHmmss"
   New-Item -ItemType Directory -Force -Path $BackupDir | Out-Null
   $env:PGPASSWORD = "your_password"
   & "C:\Program Files\PostgreSQL\14\bin\pg_dump.exe" -U SmartHiveuser -h localhost -F c -f "$BackupDir\SmartHive_$Date.backup" SmartHive
   Get-ChildItem $BackupDir -Filter "*.backup" | Where-Object { $_.LastWriteTime -lt (Get-Date).AddDays(-30) } | Remove-Item
   ```

3. Schedule the script to run every day at 2:00 AM:

   ```powershell
   schtasks /create /tn "SmartHive backup" /tr "powershell.exe -ExecutionPolicy Bypass -File C:\SmartHive\scripts\backup.ps1" /sc daily /st 02:00 /ru SYSTEM
   ```

> **Tip:** Store backups in a different location from your SmartHive server, such as an offsite storage service like Amazon S3 or Azure Blob Storage.

---

## Upgrade SmartHive

### Upgrade a cloud deployment

SmartHive Cloud updates automatically, so you don't need to take any action. SmartHive publishes release notes for all updates in the [SmartHive Release Notes](#).

### Upgrade a self-hosted deployment

> **Warning:** Always back up your database before you upgrade. See [Set up backups](#set-up-backups).

#### Linux

1. Stop the SmartHive service:

   ```bash
   sudo systemctl stop SmartHive
   ```

2. Get the latest version:

   ```bash
   cd /opt/SmartHive
   sudo git pull origin main
   ```

3. Install the updated dependencies:

   ```bash
   sudo -u SmartHive npm install --omit=dev
   ```

4. Run the database migrations:

   ```bash
   sudo -u SmartHive npm run db:migrate
   ```

5. Start the SmartHive service:

   ```bash
   sudo systemctl start SmartHive
   ```

#### Windows Server

1. Stop the SmartHive service:

   ```powershell
   nssm stop SmartHive
   ```

2. Get the latest version:

   ```powershell
   cd C:\SmartHive
   git pull origin main
   ```

3. Install the updated dependencies:

   ```powershell
   npm install --omit=dev
   ```

4. Run the database migrations:

   ```powershell
   npm run db:migrate
   ```

5. Start the SmartHive service:

   ```powershell
   nssm start SmartHive
   ```

---

## Uninstall SmartHive

### Delete a cloud workspace

> **Warning:** Deleting your SmartHive workspace permanently removes all cases, contacts, projects, and configuration. You can't undo this action. Export your data before you delete the workspace.

1. Select **Settings** > **Workspace** > **Danger zone**.
2. Select **Delete workspace**.
3. Type your workspace name to confirm.
4. Select **Delete permanently**.

### Uninstall from Linux

1. Stop and disable the SmartHive service:

   ```bash
   sudo systemctl stop SmartHive
   sudo systemctl disable SmartHive
   sudo rm /etc/systemd/system/SmartHive.service
   sudo systemctl daemon-reload
   ```

2. Remove the SmartHive files:

   ```bash
   sudo rm -rf /opt/SmartHive
   ```

3. Drop the SmartHive database and user:

   ```bash
   sudo -i -u postgres psql -c "DROP DATABASE SmartHive;"
   sudo -i -u postgres psql -c "DROP USER SmartHiveuser;"
   ```

4. Remove the Nginx configuration:

   ```bash
   sudo rm /etc/nginx/sites-enabled/SmartHive
   sudo rm /etc/nginx/sites-available/SmartHive
   sudo systemctl restart nginx
   ```

5. Remove the SmartHive system user:

   ```bash
   sudo userdel SmartHive
   ```

### Uninstall from Windows Server

1. Stop and remove the SmartHive service:

   ```powershell
   nssm stop SmartHive
   nssm remove SmartHive confirm
   ```

2. Remove the SmartHive files:

   ```powershell
   Remove-Item -Recurse -Force C:\SmartHive
   ```

3. Drop the SmartHive database by using pgAdmin or the PostgreSQL command line.
4. Stop and remove the Nginx service, and then remove the Nginx files:

   ```powershell
   nssm stop Nginx
   nssm remove Nginx confirm
   Remove-Item -Recurse -Force C:\nginx
   ```

---

## Troubleshooting

### SmartHive doesn't start

The SmartHive service fails to start or returns an error. To fix the problem:

1. Check the SmartHive service logs.

   On Linux, run:

   ```bash
   sudo journalctl -u SmartHive -n 100
   ```

   On Windows Server, run:

   ```powershell
   Get-EventLog -LogName Application -Source SmartHive -Newest 50
   ```

2. Verify that PostgreSQL and Redis are running.

   On Linux, run:

   ```bash
   sudo systemctl status postgresql
   sudo systemctl status redis-server
   ```

   On Windows Server, run:

   ```powershell
   Get-Service postgresql*, Memurai
   ```

3. Check that the `.env` file contains valid database credentials and that the database exists.

---

### Can't connect to the database

SmartHive starts but displays a database connection error. To fix the problem:

1. Verify that the database credentials in your `.env` file match the credentials you set in PostgreSQL.
2. Confirm that PostgreSQL is running and accepting connections on the configured host and port.
3. Check that the `SmartHiveuser` user has the correct privileges by running:

   ```sql
   GRANT ALL PRIVILEGES ON DATABASE SmartHive TO SmartHiveuser;
   ```

---

### SSL certificate errors

Browsers display a security warning when you access SmartHive. To fix the problem:

1. Verify that your SSL certificate is valid and hasn't expired.
2. Confirm that the certificate is issued for the correct domain.
3. On Linux, check that Certbot configured Nginx correctly:

   ```bash
   sudo nginx -t
   sudo certbot certificates
   ```

---

### Email notifications aren't sending

SmartHive isn't sending invitation emails, case notifications, or password reset emails. To fix the problem:

1. Select **Settings** > **Email** > **SMTP configuration**.
2. Select **Send test email**, and check whether the email is delivered.
3. Verify your SMTP credentials and port settings.
4. Check that your firewall allows outbound connections on port 587 or 465.
5. Check your SMTP server logs for authentication or delivery errors.

---

### Can't sign in after you turn on SSO

You're locked out of SmartHive after you turn on SSO. To fix the problem:

1. Go to the emergency admin URL:

   ```
   https://yourworkspace.SmartHive.io/admin/login
   ```

2. Sign in with your admin email and password. This sign-in bypasses SSO.
3. Select **Settings** > **Security** > **Single sign-on**, and then turn off SSO.
4. Reconfigure your SSO settings, and test them before you turn SSO on again.

---

*This document is part of the [technical-writing-portfolio](./README.md). SmartHive is a fictional product created for the [technical-writing-portfolio](./README.md) repository.*
