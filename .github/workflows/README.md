# GitHub Actions Workflows

This directory contains the CI/CD workflows for the g3 project.

## Workflows

### 1. CI (`ci.yml`)
**Triggers:** Push to `main` or `develop` branches, Pull Requests

**Jobs:**
- **Test**: Runs tests on Ubuntu, macOS, and Windows
  - Format checking (`cargo fmt`)
  - Linting with Clippy (`cargo clippy`)
  - Build verification
  - Unit and integration tests
  - Documentation tests
  
- **Build**: Creates release builds for all platforms
  - Uploads build artifacts for download
  
- **Coverage**: Generates code coverage reports
  - Uses `cargo-tarpaulin`
  - Uploads to Codecov (optional)

### 2. Quick Check (`quick-check.yml`)
**Triggers:** Push to any branch except `main`, Pull Requests

**Jobs:**
- **Quick Check**: Fast verification on Ubuntu only
  - Format checking
  - Clippy linting
  - Build check
  - Run tests

This workflow is designed for rapid feedback during development.

## System Dependencies

The workflows automatically install required system dependencies:

**Ubuntu:**
- `libx11-dev`
- `libxdo-dev`
- `libxcb-shape0-dev`
- `libxcb-xfixes0-dev`

**macOS:** No additional dependencies required

**Windows:** No additional dependencies required

## Caching

All workflows use GitHub Actions cache to speed up builds:
- Cargo registry
- Cargo git index
- Build artifacts (`target/` directory)

## Artifacts

The CI workflow produces downloadable artifacts:
- `g3-ubuntu-latest`: Linux binaries
- `g3-macos-latest`: macOS binaries
- `g3-windows-latest`: Windows binaries

## Adding Badges to README

Add these badges to your main README.md:

```markdown
[![CI](https://github.com/YOUR_USERNAME/g3/actions/workflows/ci.yml/badge.svg)](https://github.com/YOUR_USERNAME/g3/actions/workflows/ci.yml)
[![Quick Check](https://github.com/YOUR_USERNAME/g3/actions/workflows/quick-check.yml/badge.svg)](https://github.com/YOUR_USERNAME/g3/actions/workflows/quick-check.yml)
```

Replace `YOUR_USERNAME` with your GitHub username or organization name.
