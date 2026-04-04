
# 🔑 Key Concepts from the Lecture

### 1️⃣ Role

A **Role** is a set of permissions within a **namespace**.

* **Purpose:** Define **what actions** a user can perform on **which resources**.
* **Scope:** Namespace-specific (if you want cluster-wide, you use ClusterRole instead).

**Structure of a Role (YAML):**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
  namespace: default
rules:
  - apiGroups: [""]          # "" means core group
    resources: ["pods"]
    verbs: ["get", "list", "create", "delete"]
  - apiGroups: [""]          
    resources: ["configmaps"]
    verbs: ["create"]
```

* `apiGroups` → Kubernetes API group (blank for core)
* `resources` → Which resources user can access (pods, configmaps, etc.)
* `verbs` → Actions allowed (get, list, create, delete, etc.)
* You can add multiple rules in one Role.

---

### 2️⃣ RoleBinding

A **RoleBinding** links **a user (or group)** to a **Role**.

* **Purpose:** Give the defined permissions in the Role to a user.
* **Scope:** Also namespace-specific.

**Example YAML:**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-user-to-developer-binding
  namespace: default
subjects:
  - kind: User
    name: dev-user
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

* `subjects` → Users, groups, or service accounts you are granting access to
* `roleRef` → The Role that defines the permissions

---

### 3️⃣ RBAC Commands

**View Roles:**

```bash
kubectl get roles
kubectl describe role developer
```

**View RoleBindings:**

```bash
kubectl get rolebindings
kubectl describe rolebinding dev-user-to-developer-binding
```

---

### 4️⃣ Testing Permissions

Kubernetes provides a way to **check if a user can perform a specific action**:

```bash
kubectl auth can-i create pods
```

* Replace `create pods` with any action/resource.
* Add namespace if needed:

```bash
kubectl auth can-i create pods --namespace=test
```

* You can also **impersonate another user**:

```bash
kubectl auth can-i create deployments --as dev-user
```

---

### 5️⃣ Restricting Access to Specific Resources

You can limit a Role further to **specific resources only**, not all objects:

```yaml
rules:
  - apiGroups: [""]
    resources: ["pods"]
    resourceNames: ["blue-pod", "orange-pod"]
    verbs: ["get", "list"]
```

* Now the user can only access `blue-pod` and `orange-pod` inside that namespace.

---

# 🧠 Summary

| Concept              | What it does                        | Scope                                   |
| -------------------- | ----------------------------------- | --------------------------------------- |
| Role                 | Defines **permissions**             | Namespace                               |
| RoleBinding          | Assigns a **Role** to a user        | Namespace                               |
| ClusterRole          | Like Role but **cluster-wide**      | Cluster                                 |
| ClusterRoleBinding   | Assigns a **ClusterRole** to a user | Cluster                                 |
| `kubectl auth can-i` | Test **permissions**                | Optional namespace + user impersonation |

---

