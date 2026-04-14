# 🧠 Big Idea (1 line)

👉 **Kustomize helps you avoid copying the same YAML files for different environments (dev, staging, prod)**

---

# 🔴 The Problem (what he is explaining)

You have 1 app (nginx), but 3 environments:

* Dev → 1 pod
* Staging → 2 pods
* Prod → 5 pods

---

## ❌ Bad approach (what people first do)

👉 Create 3 folders:

```id="f6dks1"
dev/
staging/
prod/
```

👉 Copy SAME YAML file into all 3

👉 Then change only this:

```yaml id="7wmp3z"
replicas: 1 (dev)
replicas: 2 (staging)
replicas: 5 (prod)
```

---

## ❌ Problem with this approach

* Too much **copy-paste**
* Hard to maintain
* Easy to forget changes 😵

Example:

* You add a new service
  👉 You must copy it into all folders

👉 If you forget → environments become inconsistent ❌

---

# ✅ Solution: Kustomize

👉 Instead of copying everything:

✔ Keep **one base config**
✔ Only override what changes

---

# 🔑 Two Important Concepts

---

## 1️⃣ Base (common stuff)

👉 Base = **default config**

Example:

```yaml id="r62pf9"
replicas: 1
image: nginx
```

✔ This is shared by ALL environments

---

## 2️⃣ Overlays (changes per env)

👉 Overlay = **only changes**

Example:

### staging overlay:

```yaml id="ozu6ta"
replicas: 2
```

### prod overlay:

```yaml id="z9p4q7"
replicas: 5
```

✔ Only overriding what’s different

---

# 🔁 How it works (simple flow)

1. Base config (common YAML)
2. Overlay (environment changes)
3. Kustomize combines them

👉 Final result = ready Kubernetes YAML

---

# 📂 Folder Structure (easy view)

```text id="19m9jh"
base/
  deployment.yaml

overlays/
  dev/
  staging/
  prod/
```

---

# 🔥 Why Kustomize is useful

✔ No duplication
✔ Easy to manage
✔ Scalable (works for big projects)
✔ Less mistakes

---

# ⚡ Bonus Point (important)

👉 Kustomize is already built into `kubectl`

```bash id="fp2p1m"
kubectl apply -k overlays/prod
```

---

# ⚖️ Kustomize vs Helm (simple)

| Kustomize       | Helm                       |
| --------------- | -------------------------- |
| Plain YAML      | Uses templates             |
| Simple          | More powerful but complex  |
| No new language | Needs templating knowledge |

---

# 🎯 What he is trying to teach

👉 Don’t copy YAML for each environment
👉 Use:

* Base → common config
* Overlay → environment changes

---

# 🧠 Final Simple Summary

👉 **Kustomize = reuse + customize YAML**

* Base = common
* Overlay = changes
* Final YAML = base + overlay

---

# 🧠 One-line memory trick

👉 **“Write once, customize everywhere”**

---

🎯 What he is trying to teach

👉 Both tools solve same problem
👉 But:

Kustomize = simple + clean
Helm = powerful + complex

👉 Choose based on your project

🔥 Final Simple Summary

## 👉 Helm:

Uses templates + values
More features
More complex

## 👉 Kustomize:

Uses base + overlays
Simple
Easy to manage

## 🧠 One-line memory trick

👉 Helm = powerful but complex | Kustomize = simple but limited

#####################################################################################################################################################################################################################################################################################################################################################################################


---

# 🧠 Think like this (very simple analogy)

👉 You have **2 files**:

* deployment.yaml
* service.yaml

👉 But you want to:

* add something extra (like a label)
* or change something

👉 Instead of editing each file manually…

👉 You create **ONE control file**:

```
kustomization.yaml
```

---

# 🧃 Simple Analogy (very easy)

👉 Think:

* deployment.yaml + service.yaml = ingredients 🍅🥕
* kustomization.yaml = recipe 📖

👉 Recipe tells:

* what ingredients to use
* what changes to apply

---

# 🔑 What `kustomization.yaml` really does

👉 It just answers 2 questions:

---

## 1️⃣ Which files should I use?

```yaml
resources:
  - deployment.yaml
  - service.yaml
```

👉 Means:
👉 “Use these files”

---

## 2️⃣ What changes should I apply?

```yaml
commonLabels:
  company: KodeKloud
```

👉 Means:
👉 “Add this label to everything”

---

# 🔁 What happens when you run command

```bash
kustomize build k8s/
```

👉 It does this:

1. Reads `kustomization.yaml`
2. Loads your YAML files
3. Adds changes (label etc.)
4. Shows final result

---

# ⚠️ Important (this is where most people get confused)

👉 This command:

```bash
kustomize build
```

❌ DOES NOT create anything in Kubernetes

👉 It only shows:
👉 “This is what I will create”

---

# 🚀 To actually create in Kubernetes

```bash
kustomize build k8s/ | kubectl apply -f -
```

👉 Now it gets deployed ✔

---

# 🔥 Ultra Simple Example

### Without Kustomize:

You manually edit:

* deployment.yaml
* service.yaml

😩 Hard work

---

### With Kustomize:

You just write:

```yaml
commonLabels:
  company: KodeKloud
```

👉 Automatically added everywhere ✔

---

# 🎯 Final Understanding

👉 `kustomization.yaml` = boss file

It tells:

* what files to use
* what changes to apply

---
👉 **Kustomize only prepares YAML… you still need `kubectl` to apply it**

---

# 🔴 Step 1: What you already learned

```bash
kustomize build k8s/
```

👉 This does:

* reads files
* applies changes
* shows final YAML

❌ BUT → does NOT create anything in Kubernetes

---

# 🤔 So how to actually create resources?

👉 You need to send that output to Kubernetes

---

# 🧪 Simple Concept (IMPORTANT)

👉 Think like this:

* `kustomize build` = prepares file 📄
* `kubectl apply` = sends it to cluster 🚀
---

# 🚀 Shortcut (Easier way)

Instead of long command:

```bash
kubectl apply -k k8s/
```

👉 `-k` means:
👉 “use Kustomize here”

✔ Same result, shorter command

---

---

## Option 1 (pipe way)

```bash
kustomize build k8s/ | kubectl delete -f -
```

---

## Option 2 (easy way)

```bash
kubectl delete -k k8s/
```

---
# 🔥 Final Simple Summary

👉 Commands you must remember:

* Show config:

  ```bash
  kustomize build k8s/
  ```

* Apply:

  ```bash
  kubectl apply -k k8s/
  ```

* Delete:

  ```bash
  kubectl delete -k k8s/
  ```

---



