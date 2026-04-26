GCP IAM Login


To log in and manage Google Cloud IAM (Identity and Access Management), you authenticate to Google Cloud and then configure access permissions for users, groups, or service accounts. IAM controls who can do what on which resources in GCP.

Login via gcloud CLI

1. Install gcloud CLI Download and install the Google Cloud SDK on your system.

2. Authenticate Your Account
gcloud auth login

After login, credentials are stored locally for CLI use.



3. Set the Active Project
gcloud config set project <PROJECT_ID>	



Login via Service Account (Non-Interactive)

1. Create a Service Account In the IAM & Admin console, create a service account and assign it the required roles.

2. Download the Key File Save the JSON key file securely.

3. Authenticate Using the Key File

gcloud auth activate-service-account SERVICE_ACCOUNT_EMAIL \
--key-file=/path/to/key.json \
--project=PROJECT_ID


This is ideal for automation or CI/CD pipelines.

Verify Authentication

Check active credentials:
gcloud auth list




Best Practices

• Principle of Least Privilege: Assign only necessary roles to users or service accounts.
• Use Service Accounts for Automation: Avoid using personal accounts in scripts.
• Enable MFA: Add multi-factor authentication for human users for better security.
• Regular Audits: Review IAM policies and Cloud Audit Logs periodically to detect over-permissioned accounts.

By combining proper login methods with IAM role management, you ensure secure and efficient access control in GCP.



<br>
<br>
<br>


-----------


## 🚀 Deploying Fresh Greens to Google Cloud — Beginner's Guide

Think of it like this: **GitHub Actions builds your app → packages it into a Docker container → ships it to Google Cloud → Google runs it 24/7.**

---

## 🗺️ Big Picture (Read This First)

```
You push code to GitHub
        │
        ▼
GitHub Actions runs (automatic)
   ├── 1. Runs tests
   ├── 2. Builds a Docker image (your app packaged up)
   ├── 3. Uploads image to Google's container storage
   └── 4. Tells Google Cloud Run "use this new image"
                │
                ▼
         Google Cloud Run
         serves your app
         at a public URL 🌍
              │
              ▼
       Cloud SQL (MySQL)
       stores your data
```

---

## 📦 What You Need to Set Up (One-Time)



