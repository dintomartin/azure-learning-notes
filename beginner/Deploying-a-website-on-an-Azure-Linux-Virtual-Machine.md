Deploying a website on an Azure Linux Virtual Machine

🚀 Overview
A concise tutorial on deploying a simple static website (like a personal portfolio) on an Azure Linux VM using Ubuntu 20.04 and Apache.
------------------------------------------------------
✅ Step-by-Step Guide

1. Create an Azure Account
Sign up or log in at the Azure Portal.
------------------------------------------------------
2. Provision a Linux VM
- Navigate to Virtual Machines → Create → Azure Virtual Machine.
- BASIC settings:
    - Resource Group & VM name: choose your own
    - Region: your preferred location
    - Image: Ubuntu Server 20.04 LTS
    - Size: per your requirements
    - Authentication: SSH public key (generate new key pair)
- Leave other settings as default, review, then Create.
- Download the .pem private key securely (Azure won't keep it).
------------------------------------------------------
3. SSH from Windows (if applicable)
- Install PuTTY.
- Convert the `.pem` to `.ppk` using PuTTYgen.
- Load the `.ppk` in PuTTY under SSH → Auth, set the host as `username@public_ip`, port 22, and connect.
------------------------------------------------------
4. Install Apache
Once logged in:
```bash
sudo apt update
sudo apt upgrade
sudo apt install apache2 -y
```
------------------------------------------------------
5. Configure Network
In the Azure Portal under your VM’s Networking:
- Add an inbound rule:
    - Source: Any
    - Port: HTTP (80)
    - Allow access.
Verify you can see Apache’s default page using the VM’s public IP.
------------------------------------------------------
6. Deploy Your Static Website
```bash
git clone https://github.com/kiena-dev/kiena-web.git
cd kiena-web
sudo rm /var/www/html/index.html
sudo cp -r * /var/www/html
sudo chown -R www-data:www-data /var/www/html
ls /var/www/html
```
This clones the sample repository, replaces the default Apache files, and serves your static content.
------------------------------------------------------
7. Go Live
Visit `http://<your-vm-public-ip>` to view your site.
------------------------------------------------------
🧠 Summary
- ✅ Create an Ubuntu VM in Azure.
- 🔐 Set up SSH access and install Apache.
- 🌐 Open port 80 via the VM's Networking settings.
- 📤 Clone your site’s repo into `/var/www/html`.
- 🎉 Visit your public IP to check it’s live.
------------------------------------------------------
