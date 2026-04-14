## ✅ Correct Concept:

👉 ALL components talk to API Server

Component	Talks to API Server?
Kubelet	✅ Yes
Scheduler	✅ Yes
Controller Manager	✅ Yes
kubectl (user)	✅ Yes
etcd	❌ No (only API Server talks to etcd)

## 📘 🔹 Final Architecture (VERY IMPORTANT 🔥)

          kubectl
             ↓
        API Server
        /   |    \
       ↓    ↓     ↓
 Scheduler Controller Kubelet
       ↓      ↓        ↓
        (all talk to API Server)
             ↓
            etcd

🔹 One-Line Summary 💡

👉 Worker node has Kubelet, Container Runtime, and Kube Proxy to run and manage pods.

## 📘 🔹 Big Concept (VERY IMPORTANT 🧠)

👉 Labels + Selectors = connection

Labels → given to pods
Selector → used by ReplicaSet

👉 This is how it knows:
👉 “Which pods are mine?”
