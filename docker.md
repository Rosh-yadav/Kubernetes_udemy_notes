## ⚠️ Important confusion he cleared

👉 Many people think:

command = CMD ❌

👉 But actually:

command = ENTRYPOINT ✔️
args = CMD ✔️
💡 Final one-line understanding

👉 He is teaching:

How to change container behavior in Kubernetes using command and args


# 🧩 Step 1: Important Case (Multiple Containers)

👉 A pod can have **multiple containers**

Example:

* Container 1 → event-simulator
* Container 2 → image-processor

---

## ❓ Problem

If you run:

```bash id="cmd12"
kubectl logs <pod-name>
```

👉 Kubernetes gets confused ❌
👉 “Which container?”

---

## ✅ Solution

You must specify container name:

```bash id="cmd13"
kubectl logs <pod-name> -c <container-name>
```-

### Example:

```bash id="cmd14"
kubectl logs mypod -c event-simulator
```

---
👉 Multiple containers?
→ Use `-c container-name`

---


