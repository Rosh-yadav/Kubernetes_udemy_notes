Step 6: Important Use Case (VERY IMPORTANT)
🧩 Example: ReplicaSet
Pod:
labels:
  app: myapp
ReplicaSet:
selector:
  matchLabels:
    app: myapp

👉 Meaning:
👉 ReplicaSet will manage all pods with app=myapp

⚠️ Common Mistake (IMPORTANT)

👉 Labels appear in TWO places:

Pod labels (inside template) ✅ (important)
ReplicaSet labels (top) ❌ (less important here)

👉 Always match selector with pod labels

🌐 Step 7: Service Example

Service uses selector:

selector:
  app: myapp

👉 Meaning:
👉 Service will send traffic to pods with app=myapp
