Host a Website on Azure Windows Server Using IIS

🎯 Aim
To deploy a Windows Server virtual machine on Microsoft Azure, 
install Internet Information Services (IIS), 
and host a basic website by uploading HTML content to the server.
------------------------------------------------------------------
📋 Prerequisites

Before starting this project, ensure the following:
1. Azure Account
- An active Microsoft Azure subscription (Free Tier is sufficient for small-scale testing)
2. Basic Knowledge
- Familiarity with:
    - Azure Portal
    - Remote Desktop Protocol (RDP)
    - Basic HTML and file structure of websites
3. Tools & Access
- Remote Desktop client (RDP)
- Website files (HTML, CSS, JS, images)
- A Windows PC or macOS/Linux with RDP support
------------------------------------------------------------------
🛠 Step-by-Step Procedure

🔹 Step 1: Create a Windows Server Virtual Machine (VM)

1. Log in to the Azure Portal
2. Go to Create a resource > Virtual Machine
3. Fill out the basic settings:
    - VM Name: e.g., `MyWindowsVM`
    - Region: Choose closest to you
    - Image: Select `Windows Server 2022 Datacenter`
    - Size: Use B2s (recommended) or B1s (for testing)
    - Admin username and password: Create secure credentials
4. Under Inbound ports, allow:
    - RDP (3389) for remote access
    - HTTP (80) for website traffic
5. Click Review + Create → Then Create
------------------------------------------------------------------
🔹 Step 2: Connect to the VM via RDP

1. After deployment, go to the VM dashboard
2. Click Connect > RDP
3. Download the `.rdp` file and open it
4. Enter the credentials you set during VM creation
5. You are now inside your Windows Server
------------------------------------------------------------------
🔹 Step 3: Install IIS Web Server

Option A: Using Server Manager
1. Open Server Manager
2. Click Add roles and features
3. In the wizard:
    - Role-based installation → Select your server → Check Web Server (IIS)
    - Click Next through all sections → Click Install
4. Wait for installation to finish

Option B: Using PowerShell
1. Open PowerShell as Administrator
2. Run:
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
------------------------------------------------------------------
🔹 Step 3.5: Verify IIS Is Working (Local and External Access)
Before uploading your own website files, verify that IIS is working correctly:

✅ A. Test Locally Inside the VM
1. On the VM (via RDP), open Internet Explorer
2. Visit
    http://localhost
3. You should see the default IIS welcome page
    → “Internet Information Services” or similar
    
✅ B. Test Externally from Your Machine
1. On your local computer, open a browser
2. Go to:
    http://<your-vm-public-ip>
    (You can find this in the Azure VM Overview)
3. You should see the same IIS welcome page

🟢 If both tests work, IIS is installed and the VM firewall rules are correctly set up.
🔴 If external access fails:
- Make sure HTTP (port 80) is allowed in the Inbound Rules of the VM’s Networking settings.
- Also check your local firewall or antivirus software isn't blocking outbound connections.
------------------------------------------------------------------
🔹 Step 4: Upload and Deploy Website Files

1. Navigate to:
    C:\inetpub\wwwroot
2. Delete the default file `iisstart.htm` if present
3. Copy your website files (e.g., `index.html`, CSS, JS) into this folder
4. You can copy files using:
    - Drag and drop in RDP session
    - Copy/paste from local to remote
    - File transfer via FTP (optional setup)
------------------------------------------------------------------
🔹 Step 5: Test the Website

1. Get your VM’s public IP address from Azure Portal
2. Open a web browser on your local machine
3. Visit:
    http://<your-vm-public-ip>
4. You should see your website's homepage

✅ If successful, IIS is serving your content to the web!
------------------------------------------------------------------
📌 Conclusion

By following this project, you have:
- Created a Windows Server VM on Azure
- Installed and configured IIS (Internet Information Services)
- Uploaded and deployed a static website
- Successfully made the site available to the public over the internet
------------------------------------------------------------------
