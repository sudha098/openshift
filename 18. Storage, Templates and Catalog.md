# OpenShift Course – Storage, Templates & Catalog

This module focuses on how applications store data, how persistent volumes are provisioned, how resource limits are enforced, and how users can package reusable application blueprints with templates and catalogs.

## 📌 Topics Covered

* Storage
* Persistent Storage – Static vs Dynamic Provisioning (StorageClasses)
* Resource Allocation – CPU and RAM
* ResourceQuota Overview
* Example Voting Application
* Templates & Catalog
* Demo – Create Custom Catalog

---

## 🔶 1. Storage in OpenShift

OpenShift supports multiple storage backends to support both stateful and stateless workloads.

### **Types of Storage**

* **Ephemeral Storage**

  * Local to the node/pod
  * Data is lost when the pod restarts
  * Used for caches, temp files, short-lived apps
* **Persistent Storage**

  * Survives pod restarts
  * Backed by network storage like NFS, Ceph, AWS EBS, GCP PD, Azure Disk
  * Required for databases and stateful workloads

### **PersistentVolume (PV) & PersistentVolumeClaim (PVC)**

* **PV**: A cluster resource representing storage (pre-provisioned or dynamically created).
* **PVC**: A user request for storage, matched to a PV using size, access modes, and StorageClass.

---

## 🔶 2. Static vs Dynamic Provisioning (StorageClasses)

### **Static Provisioning**

* Admin manually creates PersistentVolumes beforehand
* PVCs bind to available PVs
* Useful in on-prem or legacy storage where automation is limited

Example PV:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-static-example
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

### **Dynamic Provisioning**

* PVC triggers automatic storage creation
* Requires a **StorageClass** with a provisioner (e.g., AWS EBS, Ceph RBD, NFS, OCS)

Example StorageClass:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: default-sc
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```

PVC using StorageClass:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-claim
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: default-sc
  resources:
    requests:
      storage: 2Gi
```

### **Key Benefits of Dynamic Provisioning**

* Automated storage creation
* Reduces admin overhead
* Eliminates the need to pre-create PVs

---

## 🔶 3. Resource Allocation – CPU & RAM

OpenShift uses **requests and limits** to ensure fair usage of cluster resources.

### **Requests**

* Minimum guaranteed resource
* Scheduler places pods on nodes that can satisfy requests

### **Limits**

* Maximum allowed resource
* Prevents containers from consuming too much

Example:

```yaml
resources:
  requests:
    cpu: "200m"
    memory: "256Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

### **Why Use Requests & Limits?**

* Prevent noisy-neighbor problems
* Ensure workloads get required CPU/RAM
* Improve cluster stability

---

## 🔶 4. ResourceQuota Overview

ResourceQuotas help administrators control resource consumption at the namespace level.

### **Types of quotas**

* **Compute quotas** – CPU, memory
* **Storage quotas** – total PVC count, storage capacity
* **Object count quotas** – max number of pods, services, routes, etc.

Example ResourceQuota:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: rq-demo
spec:
  hard:
    pods: "10"
    requests.cpu: "2"
    limits.cpu: "4"
    requests.memory: 4Gi
    persistentvolumeclaims: "5"
```

---

## 🔶 5. Example Voting Application

A typical OpenShift demo workload that uses:

* **Frontend** (web app pod)
* **Worker** (background process)
* **Redis** (ephemeral or persistent storage)
* **PostgreSQL** (persistent PVC using StorageClass)

### Concepts Illustrated

* Deployments & Services
* Connecting pods via DNS
* Using PVCs for databases
* Scaling frontend pods
* Exposing the app using Routes

---

## 🔶 6. Templates & Catalog

Templates allow you to package OpenShift objects and deploy them repeatedly.

### **Why Templates?**

* Pre-defined configurations
* Easy application deployment
* Useful for enterprise app catalogs
* Makes onboarding faster for teams

### **Template Structure**

Includes:

* Parameters (`${DATABASE_USER}`)
* Objects (Deployments, Services, Routes, PVCs)
* Labels & metadata

Example:

```yaml
apiVersion: v1
kind: Template
metadata:
  name: app-template
parameters:
  - name: APP_NAME
    value: voting-app
objects:
  - apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: ${APP_NAME}
```

### **Using a Template**

```sh
oc new-app -f app-template.yaml -p APP_NAME=myapp
```

---

## 🔶 7. Demo – Create Custom Catalog

### Steps to Create a Custom Catalog

1. **Prepare a Template** (e.g., app-template.yaml)
2. **Upload it to the OpenShift cluster**

   ```sh
   oc create -f app-template.yaml -n openshift
   ```
3. **Verify template in the Developer Catalog**
4. **Add metadata for icons, annotations, displayName**
5. **Deploy using the Web Console or CLI**

### Optional Enhancements

* Add parameter validation
* Provide multiple choices (DB type, replica count)
* Add Helm charts into the catalog (OpenShift 4.x)

---

## ✅ Summary

| Topic               | Key Takeaways                           |
| ------------------- | --------------------------------------- |
| Storage             | Persistent vs Ephemeral, PV/PVC basics  |
| Static vs Dynamic   | StorageClass enables auto provisioning  |
| Resource Allocation | CPU & RAM requests/limits               |
| ResourceQuota       | Namespace resource boundaries           |
| Voting App          | Real-world example with PVCs and routes |
| Templates & Catalog | Reusable app blueprints                 |
| Custom Catalog      | Publish templates for team-wide use     |

---

