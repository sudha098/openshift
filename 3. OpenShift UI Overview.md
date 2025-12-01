# 🖥️ OpenShift Web Console (UI) — Overview

The **OpenShift Web Console** is a graphical interface for interacting with Kubernetes and OpenShift resources. It enables developers and platform engineers to manage workloads, builds, CI/CD pipelines, storage, networking, and cluster administration without CLI commands.

---

## 🔐 Login

You can access the UI using the console URL shown after installation, for example:

```
https://console-openshift-console.apps.<cluster-domain>
```

Credentials:

* **Kubeadmin / Identity provider user**
* **Single Sign-On (if configured)**

---

## 🧭 UI Layout Overview

| Area                                      | Description                                                       |
| ----------------------------------------- | ----------------------------------------------------------------- |
| **Home**                                  | Dashboard, cluster status, resource usage, alerts                 |
| **Operators**                             | Install/manage Operators via OperatorHub, monitor operator health |
| **Workloads**                             | Manage Deployments, StatefulSets, Pods, Jobs, CronJobs            |
| **Networking**                            | Services, Routes, Ingress, NetworkPolicies                        |
| **Storage**                               | Persistent Volume Claims, StorageClasses, Snapshots               |
| **Builds**                                | BuildConfigs, ImageStreams, Pipelines                             |
| **Pipelines**                             | Tekton pipeline runs, triggers, tasks, CI/CD                      |
| **Helm**                                  | Browse and deploy Helm charts                                     |
| **Compute/Cluster Settings** (Admin only) | Nodes, Projects, MachineSets, CRDs, API Access                    |
| **User Menu**                             | API token, CLI config (kubeconfig), profile settings              |

---

## 👓 Two Console Views

OpenShift UI supports **two major perspectives** depending on the role:

| Perspective       | Audience                  | Focus                                                 |
| ----------------- | ------------------------- | ----------------------------------------------------- |
| **Developer**     | Developers & DevOps       | Workloads, deployments, CI/CD, images, routes         |
| **Administrator** | Platform Engineers & SREs | Cluster health, operators, nodes, storage, networking |

Switch using the dropdown in the top-left.

---

## 🧱 Developer Perspective — Key Features

| Menu                     | Purpose                                                  |
| ------------------------ | -------------------------------------------------------- |
| **Topology**             | Graphical map of apps: Pods, Services, Routes, Pipelines |
| **Workloads**            | Manage deployments, statefulsets, jobs, pods             |
| **Builds**               | BuildConfigs & ImageStreams for S2I builds               |
| **Pipelines**            | Visual CI/CD using Tekton                                |
| **Routes**               | Expose services to the internet                          |
| **Helm**                 | Deploy apps using Helm charts                            |
| **Secrets / ConfigMaps** | Manage app configs                                       |
| **Project**              | Namespace-level resources                                |

🎯 Designed for application development, CI/CD and day-to-day app delivery.

---

## 🔐 Administrator Perspective — Key Features

| Menu                        | Purpose                                                         |
| --------------------------- | --------------------------------------------------------------- |
| **Cluster Settings**        | Cluster version, operators, insights, updates                   |
| **Nodes**                   | List & manage cluster nodes                                     |
| **MachineSets**             | Scale compute nodes                                             |
| **Operators / OperatorHub** | Install certified operators (databases, logging, storage, etc.) |
| **CRDs**                    | Access Custom Resource Definitions                              |
| **Projects**                | Manage namespaces                                               |
| **Networking**              | DNS, Routes, Ingress, network policies                          |
| **Storage**                 | PVs, StorageClasses, Snapshot classes                           |
| **User Management**         | Authentication and RBAC                                         |
| **Monitoring**              | Metrics & Alerting via Prometheus & Alertmanager                |

🎯 Designed for managing the cluster itself, not workloads.

---

## 📊 Dashboard

The homepage dashboard provides:

* Cluster status
* Health of operators
* CPU / Memory usage
* Alerts & cluster warnings
* Details about control-plane & compute nodes
* Subscription & version channel

---

## ⚙️ Additional Useful UI Tools

| Feature                  | Description                               |
| ------------------------ | ----------------------------------------- |
| **Web Terminal**         | Open an in-browser terminal with `oc` CLI |
| **API Explorer**         | Discover Kubernetes & CRD APIs            |
| **Search**               | Query resources by Type or Label          |
| **Resource YAML Editor** | Modify manifests directly via UI          |
| **Events**               | Warning, info and system events           |
| **Logs**                 | Pod logs viewer with stream mode          |
| **Pod Terminal**         | Shell access inside containers            |

---

## 🌐 CI/CD in OpenShift UI

| Feature         | Tech                 | UI Location                                       |
| --------------- | -------------------- | ------------------------------------------------- |
| Build pipelines | Tekton               | **Pipelines → Pipelines / PipelineRuns**          |
| S2I builds      | BuildConfig          | **Builds → Builds / ImageStreams**                |
| GitOps          | ArgoCD (as Operator) | **Application → GitOps (after operator install)** |
| Image lifecycle | Image Registry       | **Builds / Workloads**                            |

---

## 🚀 Deploying an App via UI (Developer Perspective)

1. Click **+Add**
2. Choose deployment method:

   * Deploy from Git
   * Container image
   * Helm chart
   * YAML / form
3. Set resource configuration (env vars, secrets, scaling)
4. Expose externally via **Route**
5. Start pipeline (optional)

---

## 📌 Common Tasks from UI

| Task               | Where                                           |
| ------------------ | ----------------------------------------------- |
| Scale deployment   | Workloads → Deployment → Actions                |
| Edit YAML          | Actions → Edit YAML                             |
| Rollout restart    | Actions → Rollout → Restart                     |
| View logs          | Pods → Logs                                     |
| Debug container    | Pods → Terminal                                 |
| Assign permissions | Administrator → User Management → Role Bindings |

---

## 🧠 Tips for Beginners

✔ Use **Topology view** to understand app connections
✔ Switch between **Developer vs Administrator** when confused
✔ Use **Search bar** to quickly find any resource
✔ Use **Download Kubeconfig** from the profile menu to use CLI easily

---
