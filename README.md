# 📌 Peppermint Help Desk Ticketing System

## 📖 Description
This project provides a guide to setting up a **simple help desk ticketing system** using **Peppermint**. The tutorial covers both **self-hosting options**:
- **Cloud-based setup** (e.g., Linode)
- **Local hardware setup** (e.g., server, NAS, or spare laptop)

This guide is ideal for learning about **ticket documentation** and gaining **IT hands-on experience**. The system can be used for **personal or professional** purposes.

## 🚀 Features
- User-friendly **ticketing system**
- Supports **cloud and local hosting**
- Runs on **Docker** for easy deployment
- Simple **web-based access**

## 🏗️ Tech Stack
- **Languages**: YAML (Docker Compose)
- **Frameworks**: Docker, Docker Compose
- **Database**: Built-in database (via container)
- **Hosting Options**: Cloud (Linode) or Local (server, NAS, spare laptop)

## 📂 Installation

### 🏢 **Cloud-Based Setup (Linode)**
Setting up Peppermint:
1. Create a Le Node Account: If you're new to Le Node, use the link in the video description for a $100 credit for 60 days.
2. Create a Le Node: After logging in, click "Create" then "Le Node".
3. Use Marketplace: Click on "marketplace".
4. Select Peppermint: Search for "peppermint".
5. Configure Peppermint: Choose an image (like Ubuntu), select a region close to you, and pick a plan (the NAU one gigabyte plan is $5/month).
6. Label and Create: Label the node, set a password, and click "create".
7. Monitor Installation: Use the Lish console to watch the installation.
8. Access Peppermint: Once ready, log in to the Lish console with the root and password you set.
9. Verify Docker Container: Type Docker ps to confirm the Docker container is running and note the port being used (5001).
10. Access in Browser: Get the reverse DNS name from the network tab, and paste it into a new tab with the port number (e.g., yourDNS:5001).

Installing Peppermint Elsewhere (Locally):
1. Install Docker and Docker Compose
```
sudo apt install docker.io docker-compose -y
```
2. Create a directory for Peppermint
```
mkdir peppermint && cd peppermint
```
3. Create a Docker Compose file
```
nano docker-compose.yml
```
4. Paste the Docker Compose configuration below and save
## 📂 Docker Compose Configuration

```yaml
version: "3.1"

services:
  peppermint_postgres:
    container_name: peppermint_postgres
    image: postgres:latest
    restart: always
    ports:
      - 5432:5432
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: peppermint
      POSTGRES_PASSWORD: 1234
      POSTGRES_DB: peppermint

  peppermint:
    container_name: peppermint
    image: pepperlabs/peppermint:latest
    ports:
      - 3000:3000
      - 5003:5003
    restart: always
    depends_on:
      - peppermint_postgres
    environment:
      DB_USERNAME: "peppermint"
      DB_PASSWORD: "1234"
      DB_HOST: "peppermint_postgres"
      SECRET: 'peppermint4life'

volumes:
  pgdata:
```
5. Ensure Docker and Docker compose is installed:
```
sudo apt install docker.io docker-compose -y
```
6. Clone the repository (or create a new directory for the project):
```
git clone https://github.com/your-repo/peppermint-helpdesk.git
cd peppermint-helpdesk
```
7. Run Docker Compose
```
docker-compose up -d
```
8. Verify running container
```
docker ps
```
- Check port (5000)
9. Access Peppermint in browser
- Use your IP with the port: `http://yourIP:5000`
- Login with default credentials:
- Username: admin@admin.com
- Password: 1234
10. Stopping the containers
```
docker-compose down
```

