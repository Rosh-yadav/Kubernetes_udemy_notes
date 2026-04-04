## 👉 “How does authentication work in Kubernetes?”

You can say:

Kubernetes authentication is handled by the API server. It verifies the identity of users or services using methods like static password files,
tokens, certificates, or external identity providers like LDAP. Kubernetes does not manage user accounts directly but relies on external systems.
Service accounts are used for applications within the cluster.


## 🔹 2. What is TLS (in simple terms)

👉 TLS = encryption + identity verification

It ensures:

Data is secure 🔒
You are talking to the right server ✅

## 🔹 3. Why TLS is important in Kubernetes

In Kubernetes:

API Server talks to nodes
Components talk to each other
Users connect to cluster

👉 All communication must be:
🔒 Encrypted and trusted


## 👉 “Why TLS is important in Kubernetes?”

TLS is used in Kubernetes to secure communication between cluster components like the API server, nodes, and etcd. It ensures encrypted communication and verifies identities,
preventing unauthorized access and data interception.
