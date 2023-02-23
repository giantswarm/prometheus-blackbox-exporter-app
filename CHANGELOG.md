# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project's packages adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

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

[Unreleased]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.2.1...HEAD
[0.2.1]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.1.0...v0.2.1
[0.2.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/giantswarm/prometheus-blackbox-exporter-app/compare/v0.0.0...v0.1.0
