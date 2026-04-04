# 🧠 BIG IDEA

👉 In Docker you used:

* `--user`
* `--cap-add`
* `--cap-drop`

👉 In Kubernetes, the same thing is done using:

# 🔐 **Security Context**

---

# 📦 1. What is Security Context?

👉 It is a **setting in Pod/Container** that controls:

* Which user runs the container
* What permissions it has
* What capabilities are allowed

---

# 🧱 2. Where can you define it?

### ✅ Two places:

### 1. Pod level

```yaml
spec:
  securityContext:
    runAsUser: 1000
```

👉 Applies to **ALL containers in the pod**

---

### 2. Container level

```yaml
containers:
- name: app
  image: nginx
  securityContext:
    runAsUser: 2000
```

👉 Applies to **only that container**

---

# ⚠️ Important Rule (VERY IMPORTANT)

👉 If both are defined:

👉 **Container level overrides Pod level**

---

# 🧠 Example

```yaml
spec:
  securityContext:
    runAsUser: 1000

  containers:
  - name: app
    image: nginx
    securityContext:
      runAsUser: 2000
```

👉 Final result:

* Container runs as **2000**, not 1000

---

# 👤 3. runAsUser (Most Common)

👉 This sets **which user runs inside container**

```yaml
securityContext:
  runAsUser: 1000
```

---

### Why?

* Avoid root ❌
* Improve security ✅

---

# 🔐 4. Capabilities (Advanced but important)

👉 Like Docker:

```yaml
securityContext:
  capabilities:
    add: ["NET_ADMIN"]
```

---

### Remove permission:

```yaml
securityContext:
  capabilities:
    drop: ["ALL"]
```

---

# 🔥 Real-world usage

Most companies use:

```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
```

👉 Ensures:

* Container never runs as root

---

👉 **“What is securityContext in Kubernetes?”**

> SecurityContext is used to define security settings like user ID, privileges, and Linux capabilities for pods or containers.

---

# 🧠 FINAL SIMPLE SUMMARY

* SecurityContext = security settings in Kubernetes
* Can be set at:

  * Pod level
  * Container level
* Container overrides Pod
* Used for:

  * Non-root user
  * Capabilities
  * Security control

---

