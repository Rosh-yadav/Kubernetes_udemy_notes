

# 🧠 First: What is Network Policy (in simple words)?

👉 A **Network Policy** in Kubernetes is used to **control traffic between pods**.

By default:
❌ All pods can talk to each other (no restriction)

With Network Policy:
✅ You **restrict who can talk to whom**

---

# 🎯 Interview Question:

## ❓ “How do you configure Network Policy?”

You can answer like this 👇

---

# ✅ Step-by-Step Explanation

## 🔹 Step 1: Ensure Network Plugin Supports It

Not all CNI support network policies.

✅ Supported:

* Calico
* Cilium
* Weave Net

❌ Not supported:

* Flannel (important interview point ⚡)

👉 So first check:

```bash
kubectl get pods -n kube-system
```

---

## 🔹 Step 2: Label Your Pods (VERY IMPORTANT)

Network Policy works using **labels + selectors**

Example:

```yaml
labels:
  app: db
```

```yaml
labels:
  app: api
```

---

## 🔹 Step 3: Create Network Policy YAML

Example:
👉 Allow only API pod to talk to DB pod

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      app: db   # Apply policy to DB pod

  policyTypes:
  - Ingress

  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: api   # Allow only API pod
    ports:
    - protocol: TCP
      port: 3306
```

---

## 🔹 Step 4: Apply Policy

```bash
kubectl apply -f network-policy.yaml
```

---

# 🔥 What Happens After This?

👉 DB pod will ONLY accept traffic from API pod
👉 All other traffic = ❌ BLOCKED

---

# ⚠️ Important Concepts (Say This in Interview)

## 🔹 1. podSelector

👉 Defines **which pod this policy applies to**

---

## 🔹 2. ingress

👉 Controls **incoming traffic**

---

## 🔹 3. egress

👉 Controls **outgoing traffic**

---

## 🔹 4. from / to

👉 Defines **allowed sources/destinations**

---

## 🔹 5. ports

👉 Defines **which port is allowed**

---

# 🧩 Real-World Example (Very Important)

App flow:

```
User → Web → API → DB
```

You will configure:

| Component | Rule                          |
| --------- | ----------------------------- |
| Web       | Allow from internet (port 80) |
| API       | Allow from Web                |
| DB        | Allow from API only           |

👉 This is called **zero trust security model**

---

# 💡 Key Interview Points (Must Say)

✔ Network policies are **namespace scoped**
✔ They use **labels & selectors**
✔ Default Kubernetes = **allow all traffic**
✔ Once policy applied = **deny all except allowed**
✔ Depends on **CNI plugin support**

---

# 🎯 Short Answer (If interviewer wants quick answer)

👉 You can say:

> “To configure a Network Policy, first ensure the CNI plugin supports it like Calico. Then label the pods. Create a NetworkPolicy YAML
>  where we define podSelector to target pods, and ingress/egress rules using labels, ports, and protocols. Finally apply it using kubectl. Once applied, only defined traffic
>  is allowed and all other traffic is blocked.”

---


