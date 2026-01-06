# Workshop: GitHub Actions Crash Course

This module focuses on setting up a secure CI/CD pipeline using GitHub Actions, Cloudflare Pages, and OWASP ZAP for automated security testing.

## Project Overview

The goal of this workshop is to demonstrate how to deploy a static web application and automatically perform a Dynamic Application Security Testing (DAST) scan to identify vulnerabilities.

### Key Components

- **Web Application**: A lightweight static site located in the `gha/` directory.
    - `index.html`: The main landing page.
    - `public/style.css`: Basic styling for the application.
- **CI/CD Pipeline**: Managed via GitHub Actions in `.github/workflows/security-scan.yml`.
- **Security Testing**: Integration with **OWASP ZAP (Zaproxy)** for baseline security scanning.
- **Deployment**: Optimized for **Cloudflare Pages**.

## Automated Security Pipeline

The security scan workflow is designed to be robust and flexible, supporting multiple triggers:

1.  **On Push**: Automatically runs when changes are detected in the `gha/**` folder.
2.  **On Deployment**: Triggers when Cloudflare Pages successfully completes a deployment to the production environment.
3.  **Manual Trigger**: Can be started manually via the GitHub "Actions" tab with a custom target URL.

### Workflow Features

- **Dynamic Targeting**: Automatically detects the deployment URL or uses a manual override.
- **Artifact Retention**: Generates an HTML security report and stores it as a GitHub Action artifact for 5 days.
- **Baseline Scan**: Performs a non-intrusive scan to find common web vulnerabilities.

## Getting Started

1.  **Deploy to Cloudflare**: Link this repository to a Cloudflare Pages project and set the build output directory to `gha`.
2.  **Monitor Actions**: Check the "Actions" tab in GitHub to see the security scan results.
3.  **Review Reports**: Download the "ZAP Security Report" artifact from successful workflow runs to audit your site's security.