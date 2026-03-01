📁 01-PODS LAB - README
1️⃣ simple-pod.yaml (Basic Nginx)
bash

# Apply
kubectl apply -f simple-pod.yaml

# Test
kubectl get pods
kubectl port-forward nginx-pod 8080:80
# Browser: http://localhost:8080

What: Euta simple nginx web server chalauxa port 80 ma.
2️⃣ multi-container-pod.yaml (Sidecar Pattern)
bash

# Apply
kubectl apply -f multi-container-pod.yaml

# Test
kubectl get pods
kubectl logs nginx-with-sidecar -c log-sidecar -f
# New terminal:
kubectl exec nginx-with-sidecar -c nginx -- curl localhost

What: Nginx + log sidecar (busybox) same pod ma, shared volume bata logs read garne.
3️⃣ resource-limits-pod.yaml (CPU Stress Demo)
bash

# Apply
kubectl apply -f resource-limits-pod.yaml

# Test
kubectl top pod stress-pod --containers
kubectl exec stress-pod -- cat /sys/fs/cgroup/cpu/cpu.stat

What: CPU stress tool chalauxa (200m request, 300m limit) - throttling observe garna.
4️⃣ debug-pod.yaml (Admin Debug Pod)
bash

# Apply
kubectl apply -f debug-pod.yaml

# Use
kubectl exec -it debug-pod -- sh
# Inside: nslookup, wget, ping commands use gara
# Exit: exit

What: Busybox container with sleep 3600 - network troubleshooting ko lagi.
📋 QUICK REFERENCE COMMANDS
bash

# Apply all
kubectl apply -f simple-pod.yaml
kubectl apply -f multi-container-pod.yaml
kubectl apply -f resource-limits-pod.yaml
kubectl apply -f debug-pod.yaml

# List pods
kubectl get pods -o wide

# Delete specific
kubectl delete pod nginx-pod
kubectl delete pod nginx-with-sidecar
kubectl delete pod stress-pod
kubectl delete pod debug-pod

# Delete all
kubectl delete pods --all

# Logs (multi-container)
kubectl logs nginx-with-sidecar -c nginx
kubectl logs nginx-with-sidecar -c log-sidecar

# Exec into
kubectl exec -it debug-pod -- sh
kubectl exec -it nginx-with-sidecar -c nginx -- sh

🎯 WHAT EACH DEMONSTRATES
Pod	Purpose
simple-pod	Basic pod creation, port-forward
multi-container	Sidecar pattern, shared volumes
resource-limits	CPU throttling, resource enforcement
debug-pod	Network troubleshooting, exec into pod
✅ CHECKLIST

    simple-pod: curl http://localhost:8080 works

    multi-container: Sidecar shows logs when curl run

    resource-limits: CPU throttling observed (cpu.stat)

    debug-pod: Can run nslookup, wget inside
