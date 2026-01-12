Deploy a Dynamic Web App Using Azure App Service

✅ Project Goal -
Deploy a simple dynamic website (e.g., Flask or Node.js app) using Azure App Service, with code hosted on GitHub.
---------------------------------------------------
🧰 Prerequisites
Before you begin, make sure you have:
1. Azure Account
- Sign up for free (https://azure.microsoft.com/en-us/free/) if you don't have one.
2. GitHub
- A GitHub account
3. Sample Web App
Choose a simple backend app (Flask or Node.js). Here’s a Flask example:

`app.py`:
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Azure App Service!"

if __name__ == '__main__':
    app.run()
```

`requirements.txt`:
```
Flask==2.3.3
```

Optional: Add `startup.txt` with:
```
gunicorn --bind=0.0.0.0 --timeout 600 app:app
```

Push this to a GitHub repository.
---------------------------------------------------
🚀 Step-by-Step Guide

🔸 Step 1: Create an Azure App Service
1. Go to Azure Portal
2. Search for "App Services"
3. Click "Create"

Fill in the basic details:

| Field | Value |
| --- | --- |
| Subscription | Select your subscription |
| Resource Group | Create or choose one (e.g., `my-webapp-rg`) |
| Name | Unique name for your app (e.g., `myflaskwebapp123`) |
| Publish | Code |
| Runtime Stack | Python 3.11 (or Node.js if using that) |
| Region | Closest to you |

Click Next > Next > Review + Create > Create
---------------------------------------------------
🔸 Step 2: Configure Deployment from GitHub

Once the App Service is created:
1. Go to the newly created App Service
2. In the left menu, find Deployment Center
3. Choose:
    - Source: GitHub
    - Build provider: GitHub Actions
    - Organization/Repo/Branch: Choose your repo and main/master branch
4. Click Save

Azure will auto-create a GitHub Actions workflow file and start deploying your app.
---------------------------------------------------
🔸 Step 3 : Test the Web App
1. Go to Overview
2. Copy the URL under “Default domain” (e.g., `https://myflaskwebapp123.azurewebsites.net`)
3. Open it in a browser

You should see: "Hello from Azure App Service!"
---------------------------------------------------
📁 Folder Structure Recap (for Flask)

```
your-project/
├── app.py
├── requirements.txt
└── .github/
    └── workflows/
        └── your-deployment.yml (auto-created by Azure)

```
---------------------------------------------------
🧠 What You Learn from This Project
✅ How Azure App Service simplifies web hosting
✅ GitHub Actions for CI/CD
✅ Deploying Python or Node.js apps to the cloud
---------------------------------------------------
