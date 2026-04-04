
# 🔐 What is the Lecture Trying to Teach?

👉 It explains **Service Accounts in Kubernetes**
👉 And how **applications (not humans)** securely talk to the cluster

---

# 👥 Two Types of Accounts in Kubernetes

### 1️⃣ User Account

* Used by **humans**
* Examples:

  * Admin 👨‍💻
  * Developer 👩‍💻

👉 Used with:

* kubectl
* certificates / kubeconfig

---

### 2️⃣ Service Account ⭐ (Main topic)

* Used by **applications / machines**
* Examples:

  * CI/CD tools (Jenkins)
  * Monitoring tools (Prometheus)
  * Your app inside a Pod

👉 Used to **talk to Kubernetes API**

---

# 🎯 Why Service Accounts?

Example from lecture:

👉 Your app wants to:

* Get list of pods
* Call Kubernetes API

❗ But API is secured → needs authentication

👉 Solution: **Service Account + Token**

---

# 🔑 What is a Token?

👉 Token = identity proof for service account

Think like:

* Service Account = ID card
* Token = barcode on ID card

👉 When API request is sent:

```bash
Authorization: Bearer <TOKEN>
```

---

# ⚙️ Default Behavior (Very Important)

### Every namespace has:

👉 `default` service account

When you create a pod:
👉 It automatically gets attached

---

# 📦 What Happens Inside Pod?

Kubernetes automatically:

1. Creates a token
2. Mounts it inside pod

📍 Location inside pod:

```bash
/var/run/secrets/kubernetes.io/serviceaccount/
```

Inside you’ll find:

* token
* ca.crt
* namespace

👉 Your app reads token → calls API

---

# 🛠️ Creating Custom Service Account

### Imperative way:

```bash
kubectl create serviceaccount dashboard-sa
```

---

### YAML way:

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: dashboard-sa
```

---

# 🔗 Attach Service Account to Pod

```yaml
spec:
  serviceAccountName: dashboard-sa
```

👉 Now pod uses this service account

---

# 🔄 Token Behavior (Inside Cluster)

When pod uses service account:

✅ Token auto-created
✅ Token auto-mounted
✅ Token auto-rotated
✅ Token auto-deleted (when pod deleted)

---

# 🚫 Disable Auto Mount (Security)

If you don’t want token inside pod:

```yaml
automountServiceAccountToken: false
```

👉 Can be set:

* On ServiceAccount
* On Pod

---


## 🧠 Real-World Example

👉 Jenkins pipeline:

1. Create service account
2. Give RBAC permissions
3. Generate token
4. Store token in Jenkins
5. Use token to deploy apps

---

# 📊 Final Summary

| Concept         | Meaning                    |
| --------------- | -------------------------- |
| User Account    | Human access               |
| Service Account | App/machine access         |
| Token           | Authentication proof       |
| Default SA      | Auto attached to pods      |
| Custom SA       | For specific permissions   |
| Token Mount     | Auto inside pod            |
| External Token  | Use `kubectl create token` |

---
👉 If asked: *What is Service Account?*


> “A Service Account is used by applications running inside or outside Kubernetes to authenticate with the API server. It uses tokens for authentication,
> which can be automatically mounted inside pods or manually generated for external access.”

---

