# OpenShift Course – Networks, Services, Routes & Scaling

This module covers how applications communicate inside an OpenShift cluster, how traffic reaches them from outside, and how workloads scale automatically based on demand.

## 📌 Topics Covered

* Networking Overview
* Services & Routes
* Scaling
* Autoscaling (HPA)

---

## 🔶 1. Networking Overview

OpenShift networking is built to provide secure, isolated, and flexible communication between pods, services, and external clients.

### **Key Concepts**

* **Pod Networking (SDN/CNI)**
  Every pod receives its own IP address. Communication between pods is allowed by default unless restricted by **NetworkPolicies**.
* **Cluster Network vs. Service Network**

  * *Cluster Network*: IPs assigned to pods.
  * *Service Network*: Virtual IPs (cluster IPs) assigned to Kubernetes Services.
* **DNS in OpenShift**
  Services get automatic DNS names (e.g., `my-service.my-namespace.svc.cluster.local`).
* **NetworkPolicies**
  Control which pods can communicate with each other (deny-by-default patterns for security).

### **Takeaways**

* No need for port-mapping like Docker; pods communicate directly.
* Applications scale without networking reconfiguration because traffic flows through services.

---

## 🔶 2. Services and Routes

### **Services**

Services act as stable endpoints that route traffic to backend pods.

#### **Types of Services**

* **ClusterIP (default)**
  Internal-only, used for pod-to-pod communication.
* **NodePort**
  Opens a static port on every node for external access.
* **LoadBalancer**
  Integrates with cloud providers to provision an external LB.
* **Headless Services**
  Used for stateful apps requiring direct pod DNS (e.g., databases).

#### **Service Selectors**

Services use label selectors to find matching pods dynamically.

### **Routes (OpenShift-specific)**

Routes expose services externally using OpenShift’s built-in router (HAProxy or Envoy depending on version).

#### **Route Types**

* **Edge**: TLS termination at the router
* **Passthrough**: TLS termination happens at the application
* **Re-encrypt**: TLS re-encrypted between router and backend service

### **Use Cases**

* Expose an HTTP application publicly
* Provide custom domain access
* Terminate TLS securely at the router

---

## 🔶 3. Scaling in OpenShift

Scaling increases or decreases the number of pods for a deployment, deploymentConfig, or replica set.

### **Types of Scaling**

* **Manual Scaling**
  Performed using:

  ```sh
  oc scale deployment myapp --replicas=3
  ```
* **Rolling Updates with Scaling**
  Ensures zero-downtime updates.

### **When to Scale**

* Increased user requests
* High CPU/Memory usage
* To improve availability

### **Best Practices**

* Use readiness/liveness probes
* Distribute replicas across zones
* Combine with autoscaling for dynamic workloads

---

## 🔶 4. Autoscaling – Horizontal Pod Autoscaler (HPA)

HPA adjusts the number of pod replicas automatically based on resource usage.

### **How HPA Works**

* Monitors CPU, memory, or custom metrics through the Metrics Server.
* Scales pods up or down to meet target resource thresholds.

### **Example:**

```sh
oc autoscale deployment myapp \
  --min=2 --max=10 \
  --cpu-percent=70
```

### **Key Concepts**

* **Target Metrics:** CPU%, memory, or external metrics
* **Min/Max Replicas:** Ensures the app stays within safe scaling limits
* **Cool-down period:** Prevents rapid scaling loops

### **Use Cases**

* Variable workloads (e-commerce, event-driven apps)
* Reducing cost by autoscaling during off-peak hours
* Ensuring responsiveness under heavy load

---

## ✅ Summary

| Topic                   | What You Learned                          |
| ----------------------- | ----------------------------------------- |
| **Networking Overview** | Pod networking, DNS, NetworkPolicies      |
| **Services & Routes**   | ClusterIP, NodePort, LoadBalancer, Routes |
| **Scaling**             | Manual and rolling scaling                |
| **Autoscaling (HPA)**   | Automatically scale based on metrics      |

