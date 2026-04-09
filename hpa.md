🤔 Why do we need Request?

👉 For scheduling (placement of pod)

Kubernetes uses request to decide:

👉 “Which node has enough resources to run this pod?”

Without request:
❌ Scheduler can’t decide properly
❌ Pods may fail or compete badly

🤔 Why do we need Limit?

👉 To prevent one pod from using everything

Without limit:
❌ One container can consume all CPU
❌ Other apps will suffer
