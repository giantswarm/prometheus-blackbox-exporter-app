# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project's packages adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Probe `github.com`, `gsoci.azurecr.io` and `grafana.com` from every node (targets `egress-github`, `egress-registry`, `egress-grafana`), so an allowlist-style firewall change blocking a single domain becomes visible. The new `serviceMonitor.externalTargets` value is a map so per-installation, per-region or per-customer overrides can disable, change or add individual entries without copying the whole list. A separate `serviceMonitor.additionalExternalTargets` key takes regional/customer additions, structurally separated from the Giant Swarm defaults. Adds the `http_2xx_or_401` module for registry endpoints that answer unauthenticated requests with 401. See giantswarm/giantswarm#33409.
- Add the `http_2xx_egress` module, used by the internet egress targets. It carries a 15s timeout so `probe_success` reports whether an endpoint is reachable rather than whether it is fast. It is a separate module rather than a longer timeout on `http_2xx` because several installations pin `http_2xx` in their own custom values, which would silently revert the change there.

### Fixed

- Give the internet egress targets a probe deadline above the cross-border baseline: `scrapeTimeout: 20s` on `http-giantswarm`, `egress-github`, `egress-registry` and `egress-grafana`, and a 15s timeout on `http_2xx_or_401`. The exporter applies `min(module timeout, scrapeTimeout - 0.5s offset)`, so the 5s `serviceMonitor.defaults.scrapeTimeout` capped every probe at a 4.5s deadline and raising a module timeout alone had no effect. Installations whose baseline latency is a large fraction of that deadline crossed it on endpoints that were still returning HTTP 200, making `probe_success` report latency rather than reachability.
- Point the `dns-tcp-internal` and `dns-udp-internal` ServiceMonitors at the `dns_*_internal` modules. They referenced the `_external` modules, so both probed `www.prometheus.io` and in-cluster DNS resolution was never monitored.

### Removed

- Remove the inert `instance` metric relabeling from the ServiceMonitor template. It interpolated a `url` field that no target defines, so it rendered empty and Prometheus fell back to its `$1` default, leaving `instance` unchanged.

## [0.9.0] - 2026-07-27

### Added

- Add VPA for `blackbox-exporter`. Uses `updateMode: Initial` for DaemonSet and `updateMode: Auto` for Deployment.

### Fixed

- Add `probe_target` label to ensure unique synthetic metrics

## [0.8.0] - 2026-05-28

### Added

- Add toleration for `kubernetes.io/arch=arm64:NoSchedule` so the DaemonSet schedules on ARM worker nodes.

## [0.7.0] - 2026-03-24

### Added

- Add `http_2xx_insecure` module with `insecure_skip_verify: true` to support probing workload cluster API servers from the management cluster. The MC's service account CA (`http_2xx_k8sca`) only covers the MC itself; workload clusters have their own CA which is not available to the blackbox exporter, making TLS verification impossible without this module.

## [0.6.0] - 2026-03-17

### Changed

- Set `priorityClassName` to `system-node-critical` to ensure DaemonSet pods are scheduled even on full nodes.

## [0.5.1] - 2026-02-19

### Changed

- Migrate to App Build Suite (ABS) for Helm chart building.

## [0.5.0] - 2025-01-27

### Changed

- Harden security context to pass PSS compliance.

### Removed

- Remove PSP resources.

## [0.4.2] - 2024-06-25

### Fixed

- Remove duplicated team label.

## [0.4.1] - 2023-12-20

### Changed

- Configure `gsoci.azurecr.io` as the default container image registry.

## [0.4.0] - 2023-10-18

### Added

- Add `global.podSecurityStandards.enforced` value for PSS migration.

## [0.3.2] - 2023-04-25

### Added

- Add icon.

## [0.3.1] - 2023-03-16

### Fixed

- Change image registry for DaemonSet.

## [0.3.0] - 2023-03-16

### Changed

- Change image registry.

## [0.2.2] - 2023-02-24

### Changed

- Add IRSA webhook module
- Fix k8s CA for API probe
- Use IPV4 by default

## [0.2.1] - 2023-02-14

### Changed

- Change default timeouts and scraping configuration

## [0.2.0] - 2023-02-09

### Added

- Allow cluster domain customization on servicemonitors and modules.
- Add json schema.

### Changed

- Default interval to 10 seconds on all probes.

## [0.1.0] - 2023-02-07

### Added

- First release featuring upstream version 7.5.0.

[Unreleased]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.9.0...HEAD
[0.9.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.8.0...v0.9.0
[0.8.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.7.0...v0.8.0
[0.7.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.6.0...v0.7.0
[0.6.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.5.1...v0.6.0
[0.5.1]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.5.0...v0.5.1
[0.5.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.4.2...v0.5.0
[0.4.2]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.4.1...v0.4.2
[0.4.1]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.4.0...v0.4.1
[0.4.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.3.2...v0.4.0
[0.3.2]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.3.1...v0.3.2
[0.3.1]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.2.2...v0.3.0
[0.2.2]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.2.1...v0.2.2
[0.2.1]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.1.0...v0.2.1
[0.2.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.0.0...v0.1.0
