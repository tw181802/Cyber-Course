# Docker 101: Deploy, Scale, and Manage Apps Using Containers

This guide introduces the fundamentals of Docker and walks you through deploying applications, including security tips and practical examples related to web app penetration testing.

## Docker Concepts

- **Images**: Lightweight, portable packages that contain everything needed to run software (code, libraries, dependencies, etc.).
- **Containers**: Running instances of Docker images. Containers are isolated, lightweight, and portable.
- **Daemon**: A background process that manages and maintains containers on a system.

### Benefits of Docker
- **Resource Efficiency**: Containers share the host operating system kernel, reducing resource overhead.
- **Isolation**: Containers run independently, ensuring that applications are isolated from one another.
- **Portability**: Docker containers can be easily moved between different environments (development, staging, production).

### Drawbacks of Docker
- **Container Management**: Managing multiple containers in a large-scale environment can become complex and challenging.

---

## Deploying an App with Docker (Web App Pentest Example)

### Pulling an Image from Docker Hub
1. **Find the Image**  
   You can find images like Magento on Docker Hub. However, be cautious, as some images may contain malware. Always verify the source of the image.

2. **Pull the Latest Image**  
   To pull the latest version of an image, use:
   ```bash
   docker pull <image-name>:latest

# Docker Container Security and Deployment Guide

## Securing the Container
Refer to the [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) for best practices in securing Docker containers.

---

## Deploying an Application with Docker Compose

### Using a Docker Compose File
To deploy Magento or any other application with Docker Compose, follow these steps:

1. **Download the `docker-compose.yml` File**  
   Use `curl` to download the required Docker Compose file:
   ```bash
   curl -sSL https://raw.githubusercontent.com/hitnami/containers/main/bitnami/magento/docker-compose.yml -o docker-compose.yml

# Deploy the Application

After modifying the file, deploy the container using Docker Compose:
```bash
docker-compose up -d




## Access the Application

Once the container is up and running, navigate to the following URL to access the Magento installation page:

[http://localhost:8000](http://localhost:8000)

# Managing Containers

## Listing Running Containers

To view a list of running containers, use the following command:


docker ps



## Stopping a Running Container

To stop a running container, first grab its container ID from the docker ps list, then use the following command:

sudo docker stop <containerID>





# Capture The Flag (CTF) Steps

## Planning

### Decide on Tech Stack & OS
Choose the operating system (e.g., Ubuntu) and the tech stack (e.g., WordPress, custom plugins) for your CTF setup.

### Build & Test Privilege Escalation (Priv Esc)
Identify possible privilege escalation techniques and test them in a safe environment.

### Deploy the Box
Set up the target environment, including services and configurations necessary for the CTF.

## Testing

### Cleanup
Always ensure that you perform cleanup after testing to remove sensitive data and prevent leaks.



# Foothold (e.g., WordPress)

## Deploy WordPress
You can use a custom plugin or other techniques to establish a foothold in the target system.

## Privilege Escalation
Privilege escalation can be achieved by exploiting vulnerabilities such as:
- SUID bits
- Moving sensitive files like `/root/.ssh` or `/etc/shadow`


# Setting Up WordPress on Ubuntu

## Steps for Setting Up WordPress

### Install Required Packages
Use the following commands to install Apache, MySQL, and PHP on Ubuntu:


sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-gd php-cli php-curl php-xml


### Set up MySQL for Wordpress

sudo mysql_secure_installation
sudo mysql
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;

cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar xzvf latest.tar.gz


### Configure Apache
sudo vim /etc/apache2/sites-available/wordpress.conf



### Restart Apache
sudo a2ensite wordpress.conf
sudo systemctl restart apache2


---

# Install WordPress

## Navigate to WordPress Setup Page
Open your browser and go to:

http://<server-ip>/wordpress


## Complete the WordPress Installation
Follow the WordPress installation wizard to complete the setup. Choose the site title, admin username (e.g., "Jeremy"), email, and password.



# Privilege Escalation via WordPress Plugin

## Developing a Custom Plugin

### Create the Plugin Code
Example plugin code can be obtained from resources like Alexa AppSecExplained. Copy and paste the plugin code into a new file:

nano <plugin-name>.php



### Activate the Plugin
After saving the plugin file, navigate to the WordPress plugin section in the GUI and activate your plugin.

### Testing Plugin Vulnerabilities
Test the plugin for vulnerabilities. Common issues to check for:
- Improper input handling
- Insecure file permissions
- Code injection vulnerabilities

---

# Final Setup and Testing

## Testing with WPScan

### Scan for WordPress Vulnerabilities
Use WPScan to scan your WordPress site for vulnerabilities:

wpscan --url http://<server-ip>/wordpress --enumerate u


### Obtain Credentials
WPScan can help identify known vulnerabilities, including credential leaks. Use the credentials discovered to log in.

### Privilege Escalation
After logging in, explore the site for potential privilege escalation vectors, such as insecure plugins, misconfigured settings, or file system vulnerabilities.