Step 1.Go to [cloud.google.com](https://cloud.google.com) → Click "Start Free"
- Google gives you **$300 free credits** for 90 days
- You need a credit card (you won't be charged unless you upgrade)

Step 2. Create a Project

---

Download & Install Google Cloud CLI 

[https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)

gcloud auth login	


gcloud config set project <YOUR_PROJECT_ID>	


gcloud services enable run.googleapis.com sqladmin.googleapis.com artifactregistry.googleapis.com cloudbuild.googleapis.com  secretmanager.googleapis.com	
---

Create Your MySQL Database on GCP


Create the database server:

gcloud sql instances create fresh-greens-db --database-version=MYSQL_8_0 --tier=db-f1-micro --region=asia-south1 --root-password= <StrongPassword>	

> ⏳ This takes 5–10 minutes. The `db-f1-micro` tier is the cheapest (~$7/month).



Create the actual database inside that server:

gcloud sql databases create fresh_greens_db --instance=fresh-greens-db	


Create a dedicated app user (don't use root in production):

gcloud sql users create appuser  --instance=fresh-greens-db --password= <AnotherStrongPassword>	

---

Store Your Secrets Safely in GCP

> Instead of hardcoding passwords anywhere, GCP **Secret Manager** stores them securely. Cloud Run reads them at runtime.

Save each secret (run these one by one):


# Your DB connection string — get your instance connection name first:
gcloud sql instances describe fresh-greens-db --format="value(connectionName)"
# It looks like: fresh-greens-prod-123456:asia-south1:fresh-greens-db

# Now create the secrets:
echo -n "jdbc:mysql:///fresh_greens_db?cloudSqlInstance=YOUR_CONNECTION_NAME&socketFactory=com.google.cloud.sql.mysql.SocketFactory&user=appuser&password=AnotherStrongPassword456" | gcloud secrets create DB_URL --data-file=-

echo -n "appuser" | gcloud secrets create DB_USERNAME --data-file=-
echo -n "AnotherStrongPassword456" | gcloud secrets create DB_PASSWORD --data-file=-

echo -n "rzp_live_YOUR_KEY" | gcloud secrets create RAZORPAY_KEY_ID --data-file=-
echo -n "YOUR_RAZORPAY_SECRET" | gcloud secrets create RAZORPAY_KEY_SECRET --data-file=-
echo -n "YOUR_WEBHOOK_SECRET" | gcloud secrets create RAZORPAY_WEBHOOK_SECRET --data-file=-

# Firebase JSON — this uploads the whole file
gcloud secrets create FIREBASE_SERVICE_ACCOUNT_JSON --data-file="app/src/main/resources/firebase-service-account.json"	


---

### **Part 5 — Create a Docker Container Registry**

> Docker is like a ZIP file for your app + Java + everything it needs to run.
> Artifact Registry is Google's private storage for these ZIP files.

gcloud artifacts repositories create fresh-greens --repository-format=docker --location=asia-south1 --description="Fresh Greens container images"	

---

### **Part 6 — Create a Service Account for GitHub Actions**

> GitHub Actions needs permission to deploy to your GCP project. You give it a "key" (Service Account) to authenticate.

**Step 11.**
```powershell
# Create the service account
gcloud iam service-accounts create github-deployer --display-name="GitHub Actions Deployer"	

# Give it the permissions it needs
$PROJECT_ID = gcloud config get-value project	

gcloud projects add-iam-policy-binding $PROJECT_ID --member="serviceAccount:github-deployer@$PROJECT_ID.iam.gserviceaccount.com"  --role="roles/run.admin"	

gcloud projects add-iam-policy-binding $PROJECT_ID --member="serviceAccount:github-deployer@$PROJECT_ID.iam.gserviceaccount.com" --role="roles/artifactregistry.writer"	

gcloud projects add-iam-policy-binding $PROJECT_ID --member="serviceAccount:github-deployer@$PROJECT_ID.iam.gserviceaccount.com"  --role="roles/cloudsql.client"	

gcloud projects add-iam-policy-binding $PROJECT_ID --member="serviceAccount:github-deployer@$PROJECT_ID.iam.gserviceaccount.com" --role="roles/secretmanager.secretAccessor"	

gcloud projects add-iam-policy-binding $PROJECT_ID --member="serviceAccount:github-deployer@$PROJECT_ID.iam.gserviceaccount.com" --role="roles/iam.serviceAccountUser"	

# Download the key as a JSON file
gcloud iam service-accounts keys create gcp-sa-key.json --iam-account="github-deployer@$PROJECT_ID.iam.gserviceaccount.com"	

> ⚠️ **`gcp-sa-key.json` is sensitive — never commit this file!** We'll add it to GitHub Secrets next.

---

### **Part 7 — Add Secrets to GitHub**

**Step 12.** Go to your repo:
👉 `https://github.com/tharun-extinct/Fresh-Greens/settings/secrets/actions`

Click **"New repository secret"** and add:


`GCP_PROJECT_ID` 
`GCP_SA_KEY` 
`GCP_REGION`



> After adding, **delete `gcp-sa-key.json`** from your PC:
> ```powershell
> Remove-Item gcp-sa-key.json
> ```

---

Add `Dockerfile` to Your Project


```dockerfile
Build the JAR

Run the JAR (smaller image, no build tools)
```


> Cloud Run injects a `PORT` env variable — this line makes Spring Boot listen on it.

---

### **Part 9 — Update GitHub Actions Workflow**

Add a `deploy` job to your existing ci.yml — paste this **after** the existing `test` job:

---

Go to:
👉 `https://github.com/tharun-extinct/Fresh-Greens/actions`

You'll see the workflow running. After **~5 minutes** you'll see a green ✅ and a URL like:
```
https://fresh-greens-xxxxxxxx-el.a.run.app
```






❓ Troubleshooting

 | Problem	| Fix |
 |----------|-----|
`Permission denied` on Cloud Run	| Re-check IAM roles in Step 11 
 `Connection refused` to MySQL 	 | Verify `--add-cloudsql-instances` matches your connection name
Firebase not initializing	| Check `FIREBASE_SERVICE_ACCOUNT_JSON` secret has valid JSON
App crashes on startup	| Run `gcloud run logs read --service=fresh-greens --region=asia-south1`




----


<br>
<br>
<br>


**Root cause:** The `GCP_SA_KEY` secret was **not pasted correctly** — Windows PowerShell likely added BOM characters, CRLF line endings, or encoding artifacts when you copied the JSON file. The bytes `o޻wm` are garbled binary, not valid JSON.

---

### Fix — Re-add the Secret Correctly

**Step 1.** Re-download a fresh key (the old one may be corrupted):

```powershell
# Get your project ID
$PROJECT_ID = gcloud config get-value project

# Delete the old key if exists, then create a fresh one
gcloud iam service-accounts keys create gcp-sa-key.json --iam-account="github-deployer@$PROJECT_ID.iam.gserviceaccount.com"	
```

**Step 2.** Copy it **safely** — this avoids all encoding issues:

```powershell
# This reads the file as raw UTF-8 text and copies to clipboard
[System.IO.File]::ReadAllText("gcp-sa-key.json") | Set-Clipboard
```

> ⚠️ Do **NOT** use `Get-Content | Set-Clipboard` — it adds CRLF newlines that break JSON parsing.

**Step 3.** Go to GitHub Secrets:
👉 `https://github.com/tharun-extinct/Fresh-Greens/settings/secrets/actions`

- Find `GCP_SA_KEY` → click **Update**
- **Clear the existing value completely**
- Paste the clipboard (should start with `{` and end with `}`)
- Save

**Step 4.** Verify it looks right — it should start exactly like:
```json
{
  "type": "service_account",
  "project_id": "...",
```

---

**Step 5.** After saving the secret, **delete the key file from your PC:**
```powershell
Remove-Item gcp-sa-key.json
```

Then re-trigger the workflow by pushing a small commit or clicking **"Re-run jobs"** in the Actions tab.


---

<br>
<br>
**No** — and here's why:

`gcloud config set` stores settings **locally on your PC** (in `~/.config/gcloud/`). It's a client-side CLI preference, not a server-side Google Cloud setting. The Console UI has no equivalent panel for this.

---

### What the Console CAN do vs CLI:

| Setting | Console UI | CLI |
|---|---|---|
| **Switch active project** | ✅ Top dropdown bar | `gcloud config set project` |
| **Default region per service** | ❌ Not available | `gcloud config set run/region` |
| **Default SQL region** | ❌ Not available | `gcloud config set sql/region` |
| **Default compute zone** | ❌ Not available | `gcloud config set compute/region` |

---

### The Console equivalent workflow:

When using the UI, Google simply **always asks you to pick a region** in a dropdown each time — it doesn't remember your preference. That's why the CLI defaults are the only way to avoid it.

---

### Practical tip for Console users:

If you prefer using the Console UI, just **bookmark the direct URLs** with your region pre-selected:

- Cloud Run: `console.cloud.google.com/run?project=YOUR_PROJECT_ID`
- Cloud SQL: `console.cloud.google.com/sql/instances?project=YOUR_PROJECT_ID`

This saves navigation time, even if it doesn't pre-fill the region dropdown.


---

<br>
<br>
<br>


gcloud services enable run.googleapis.com sqladmin.googleapis.com artifactregistry.googleapis.com cloudbuild.googleapis.com secretmanager.googleapis.com



gcloud sql instances create fresh-greens-db --database-version=MYSQL_8_0 --tier=db-f1-micro --region=asia-south1 --root-password=TharunExtinct@12345


Created [https://sqladmin.googleapis.com/sql/v1beta4/projects/fresh-greens-cz007/instances/fresh-greens-db].
NAME             DATABASE_VERSION  LOCATION       TIER         PRIMARY_ADDRESS  PRIVATE_ADDRESS  STATUS
fresh-greens-db  MYSQL_8_0         asia-south1-c  db-f1-micro  35.200.238.247   -                RUNNABLE


C:\Users\2472081>gcloud sql databases create fresh_greens_db --instance=fresh-greens-db
Creating Cloud SQL database...done.
Created database [fresh_greens_db].
instance: fresh-greens-db
name: fresh_greens_db
project: fresh-greens-cz007


gcloud sql users create appuser --instance=fresh-greens-db --password=TharunExtinct@12345



 gcloud secrets create DB_URL --data-file=-
Created version [1] of the secret [DB_URL].



# Your DB connection string — get your instance connection name first:
gcloud sql instances describe fresh-greens-db --format="value(connectionName)"
# It looks like: fresh-greens-prod-123456:asia-south1:fresh-greens-db

# Now create the secrets:
echo -n "jdbc:mysql:///fresh_greens_db?cloudSqlInstance=YOUR_CONNECTION_NAME&socketFactory=com.google.cloud.sql.mysql.SocketFactory&user=appuser&password=AnotherStrongPassword456" | gcloud secrets create DB_URL --data-file=-

echo -n "appuser" | gcloud secrets create DB_USERNAME --data-file=-
echo -n "TharunExtinct@12345" | gcloud secrets create DB_PASSWORD --data-file=-

echo -n "rzp_test_SLjxKvw0xqw49g" | gcloud secrets create RAZORPAY_KEY_ID --data-file=-
echo -n "3WAHhUubrFjgubqDsZzKgU0U" | gcloud secrets create RAZORPAY_KEY_SECRET --data-file=-
echo -n "YOUR_WEBHOOK_SECRET" | gcloud secrets create RAZORPAY_WEBHOOK_SECRET --data-file=-

# Firebase JSON — this uploads the whole file
gcloud secrets create FIREBASE_SERVICE_ACCOUNT_JSON --data-file="C:/Users/2472081/OneDrive - Cognizant/Project/fresh-greens/app/src/main/resources/firebase-service-account.json"

gcloud artifacts repositories create fresh-greens --repository-format=docker --location=asia-south1 --description="Fresh Greens Container Images"


gcloud iam service-accounts create github-deployer --display-name="GitHub Actions Deployer"




# Create the service account
gcloud iam service-accounts create github-deployer --display-name="GitHub Actions Deployer"

# Give it the permissions it needs
fresh-greens-cz007 = gcloud config get-value project

gcloud projects add-iam-policy-binding fresh-greens-cz007 --member="serviceAccount:github-deployer@fresh-greens-cz007.iam.gserviceaccount.com" --role="roles/run.admin"

gcloud projects add-iam-policy-binding fresh-greens-cz007 --member="serviceAccount:github-deployer@fresh-greens-cz007.iam.gserviceaccount.com" --role="roles/artifactregistry.writer"

gcloud projects add-iam-policy-binding fresh-greens-cz007 --member="serviceAccount:github-deployer@fresh-greens-cz007.iam.gserviceaccount.com" --role="roles/cloudsql.client"

gcloud projects add-iam-policy-binding fresh-greens-cz007 --member="serviceAccount:github-deployer@fresh-greens-cz007.iam.gserviceaccount.com" --role="roles/secretmanager.secretAccessor"

gcloud projects add-iam-policy-binding fresh-greens-cz007 --member="serviceAccount:github-deployer@fresh-greens-cz007.iam.gserviceaccount.com" --role="roles/iam.serviceAccountUser"

# Download the key as a JSON file
gcloud iam service-accounts keys create gcp-sa-key.json --iam-account="github-deployer@fresh-greens-cz007.iam.gserviceaccount.com"

C:\Users\2472081>gcloud iam service-accounts keys create gcp-sa-key.json --iam-account="github-deployer@fresh-greens-cz007.iam.gserviceaccount.com"
created key [b967d228a5bb6527f281101153b90c8d644761ad] of type [json] as [gcp-sa-key.json] for [github-deployer@fresh-greens-cz007.iam.gserviceaccount.com]




