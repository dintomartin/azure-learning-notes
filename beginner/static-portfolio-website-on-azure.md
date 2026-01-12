Static Portfolio Website on Azure

✅ Requirements
Before you begin, make sure you have:
- An Azure account
- A basic portfolio site (HTML, CSS, JS files)
----------------------------------------------
🛠 Step 1: Prepare Your Static Website Files
1. Create a folder, e.g., `portfolio-site/`.
2. Inside it, put your files:
    pgsql
    CopyEdit
    index.html
    styles.css
    script.js
    images/ (folder with any images)
3. Test locally by opening `index.html` in a browser.
------------------------------------------------------
☁️ Step 2: Create an Azure Storage Account
1. Go to the Azure Portal.
2. Click Create a resource > Storage account.
3. Fill in the required fields:
    - Subscription: Your active one
    - Resource group: Create or select one
    - Storage account name: Must be globally unique (e.g., `yournameportfolio`)
    - Region: Choose closest to your audience
    - Performance: Standard
    - Redundancy: LRS (Locally-redundant storage)
4. Click Review + Create > Create
--------------------------------------------------
🌍 Step 3: Enable Static Website Hosting
1. After deployment, go to your Storage account.
2. In the left sidebar, scroll to Data management > Click Static website.
3. Enable Static website.
4. Set:
    - Index document name: `index.html`
    - (Optional) Error document path: `404.html` (if you have one)
5. Click Save
6. Copy the Primary endpoint URL — this is your website’s public URL.
---------------------------------------------------------------------
📂 Step 4: Upload Your Website Files
Use Azure Portal (GUI)
1. Go to Storage Account > Containers > Click on `$web` (auto-created for static hosting).
2. Click Upload and add your `index.html`, `styles.css`, etc.
3. Maintain folder structure for assets (e.g., upload `images/` if used).
❌ Unfortunately, you cannot upload a full folder directly via the Azure Portal UI.
You have to recreate the folder structure manually and upload files inside each folder individually.
🛠 Workaround:
1. Go to `$web` container.
2. Click "Upload" > Select files (not folders).
3. Use the "Advanced" option to set the "Upload to folder" path (e.g., `images/`).
4. Repeat for other folders like `css/`, `js/`, etc.
-------------------------------------------------------
🌐 Step 5: Test Your Site
1. Open the Primary endpoint URL (e.g., `https://yournameportfolio.z13.web.core.windows.net`)
2. You should see your website live.
-------------------------------------
