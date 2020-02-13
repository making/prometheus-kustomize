```
kubectl create -n monitoring configmap grafana-dashboard-micrometer \
  --from-file=base/grafana/spring-boot.json \
  --from-file=base/grafana/jvm.json \
  --dry-run -oyaml > base/grafana-micrometer.yml

kubectl create -n monitoring configmap grafana-dashboard-zipkin \
  --from-file=base/grafana/zipkin.json \
  --dry-run -oyaml > base/grafana-zipkin.yml

kubectl create -n monitoring configmap grafana-dashboard-spring-cloud-gateway \
  --from-file=base/grafana/spring-cloud-gateway.json \
  --dry-run -oyaml > base/grafana-spring-cloud-gateway.yml

kubectl create -n monitoring configmap grafana-dashboard-ingress-nginx \
  --from-file=base/grafana/ingress-nginx.json \
  --dry-run -oyaml > base/grafana-ingress-nginx.yml

kubectl create -n monitoring configmap grafana-dashboard-system \
  --from-file=base/grafana/system-overview.json \
  --from-file=base/grafana/system-disk-space.json \
  --from-file=base/grafana/system-disk-performance.json \
  --dry-run -oyaml > base/grafana-system.yml

kubectl create -n monitoring configmap grafana-dashboard-postgres \
  --from-file=base/grafana/postgres-overview.json \
  --dry-run -oyaml > base/grafana-postgres.yml

kubectl create -n monitoring configmap grafana-dashboard-bosh \
  --from-file=base/grafana/bosh-jobs.json \
  --from-file=base/grafana/bosh-overview.json \
  --from-file=base/grafana/bosh-processes.json \
  --from-file=base/grafana/bosh-system-disk-performance.json \
  --from-file=base/grafana/bosh-system-disk-space.json \
  --from-file=base/grafana/bosh-system-overview.json \
  --dry-run -oyaml > base/grafana-bosh.yml

kubectl create -n monitoring configmap grafana-dashboard-probe \
  --from-file=base/grafana/probe-https-summary.json \
  --dry-run -oyaml > base/grafana-probe.yml

kubectl create -n monitoring secret generic additional-scrape-configs \
  --from-file=base/prometheus/prometheus-additional.yml \
  --dry-run -o yaml > base/additional-scrape-configs.yml

kubectl create -n monitoring secret generic alertmanager-main \
  --from-file=base/alertmanager/alertmanager.yaml \
  --dry-run -oyaml > base/alertmanager-secret.yml

GF_SECURITY_ADMIN_PASSWORD=..........
kubectl create -n monitoring secret generic grafana-secret \
  --from-literal=grafana-password=${GF_SECURITY_ADMIN_PASSWORD} \
  --dry-run -oyaml > base/grafana-secret.yml

kubectl kustomize overlays | kubectl diff -f -
kubectl kustomize overlays | kubectl apply -f -
```