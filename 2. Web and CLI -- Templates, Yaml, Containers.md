

# Demo: Web Console & CLI

This section demonstrates how to work with OpenShift using both the **Web UI** and the **CLI (oc)**.
You will learn how to deploy applications using **Templates**, manage resources via **YAML**, and handle **Container images**.

---

## 📌 6.1 Using the Web Console (GUI)

### ✔️ Create a New Project

1. Open the OpenShift Console
2. Click **Home → Projects**
3. Select **Create Project**
4. Enter:

   * Name: `demo-web`
   * Display Name: `Web Demo Project`
   * Description: (optional)

---

### ✔️ Deploy an Application From a Container Image (Web)

1. Go to your project: **demo-web**
2. Click **+Add**
3. Choose **Container Image**
4. Enter an example image, such as:

   ```
   quay.io/redhattraining/hello-world-nginx
   ```
5. Set:

   * Application name: `web-demo-app`
   * Resource type: **Deployment**
6. Click **Create**

🎉 Your application is now deployed using the Web Console.

---

### ✔️ View and Edit YAML in the Console

1. Open your deployment: **web-demo-app**
2. Click **Actions → Edit YAML**
3. Modify environment variables or replicas, for example:

   ```yaml
   spec:
     replicas: 2
   ```
4. Click **Save**

You’ve now edited cluster resources using YAML directly in the web interface.

---

## 📌 6.2 Using the CLI (oc)

Before running commands, log in using:

```bash
oc login --token=<your-token> --server=<api-url>
```

### ✔️ Create a Project via CLI

```bash
oc new-project demo-cli
```

---

### ✔️ Deploy a Container Image (CLI)

```bash
oc new-app quay.io/redhattraining/hello-world-nginx --name=cli-demo-app
```

Check deployment status:

```bash
oc get pods
```

Expose a route:

```bash
oc expose service/cli-demo-app
```

Get the route URL:

```bash
oc get route cli-demo-app -o jsonpath='{.spec.host}'
```

---

## 📌 6.3 Working With Templates

OpenShift Templates allow you to deploy multi-resource applications with parameters.

### ✔️ Example: Use a Built-in Template

```bash
oc new-app --template=postgresql-persistent \
  -p DATABASE_SERVICE_NAME=pgdemo \
  -p POSTGRESQL_USER=user1 \
  -p POSTGRESQL_PASSWORD=pass123 \
  -p POSTGRESQL_DATABASE=demodb
```

List all available templates:

```bash
oc get templates -A
```

---

### ✔️ Create a Template from YAML

Save the following template as `hello-template.yaml`:

```yaml
apiVersion: template.openshift.io/v1
kind: Template
metadata:
  name: hello-template
objects:
  - apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: hello-app
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: hello-app
      template:
        metadata:
          labels:
            app: hello-app
        spec:
          containers:
            - name: hello-app
              image: quay.io/redhattraining/hello-world-nginx
parameters: []
```

Create and instantiate it:

```bash
oc create -f hello-template.yaml
oc new-app --template=hello-template
```

---

## 📌 6.4 Working With YAML Directly (CLI)

### Get YAML

```bash
oc get deployment hello-app -o yaml
```

### Apply YAML

```bash
oc apply -f deployment.yaml
```

### Edit live resource

```bash
oc edit deployment hello-app
```

---

## 📌 6.5 Working With Containers

### ✔️ Import an Image into OpenShift

```bash
oc import-image my-image:latest --from=quay.io/example/image --confirm
```

### ✔️ Build an Image From Source (S2I)

```bash
oc new-app nodejs:16~https://github.com/sclorg/nodejs-ex
```

### ✔️ View ImageStreams

```bash
oc get is
```

---

# ✅ Summary: What You Learned in the Demo

* Creating projects via **Web Console** and **CLI**
* Deploying apps from **container images**
* Editing and managing **YAML resources**
* Using **Templates** for multi-object deployments
* Creating routes and viewing pod status
* Working with **ImageStreams** and **S2I builds**

---

