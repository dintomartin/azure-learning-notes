Deploy a static personal portfolio website using Azure Static Web Apps and GitHub

✅ Prerequisites

- A GitHub account with your website code (HTML, CSS, images, etc.)
- A free-tier Azure account
- Your website is a static site (no backend/server-side code)
--------------------------------------------------------------
Push Website Code to GitHub

1. Create a new GitHub repository
    1. Go to https://github.com
    2. Click the + button in the top-right corner → "New repository"
    3. Fill in:
        - Repository name: `portfolio-site` (or any name you like)
        - Public or Private: Your choice
        - Do NOT check "Initialize with a README"
    4. Click "Create repository"
2. Push your website files (HTML, CSS, images) to this repo.
-------------------------------------------------------------
Create Azure Static Web App
✅ Goal:
Create an Azure Static Web App that is connected to your GitHub repository, so your static website is deployed and updated automatically.

🧭 Open Azure Portal

1. Go to: https://portal.azure.com
2. Log in with your Microsoft/Azure account
3. In the search bar at the top, type "Static Web Apps"
4. Click on "Static Web Apps" from the dropdown
5. Click the "+ Create" button
------------------------------------------------
📋Fill in Basic Details

1. Subscription
Choose your Azure subscription (usually the free one if you're on free tier)
2. Resource Group
A resource group is a container for related Azure resources:
- Click "Create new"
- Name it something like `portfolio-rg`
3. Static Web App Name
This is the name of your app in Azure (e.g., `my-portfolio-site`)
4. Hosting Plan
Select `Free`
5. Region
Pick a location near you (e.g., `Central US`, `West Europe`)
Click Next: Deployment >
---------------------------------------------
🔗 Connect to GitHub

Azure now asks to connect to GitHub to pull your code.
1. Sign In to GitHub
Click "Sign in with GitHub" and authorize Azure (if you haven't already)
2. Choose Your Repository
Once signed in:
- Organization: Choose your GitHub username
- Repository: Select the repo you created (e.g., `portfolio-site`)
- Branch: Choose `main`
Click Next: Build >
-------------------------------------------------
🛠 Configure Build Details

For a static HTML/CSS site (no frameworks like React/Vue):
- Build Presets: Select "Custom"
- App Location: Type `.` (dot) → This means the root of your repo
- API Location: Leave blank (you don’t have serverless APIs)
- Output Location: Leave blank
> ⚠️ If your files are inside a folder like /src or /site, then put that folder name instead of .
Click Review + Create
--------------------------------------------------------
✅ Review and Create

1. Review all your inputs
2. Click "Create"
3. Wait a few seconds for deployment to complete
-----------------------------------------------------------
🕒 Let Azure Set Up Deployment

After creation:
1. Go to your new Static Web App in Azure
2. Under the Overview tab, you’ll see the Live UR like:
    https://icy-moss-0ab12340e.1.azurestaticapps.net/
3. Visit the URL to see your live site!
4. Under "Workflow", you’ll notice Azure created a GitHub Actions workflow:
    - In your GitHub repo, check:
        .github/workflows/azure-static-web-apps-<random>.yml
--------------------------------------------------------------
🔄 Automatic Deployment

Every time you:
- Make changes to your HTML, CSS, or images
- Commit and push those changes to GitHub
👉 Azure will automatically redeploy your site within a few minutes!
-----------------------------------------------------------------
