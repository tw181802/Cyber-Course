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



## Deploying an App with Docker (Web App Pentest Example)

### Pulling an Image from Docker Hub
1. **Find the Image**  
   You can find images like Magento on Docker Hub. However, be cautious, as some images may contain malware. Always verify the source of the image.

   ![IMG_1184](https://github.com/user-attachments/assets/db723b56-5e74-4993-9394-b2ebbc4b4759)



3. **Pull the Latest Image**  
   To pull the latest version of an image, use:
   
 
![IMG_1186](https://github.com/user-attachments/assets/35074f37-7d3b-4a21-99d9-73d599fae300)

# Docker Container Security and Deployment Guide

## Securing the Container
Refer to the [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) for best practices in securing Docker containers.

![IMG_1185](https://github.com/user-attachments/assets/c1e3abeb-80b1-44cf-abd7-afbd790a672d)


## Deploying an Application with Docker Compose

### Using a Docker Compose File
To deploy Magento or any other application with Docker Compose, follow these steps:

1. **Download the `docker-compose.yml` File**  
   Use `curl` to download the required Docker Compose file:
 
   `curl -sSL https://raw.githubusercontent.com/hitnami/containers/main/bitnami/magento/docker-compose.yml -o docker-compose.yml`
   Afterward > vim docker-compose.yml and paste it
![IMG_1187](https://github.com/user-attachments/assets/0286de9c-bef0-4ece-9c36-e875583bcc1f)

   
# Deploy the Application

After modifying the file, deploy the container using Docker Compose:
docker-compose up -d

![IMG_1188](https://github.com/user-attachments/assets/d775b0a3-09da-4d28-a2ae-382ae4c1c598)



## Access the Application

Once the container is up and running, navigate to the following URL to access the Magento installation page:

[http://localhost:8000](http://localhost:8000)

![IMG_1189](https://github.com/user-attachments/assets/2474de09-f559-4418-b6b8-2eea7fc9fad4)

# Managing Containers

## Listing Running Containers

To view a list of running containers, use the following command:

![IMG_1190](https://github.com/user-attachments/assets/bf333905-a711-4fbd-a458-fb2ae0f0ceec)

`docker ps`

### To drop into a containter

![IMG_1191](https://github.com/user-attachments/assets/c3d38276-9d29-4ee6-875d-bda564c59246)

## Stopping a Running Container

To stop a running container, first grab its container ID from the docker ps list, then use the following command:

`sudo docker stop <containerID>`





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
1. **Copy the `docker-compose.yml` File for WordPress**  
![IMG_1193](https://github.com/user-attachments/assets/a196f682-317e-4604-9e31-1eb6bf8c9bd8)

2. **Paste the `docker-compose.yml` File for WordPress**
 ![IMG_1195](https://github.com/user-attachments/assets/1da3bfdd-03c3-4321-a125-cc2d559fec54)
![IMG_1194](https://github.com/user-attachments/assets/cc034d55-bea8-43dd-8b90-bf01cd82e00c)

## Deploy WordPress
You can use a custom plugin or other techniques to establish a foothold in the target system.

![IMG_1196](https://github.com/user-attachments/assets/5b738129-c66c-4434-8ef1-b1e77e8e2648)
## Access the Application

Once the container is up and running, navigate to the following URL to access the Magento installation page:

[http://localhost:8000](http://localhost:8000)

![IMG_1197](https://github.com/user-attachments/assets/8eed7be7-7fe4-41d3-a713-132e0db9c13f)

![IMG_1198](https://github.com/user-attachments/assets/c3cb78f7-e0c1-4bd0-a3fc-ce58cefcd41d)


### Setup the Account
![IMG_1199](https://github.com/user-attachments/assets/5cb5b5bf-5b0d-4c16-87b9-49cc1857317b)
![IMG_1201](https://github.com/user-attachments/assets/e52c30f8-9c54-41eb-8e36-766cea4eaa8b)
![IMG_1203](https://github.com/user-attachments/assets/f41586d8-5fd0-4e6d-9223-6784cbf9e941)
![IMG_1202](https://github.com/user-attachments/assets/b5926f39-5808-461b-8b61-b80dfe7b94bf)

### Can see the Process Running

![IMG_1200](https://github.com/user-attachments/assets/4852ecd2-0faa-4f32-91ed-32c6b38f1d17)

### Drop into the Interactive Shell

![IMG_1204](https://github.com/user-attachments/assets/3ce1d641-6edd-43ec-882a-2472e254fb6b)


## Change directory to plugins

![IMG_1205](https://github.com/user-attachments/assets/5f2c7749-e5b7-48c3-ae7f-65dcb320a72f)

## To Find Info on How to Create a WordPress Plugin
# Privilege Escalation via WordPress Plugin

## Developing a Custom Plugin

### Create the Plugin Code
Example plugin code can be obtained from resources like Alexa AppSecExplained. Copy and paste the plugin code into a new file:

`nano <plugin-name>.php`

![IMG_1206](https://github.com/user-attachments/assets/ce23242f-5aec-43fe-8535-a7927cf9935f)


### We need to create it using PHP 
![IMG_1207](https://github.com/user-attachments/assets/fee8705a-a8db-43e6-8dab-c70dda494ae7)
![IMG_1208](https://github.com/user-attachments/assets/6c9183c7-4a36-45cc-9ead-9691455a2b92)
![IMG_1209](https://github.com/user-attachments/assets/cbd51143-f3ca-41f4-be49-acc93461ddbe)



### Once we create we navigate to our WordPress Instance and Activate the Plugin

![IMG_1211](https://github.com/user-attachments/assets/dd0790a2-8ab0-44cb-96e8-0959747bc37c)
![IMG_1210](https://github.com/user-attachments/assets/68d233b0-951f-4031-9880-49b1ff1f623b)

### This is what it look liked before our Plugin was there
![IMG_1212](https://github.com/user-attachments/assets/000ebea0-63b3-4c1b-b1b9-2494af3a1d9d)

### As you can see we have a security vulnerability where it shows 

![IMG_1213](https://github.com/user-attachments/assets/c8cbb764-294b-46f3-9c46-046868afe4b7)

### Setup Ubuntu Server (TryHackMe only supports ubuntu 20, not 22)
![IMG_1216](https://github.com/user-attachments/assets/5c180304-ae85-4f6b-840f-f20f248a469d)

### Once Setup we can ssh into that sever
![IMG_1218](https://github.com/user-attachments/assets/20b0ee65-f3c8-40c5-b463-dc6cb739fea9)
![IMG_1219](https://github.com/user-attachments/assets/582ba392-9de9-4e9d-a549-32b119f60b36)

![IMG_1221](https://github.com/user-attachments/assets/f28becdd-85e7-4994-b816-9ba6ffac63db)

## Add user and configure ssh keys
![IMG_1227](https://github.com/user-attachments/assets/4766d41d-2001-4f41-a186-76095b97f4da)
![IMG_1228](https://github.com/user-attachments/assets/238bc48d-f8ae-413d-90eb-d3fdda86b48b)
![IMG_1229](https://github.com/user-attachments/assets/3fdf91dd-1077-4acd-8320-36c3af0ef90d)
![IMG_1230](https://github.com/user-attachments/assets/5672bdc1-4be6-48c7-8822-afd78c34ac90)
![IMG_1231](https://github.com/user-attachments/assets/14fe9893-9abe-44b6-bb1d-f8b87d0d733a)
![IMG_1236](https://github.com/user-attachments/assets/83d19a3d-85c3-41df-bb04-454c21aec910)
![IMG_1237](https://github.com/user-attachments/assets/7b0a3a9b-4adf-4158-9ed8-ee906a15f2f6)
![IMG_1238](https://github.com/user-attachments/assets/2b8b1c5c-cf01-4879-a0fc-806febf06cb2)


### switch to root
![IMG_1232](https://github.com/user-attachments/assets/bb7ccffe-15b2-47c0-b4d8-3f1d1c6690fe)


### Now we can see ubuntu default page and navigate to wordpress directory

![IMG_1222](https://github.com/user-attachments/assets/92efc2dd-1d73-44c6-bf17-61bf5ac12e48)

### Lets Configure
![IMG_1223](https://github.com/user-attachments/assets/423dcaad-180e-4766-a1a2-9288185974ab)

![IMG_1226](https://github.com/user-attachments/assets/33507a45-fcdb-4bfd-bf5f-c41a7d5786f7)



### Configure the Database

![IMG_1224](https://github.com/user-attachments/assets/7fdb9039-3d2b-478b-b099-af7ff05c58ac)








## Privilege Escalation
Privilege escalation can be achieved by exploiting vulnerabilities such as:
- SUID bits
- Moving sensitive files like `/root/.ssh` or `/etc/shadow`


# Setting Up WordPress on Ubuntu

## Steps for Setting Up WordPress

### Install Required Packages
`Use the following commands to install Apache, MySQL, and PHP on Ubuntu:`

`
sudo apt update
sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql php-gd php-cli php-curl php-xml`


### Set up MySQL for Wordpress
`
sudo mysql_secure_installation
sudo mysql
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;`

`cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar xzvf latest.tar.gz
sudo cp -a wordpress/./var/www/html`

### Configure Apache
`sudo vim /etc/apache2/sites-available/wordpress.conf`



### Restart Apache
`sudo a2ensite wordpress.conf`
`sudo systemctl restart apache2`



### Testing Plugin Vulnerabilities
Test the plugin for vulnerabilities. Common issues to check for:
- Improper input handling
- Insecure file permissions
- Code injection vulnerabilities


# Final Setup and Testing



![IMG_1242](https://github.com/user-attachments/assets/9e35c5b2-cd0e-4388-9929-afb4651e69be)
![IMG_1241](https://github.com/user-attachments/assets/5311743c-3a26-4d47-aef9-91c85959abfe)
![IMG_1240](https://github.com/user-attachments/assets/10f419b8-8d06-42b9-a6a4-13a440720301)
![IMG_1239](https://github.com/user-attachments/assets/94ac713f-decd-4924-a86a-32d6f4180ed5)


## Testing with WPScan

### Scan for WordPress Vulnerabilities
Use WPScan to scan your WordPress site for vulnerabilities:

`wpscan --url http://<server-ip>/wordpress --enumerate u`


### Obtain Credentials
WPScan can help identify known vulnerabilities, including credential leaks. Use the credentials discovered to log in.

### Privilege Escalation
After logging in, explore the site for potential privilege escalation vectors, such as insecure plugins, misconfigured settings, or file system vulnerabilities.


#### UPload the Try Hack Me Steps:
![IMG_1244](https://github.com/user-attachments/assets/1bc326ed-b0ad-4503-925a-e552b6f2c647)
![IMG_1243](https://github.com/user-attachments/assets/8290bd2a-374d-4532-822b-e05a50a41178)





