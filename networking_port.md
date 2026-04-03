This lecture is basically explaining **what network setup is required for a Kubernetes cluster to work properly**—especially focusing on **master (control plane) and worker nodes**.
---

# 🧠 1. Basic Idea: Every Node Needs Proper Networking

In Kubernetes, you have:

* **Master node (Control Plane)** → manages the cluster
* **Worker nodes** → run applications (pods)

👉 For them to communicate:

* Each node must have:

  * A **network interface** (like `eth0`)
  * A **valid IP address**
  * A **unique hostname**
  * A **unique MAC address**

⚠️ Important:
If you create VMs by cloning → they might have duplicate MAC/hostname → this breaks networking.

---

# 🔌 2. Important Ports in Kubernetes (VERY IMPORTANT FOR INTERVIEWS)

He is mainly teaching:
👉 “Which ports must be open for Kubernetes components to talk to each other”

---

## 🔷 Master Node (Control Plane Ports)

### 1. **6443 → Kubernetes API Server**

* Most important port
* Used by:

  * `kubectl`
  * worker nodes
  * control plane components

👉 Think:
➡️ This is the **main entry point of the cluster**

---

### 2. **10257 → kube-controller-manager**

* Handles:

  * replication
  * node management
  * controllers

---

### 3. **10259 → kube-scheduler**

* Decides:

  * which pod runs on which node

---

### 4. **2379 → etcd (database)**

* Stores cluster state

---

### 5. **2380 → etcd peer communication**

* Used when:

  * multiple master nodes (HA setup)

---

## 🔷 Worker Node Ports

### 6. **10250 → kubelet**

* Runs on:

  * both master & worker
* Used for:

  * communication with control plane

---

### 7. **30000–32767 → NodePort services**

* Used to expose apps outside cluster

👉 Example:

```bash
http://<NodeIP>:30007
```

---

# 🔥 3. Why This Matters

He is teaching this because:

👉 If these ports are NOT open:

* Cluster will NOT work
* Pods won’t start
* Nodes won’t join
* `kubectl` won’t connect

---





