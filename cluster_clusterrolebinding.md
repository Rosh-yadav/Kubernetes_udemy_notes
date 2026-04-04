
---

# 🔑 Key Concepts: ClusterRoles & ClusterRoleBindings

### 1️⃣ Namespaced vs Cluster-scoped Resources

| Resource Type  | Examples                                           | Scope                                                     |
| -------------- | -------------------------------------------------- | --------------------------------------------------------- |
| Namespaced     | Pods, Deployments, Services, ConfigMaps, Secrets   | Exist **within a namespace**                              |
| Cluster-scoped | Nodes, PersistentVolumes, Namespaces, ClusterRoles | Exist **at the cluster level**, not tied to any namespace |

* **Roles** → Work only on **namespaced resources** (within a specific namespace).
* **RoleBindings** → Link **users/groups** to Roles **within a namespace**.

---

### 2️⃣ ClusterRole

* **Purpose:** Define permissions for **cluster-scoped resources**.
* **Usage:** Similar to Role, but applies **cluster-wide**.

**Example YAML: ClusterRole for nodes**

```yaml id="1k9nlz"
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-admin-role
rules:
  - apiGroups: [""]      # Core API group
    resources: ["nodes"]
    verbs: ["get", "list", "create", "delete"]
```

* You can also use ClusterRoles for **namespaced resources** if you want access **across all namespaces**.

  * Example: If you create a ClusterRole for pods, a user can access **pods in all namespaces**.

---

### 3️⃣ ClusterRoleBinding

* **Purpose:** Link **users, groups, or service accounts** to a **ClusterRole**.
* **Scope:** Cluster-wide.

**Example YAML: ClusterRoleBinding**

```yaml id="2i9t5l"
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: limit-cluster-admin-binding
subjects:
  - kind: User
    name: cluster-admin-user
    apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-admin-role
  apiGroup: rbac.authorization.k8s.io
```

* `subjects` → Users/groups/service accounts getting access.
* `roleRef` → The ClusterRole granting the permissions.

---

### 4️⃣ Key Points

1. **Roles vs ClusterRoles**

   * Role → Namespaced (limited to one namespace)
   * ClusterRole → Cluster-scoped (all namespaces + cluster resources)

2. **RoleBinding vs ClusterRoleBinding**

   * RoleBinding → Assigns a Role **within a namespace**
   * ClusterRoleBinding → Assigns a ClusterRole **cluster-wide**

3. **ClusterRole for Namespaced Resources**

   * You can use ClusterRoles on namespaced resources to give access **across all namespaces**.

4. **Default ClusterRoles**

   * Kubernetes comes with built-in ClusterRoles like `cluster-admin`, `admin`, `edit`, `view`.
   * You can assign these to users using ClusterRoleBindings.

---

### 5️⃣ Real-world Example

* You have a **storage admin**:

  * Needs access to all PersistentVolumes → Create a **ClusterRole** for PVs.
  * Bind it to the storage admin user → Create **ClusterRoleBinding**.

* You have a **developer**:

  * Needs access to pods in **all namespaces** → Use ClusterRole for pods.
  * Bind it using ClusterRoleBinding.

---

