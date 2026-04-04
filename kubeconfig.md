This lecture is actually **very important for real DevOps work** 👍 — it explains how you *connect to Kubernetes clusters easily without typing long commands every time*

# 🧠 What this lecture is trying to teach

👉 **Kubeconfig = a config file that stores cluster access details**

Instead of writing this every time:

```bash
kubectl get pods \
  --server=https://1.2.3.4 \
  --client-key=key.pem \
  --client-certificate=cert.pem \
  --certificate-authority=ca.pem
```

❌ Too long + annoying

👉 You store everything in **one file → kubeconfig**

---

# 📁 Where kubeconfig is stored

Default location:

```
~/.kube/config
```

👉 That’s why you normally just run:

```bash
kubectl get pods
```

(no need to pass certificates manually)

---

# 🔑 Core Idea: 3 Main Sections

The kubeconfig file has **3 important parts**:

---

## 1️⃣ Clusters

👉 Defines **which cluster you want to connect to**

Example:

```yaml
clusters:
- name: my-cluster
  cluster:
    server: https://1.2.3.4
    certificate-authority: ca.crt
```

✔️ Contains:

* API server URL
* CA certificate

---

## 2️⃣ Users

👉 Defines **who you are (authentication)**

```yaml
users:
- name: admin
  user:
    client-certificate: admin.crt
    client-key: admin.key
```

✔️ Contains:

* client certificate
* private key

---

## 3️⃣ Contexts (MOST IMPORTANT)

👉 Context = **cluster + user mapping**

```yaml
contexts:
- name: admin@my-cluster
  context:
    cluster: my-cluster
    user: admin
```

✔️ Means:
👉 “Use **admin user** to access **my-cluster**”

---

# 🔥 Final Piece: Current Context

```yaml
current-context: admin@my-cluster
```

👉 This decides:

* Which cluster you are using
* Which user credentials are used

---

# 🔄 Important Commands (VERY COMMON in interviews)

### 👉 View config

```bash
kubectl config view
```

---

### 👉 Check current context

```bash
kubectl config current-context
```

---

### 👉 Switch context

```bash
kubectl config use-context <context-name>
```

Example:

```bash
kubectl config use-context prod@cluster
```

---



# 🎯 Interview One-Liner

👉 *“Kubeconfig is a YAML file that stores cluster, user, and context information, allowing kubectl to authenticate and connect to Kubernetes clusters without 
specifying credentials manually.”*

---

