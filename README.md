# Install

`helm install blackbox-exporter helm/prometheus-blackbox-exporter -n kube-system -f custom-values.yaml`

# Upgrade

`helm upgrade blackbox-exporter helm/prometheus-blackbox-exporter -n kube-system -f custom-values.yaml`

# References

- Project https://github.com/prometheus/blackbox_exporter
- Helm Chart https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus-blackbox-exporter