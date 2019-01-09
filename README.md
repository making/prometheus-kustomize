```
kubectl create -n monitoring configmap grafana-dashboard-micrometer \
  --from-file=base/grafana/micrometer.json \
  --dry-run -oyaml > base/grafana-micrometer.yml

kubectl create -n monitoring configmap grafana-dashboard-hystrix \
  --from-file=base/grafana/hystrix.json \
  --dry-run -oyaml > base/grafana-hystrix.yml

kubectl create -n monitoring configmap grafana-dashboard-zipkin \
  --from-file=base/grafana/zipkin.json \
  --dry-run -oyaml > base/grafana-zipkin.yml

kubectl create -n monitoring configmap grafana-dashboard-spring-cloud-gateway \
  --from-file=base/grafana/spring-cloud-gateway.json \
  --dry-run -oyaml > base/grafana-spring-cloud-gateway.yml

kubectl create -n monitoring configmap grafana-dashboard-ingress-nginx \
  --from-file=base/grafana/ingress-nginx.json \
  --dry-run -oyaml > base/grafana-ingress-nginx.yml

kubectl create -n monitoring configmap grafana-dashboard-pks \
  --from-file=wavefront-proxy-exporter/grafana/overview.json \
  --from-file=wavefront-proxy-exporter/grafana/namespace.json \
  --from-file=wavefront-proxy-exporter/grafana/node.json \
  --from-file=wavefront-proxy-exporter/grafana/pod.json \
  --from-file=wavefront-proxy-exporter/grafana/pod-container.json \
  --from-file=wavefront-proxy-exporter/grafana/deployment.json \
  --dry-run -o yaml > base/grafana-pks.yml

kubectl create -n monitoring secret generic additional-scrape-configs \
  --from-file=base/prometheus/prometheus-additional.yml \
  --dry-run -o yaml > base/additional-scrape-configs.yml

kubectl create -n monitoring secret generic alertmanager-main \
  --from-file=base/alertmanager/alertmanager.yaml \
  --dry-run -oyaml > alertmanager-secret.yml

kustomize build overlays | kubectl apply -f -							
```