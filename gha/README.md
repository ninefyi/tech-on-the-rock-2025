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

## Automated Deployment & Security Pipeline

The GitHub Actions workflow (`.github/workflows/security-scan.yml`) implements a two-stage pipeline:

1.  **Deployment Stage**:
    *   Triggered automatically on `push` to the `gha/**` directory.
    *   Uses the `cloudflare/pages-action` to build and deploy the site to Cloudflare Pages.
    *   Outputs the dynamic deployment URL for the next stage.

2.  **Security Scan Stage**:
    *   Runs immediately after a successful deployment.
    *   Performs an **OWASP ZAP Baseline Scan** against the live URL.
    *   Also supports `deployment_status` events (for external deployments) and manual `workflow_dispatch` triggers.

### Workflow Features

- **Integrated Deployment**: No need to manually trigger Cloudflare; the workflow handles the sync.
- **Dynamic Targeting**: Automatically passes the newly created deployment URL to the ZAP scanner.
- **Artifact Retention**: Generates an HTML security report and stores it as a GitHub Action artifact for 5 days.

## Getting Started

### 1. Prerequisites
Ensure you have the following secrets configured in your GitHub Repository (**Settings > Secrets and variables > Actions**):
*   `CLOUDFLARE_API_TOKEN`: Your Cloudflare API token (with Pages edit permissions).
*   `CLOUDFLARE_ACCOUNT_ID`: Your Cloudflare Account ID.

### 2. Deployment
*   The workflow is configured to deploy to a project named `gha-workshop-demo`. Update the `projectName` in the YAML file if yours differs.
*   Push any changes to the `gha/` folder to trigger the pipeline.

### 3. Verification
*   **Monitor Actions**: Check the "Actions" tab in GitHub to see the deployment and security scan progress.
*   **Review Reports**: Download the "ZAP Security Report" artifact from successful workflow runs to audit your site's security.