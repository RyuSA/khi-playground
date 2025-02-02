Playground
===

```
# create a kind cluster
kind create cluster --config ./config.yaml

# install fluent-bit
kubectl apply -f ./manifests/

kubectl create deploy nginx --image nginx --replicas 3
kubectl rollout status deploy/nginx

kubectl scale deploy nginx --replicas 8
kubectl rollout status deploy/nginx

kubectl rollout restart deploy/nginx
kubectl rollout status deploy/nginx

kubectl scale deploy/nginx --replicas 3
kubectl rollout status deploy/nginx

kubectl delete deploy nginx

docker exec -e SYSTEMD_COLORS=false -it kind-control-plane journalctl --until "2025-02-02 20:46:56" --no-pager -u kubelet -o json > mnt/kind-control-plane/journal/kubelet.json
docker exec -e SYSTEMD_COLORS=false -it kind-control-plane journalctl --until "2025-02-02 20:46:56" --no-pager -u containerd -o json > mnt/kind-control-plane/journal/containerd.json

docker exec -e SYSTEMD_COLORS=false -it kind-worker journalctl --until "2025-02-02 20:46:56" --no-pager -u containerd -o json > mnt/kind-worker/journal/containerd.json
docker exec -e SYSTEMD_COLORS=false -it kind-worker journalctl --until "2025-02-02 20:46:56" --no-pager -u kubelet -o json > mnt/kind-worker/journal/kubelet.json

docker exec -e SYSTEMD_COLORS=false -it kind-worker2 journalctl --until "2025-02-02 20:46:56" --no-pager -u containerd -o json > mnt/kind-worker2/journal/containerd.json
docker exec -e SYSTEMD_COLORS=false -it kind-worker2 journalctl --until "2025-02-02 20:46:56" --no-pager -u kubelet -o json > mnt/kind-worker2/journal/kubelet.json

docker exec -e SYSTEMD_COLORS=false -it kind-worker3 journalctl --until "2025-02-02 20:46:56" --no-pager -u containerd -o json > mnt/kind-worker3/journal/containerd.json
docker exec -e SYSTEMD_COLORS=false -it kind-worker3 journalctl --until "2025-02-02 20:46:56" --no-pager -u kubelet -o json > mnt/kind-worker3/journal/kubelet.json

kind delete cluster
tar -czvf k8s.tar.gz mnt/
```
