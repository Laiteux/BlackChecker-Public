# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.4] - 2020-06-11

### Added

- Filter proxies with invalid port (>65535)

### Fixed

- Fixed insecure worth being included twice in total hits worth

## [1.0.3] - 2020-05-30

### Changed

- Removed extra "%" characters from console title & Discord progress webhook.

## [1.0.2] - 2020-05-28

### Fixed

- Fixed a bug with `internal` models properties not being seen by `JsonSerializer` reflection, causing no hit to be obtained as well as other issues.
- Fixed a bug with check ID always changing when requesting custom webhook.

## [1.0.1] - 2020-05-24

### Fixed

- Fixed a bug preventing checker to start.