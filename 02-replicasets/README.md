📁 REPLICASET LAB - README
1️⃣ replicaset.yaml (Basic ReplicaSet)
bash

# Apply
kubectl apply -f replicaset.yaml

# Test
kubectl get rs
kubectl get pods
kubectl delete pod <pod-name>  # Test self-healing
kubectl get pods  # New pod created automatically

What: 3 ota nginx pods manage garne ReplicaSet. Pod delete garepachi feri create garxa.
2️⃣ scaling-demo.yaml (Scale ReplicaSet)
bash

# Apply
kubectl apply -f scaling-demo.yaml

# Scale up
kubectl scale rs nginx-rs --replicas=5
kubectl get pods  # 5 pods bhayeko check

# Scale down
kubectl scale rs nginx-rs --replicas=2
kubectl get pods  # 2 pods matrai bhayeko check

What: Scaling demonstration - replicas badhaune/ghataune.
3️⃣ label-mismatch-demo.yaml (Common Mistake Demo)
bash

# Apply
kubectl apply -f label-mismatch-demo.yaml

# Observe
kubectl get rs
kubectl get pods  # Pods create bhayena!
kubectl describe rs mismatch-rs
# Events ma "selector mismatch" error dekhincha

What: Selector ra template labels mismatch vayo bhane pods create hudaina - common mistake siknu.
📋 QUICK REFERENCE COMMANDS
bash

# Apply all
kubectl apply -f replicaset.yaml
kubectl apply -f scaling-demo.yaml
kubectl apply -f label-mismatch-demo.yaml

# List ReplicaSets
kubectl get rs
kubectl get rs -o wide

# List pods
kubectl get pods --show-labels

# Scale
kubectl scale rs nginx-rs --replicas=5
kubectl scale rs scaling-rs --replicas=3

# Delete specific
kubectl delete rs nginx-rs
kubectl delete rs scaling-rs
kubectl delete rs mismatch-rs

# Delete all
kubectl delete rs --all
kubectl delete pods --all

🎯 WHAT EACH DEMONSTRATES
File	Purpose	Key Learning
replicaset.yaml	Basic ReplicaSet	Self-healing, desired replicas
scaling-demo.yaml	Scaling	kubectl scale command
label-mismatch-demo.yaml	Label mismatch	Selector vs template labels must match
🔍 IMPORTANT OBSERVATIONS
Self-healing Test:
bash

kubectl get pods
# Pick one pod name
kubectl delete pod <pod-name>
kubectl get pods  # New pod with different name created!

Scale Test:
bash

kubectl get rs
# Watch replicas change
kubectl scale rs nginx-rs --replicas=5
kubectl get pods -w  # Watch new pods create

Label Mismatch Error:
bash

kubectl describe rs mismatch-rs
# Events ma: "selector does not match template labels"

✅ CHECKLIST

    replicaset.yaml: 3 pods running

    replicaset.yaml: Delete pod → new pod created

    scaling-demo.yaml: Scale to 5 → 5 pods running

    scaling-demo.yaml: Scale to 2 → 2 pods running

    label-mismatch-demo.yaml: 0 pods (intentional error)

    label-mismatch-demo.yaml: Describe shows mismatch error

⚠️ COMMON MISTAKES (LEARN FROM LABEL-MISMATCH!)
yaml

# WRONG (pods not created)
selector:
  matchLabels:
    app: nginx
template:
  metadata:
    labels:
      app: wrong-label  # ❌ Mismatch!

yaml

# CORRECT (pods created)
selector:
  matchLabels:
    app: nginx
template:
  metadata:
    labels:
      app: nginx  # ✅ Must match!

📝 QUICK NOTES

    ReplicaSet = Pods ko duplicate machine

    Desired = Current = Ready huna parcha

    Selector = "Kun pods manage garne?"

    Template = "Kasto pods banaune?"

    Scaling = kubectl scale command

    Label mismatch = Pods create hudaina!
