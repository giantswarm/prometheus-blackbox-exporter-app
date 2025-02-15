# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project's packages adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

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

[Unreleased]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.5.0...HEAD
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
