
# 1. Create a Red Hat Account

Follow these steps to create your account:

1. Go to the Red Hat customer portal:
   [https://www.redhat.com/wapps/ugc/register.html](https://www.redhat.com/wapps/ugc/register.html)
2. Fill out the registration form
3. Verify your email
4. Log in at: [https://access.redhat.com](https://access.redhat.com)

Your Red Hat account gives you access to OpenShift downloads, Sandbox environments, and learning resources.

---

# 2. Access the Red Hat Hybrid Cloud Console

1. Visit: [https://console.redhat.com](https://console.redhat.com)
2. Sign in with your Red Hat account
3. Explore key sections:

   * **OpenShift** → Clusters
   * **OpenShift** → Downloads
   * **Training & Sandbox** options

This console is the central management page for Red Hat cloud services.

---

# 3. Install Single-Node OpenShift Using CRC (OpenShift Local)

OpenShift Local (formerly CRC) allows you to run a **single-node OpenShift cluster** on your local machine.

### ✔️ Requirements

* 4 vCPUs
* 16–32 GB RAM (recommended)
* 45+ GB free disk
* Virtualization enabled (KVM / Hyper-V / HyperKit)

### Step-by-Step Installation

#### 1. Download CRC

1. Go to:
   **Hybrid Cloud Console → OpenShift → Downloads → OpenShift Local**
2. Download the latest CRC release for your OS.

#### 2. Install CRC

```bash
# Linux example
tar -xvf crc-linux-amd64.tar.xz
sudo mv crc-linux-*/crc /usr/local/bin/
```

macOS and Windows users can use their respective installers.

#### 3. Set up CRC

```bash
crc setup
```

#### 4. Start the Single-Node Cluster

```bash
crc start
```

CRC will display:

* `kubeadmin` username
* `kubeadmin` password
* OpenShift Console URL
* API URL

#### 5. Login to the Web Console

Open the URL provided by CRC (usually `https://console-openshift-console.apps-crc.testing/`) and log in with:

```
Username: kubeadmin  
Password: <password-from-crc-start-output>
```

You now have a full **single-node OpenShift cluster** running locally.

---

# 4. Use the OpenShift Developer Sandbox

The Developer Sandbox provides **free, cloud-hosted OpenShift** for learning.

### Steps:

1. Go to:
   [https://developers.redhat.com/developer-sandbox](https://developers.redhat.com/developer-sandbox)
2. Click **Start your sandbox**
3. Log in with your Red Hat account
4. Wait for your sandbox environment to be provisioned
5. Access the web console when ready

### What You Get

* 30-day renewable free cluster
* Full OpenShift dashboard
* Image builds, pipelines, GitOps, and more
* No local hardware requirements

---

# 5. Accessing the OpenShift Web Console

Regardless of whether you're using **CRC** or **Developer Sandbox**, you can log in to the web interface.

### For CRC

CRC will print the console URL:
`https://console-openshift-console.apps-crc.testing/`

Log in using:

```
Username: kubeadmin
Password: <provided-by-crc>
```

### For Developer Sandbox

You will be automatically logged in via your Red Hat SSO.

---

# 📂 Repository Structure (Suggested)

```
openshift-course/
│
├── 01-redhat-account/
├── 02-hybrid-cloud-console/
├── 03-openshift-local-crc/
├── 04-developer-sandbox/
└── README.md
```

---

# 🧪 Useful Commands (Quick Reference)

### Login to cluster using CLI

```bash
oc login -u kubeadmin -p <password> https://api.crc.testing:6443
```

### Check cluster status

```bash
oc status
```

### OpenShift projects

```bash
oc get projects
```

---

# 🎯 End Result

By completing this course, you will be able to:

* Create and manage a Red Hat account
* Navigate Red Hat’s Hybrid Cloud Console
* Run a **local single-node OpenShift cluster** using CRC
* Use the **Developer Sandbox** for cloud-based development
* Access and use the OpenShift Web Console and CLI

---

