Helm CLI Commands — v4.3.0

A practical reference for commonly used Helm CLI commands for managing Kubernetes applications and Helm charts.

📌 Version

helm version

Helm Version: 4.3.0


---

📚 Command Reference

🔹 Helm

Display general Helm information and available commands.

helm


---

🔹 Shell Autocompletion

Generate autocompletion scripts for different shells.

Shell	Command

Bash	helm completion bash
Fish	helm completion fish
PowerShell	helm completion powershell
Zsh	helm completion zsh


Example:

helm completion bash


---

🔹 Chart Creation

Create a new Helm chart.

helm create <chart-name>

Example:

helm create my-app

This creates a standard Helm chart structure containing:

my-app/
├── Chart.yaml
├── values.yaml
├── charts/
├── templates/
└── templates/tests/


---

📦 Dependencies

Manage dependencies required by a Helm chart.

Dependency

helm dependency

Build Dependencies

Rebuild the charts/ directory using Chart.lock.

helm dependency build <chart>

List Dependencies

helm dependency list <chart>

Update Dependencies

Update dependencies based on Chart.yaml.

helm dependency update <chart>


---

⚙️ Helm Environment

Display Helm client environment information.

helm env


---

🔍 Release Information

Helm releases are installed instances of charts.

List Releases

helm list

Example:

helm list -A

List releases across all namespaces.


---

Release Status

helm status <release-name>

Example:

helm status nginx


---

Release History

View previous revisions of a release.

helm history <release-name>

Example:

helm history nginx


---

📄 Get Release Information

Get All Information

helm get all <release-name>

Get Hooks

helm get hooks <release-name>

Get Manifest

View the Kubernetes manifests generated for a release.

helm get manifest <release-name>

Get Metadata

helm get metadata <release-name>

Get Notes

helm get notes <release-name>

Get Values

helm get values <release-name>

Example:

helm get values nginx

To see all values, including defaults:

helm get values nginx --all


---

🚀 Install

Install a Helm chart as a release.

helm install <release-name> <chart>

Example:

helm install nginx ./nginx-chart

Install into a specific namespace:

helm install nginx ./nginx-chart -n production

Create the namespace if it doesn't exist:

helm install nginx ./nginx-chart \
  -n production \
  --create-namespace


---

🔄 Upgrade

Upgrade an existing Helm release.

helm upgrade <release-name> <chart>

Example:

helm upgrade nginx ./nginx-chart

Upgrade using a custom values file:

helm upgrade nginx ./nginx-chart \
  -f values-prod.yaml


---

↩️ Rollback

Roll back a release to an earlier revision.

helm rollback <release-name> <revision>

Example:

helm rollback nginx 2

Check the revision history first:

helm history nginx


---

🗑️ Uninstall

Remove a Helm release.

helm uninstall <release-name>

Example:

helm uninstall nginx


---

🔎 Search Charts

Search Artifact Hub

helm search hub <keyword>

Example:

helm search hub nginx

Search Configured Repositories

helm search repo <keyword>

Example:

helm search repo prometheus


---

📦 Helm Repositories

Add Repository

helm repo add <repo-name> <repo-url>

Example:

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

List Repositories

helm repo list

Update Repository Information

helm repo update

Remove Repository

helm repo remove <repo-name>

Example:

helm repo remove prometheus-community

Generate Repository Index

helm repo index <directory>


---

📋 Show Chart Information

Show Everything

helm show all <chart>

Show Chart Definition

helm show chart <chart>

Show CRDs

helm show crds <chart>

Show README

helm show readme <chart>

Show Default Values

helm show values <chart>

Example:

helm show values prometheus-community/prometheus

This is particularly useful before installing a third-party chart.


---

🧪 Lint

Check a chart for potential problems.

helm lint <chart>

Example:

helm lint ./my-app


---

🖨️ Template

Render Helm templates locally without installing them into Kubernetes.

helm template <release-name> <chart>

Example:

helm template nginx ./nginx-chart

Using custom values:

helm template nginx ./nginx-chart \
  -f values-prod.yaml

This is extremely useful for debugging generated Kubernetes manifests.


---

📦 Package

Package a Helm chart into a .tgz archive.

helm package <chart-directory>

Example:

helm package ./my-app

Output:

my-app-0.1.0.tgz


---

📥 Pull

Download a chart from a repository.

helm pull <chart>

Example:

helm pull prometheus-community/prometheus

Download and extract:

helm pull prometheus-community/prometheus --untar


---

📤 Push

Push a packaged chart to a remote registry.

helm push <chart.tgz> <registry>


---

🔐 Helm Registry

Login

helm registry login <registry>

Example:

helm registry login registry.example.com

Logout

helm registry logout <registry>


---

🔌 Helm Plugins

Manage Helm plugins.

List Plugins

helm plugin list

Install Plugin

helm plugin install <url>

Update Plugin

helm plugin update <plugin>

Uninstall Plugin

helm plugin uninstall <plugin>

Package Plugin

helm plugin package <directory>

Verify Plugin

helm plugin verify <path>


---

🧪 Helm Test

Run tests associated with an installed release.

helm test <release-name>

Example:

helm test nginx


---

🔏 Chart Verification

Verify that a chart has been signed and is valid.

helm verify <chart>


---

ℹ️ Helm Version

Display Helm version information.

helm version

Example output:

version.BuildInfo{
  Version:"v4.3.0",
  ...
}


---

🧠 Most Important Commands to Remember

If you're learning Helm for DevOps/Kubernetes, don't try to memorize every command. Start with these:

# Create
helm create my-app

# Repository
helm repo add <name> <url>
helm repo update
helm repo list

# Search
helm search repo <keyword>

# Inspect
helm show values <chart>
helm show readme <chart>

# Install
helm install <release> <chart>

# Check
helm list
helm status <release>
helm get values <release>
helm get manifest <release>

# Debug
helm lint <chart>
helm template <release> <chart>

# Upgrade
helm upgrade <release> <chart>

# History / Rollback
helm history <release>
helm rollback <release> <revision>

# Remove
helm uninstall <release>

🔄 Typical Helm Workflow

Helm Repository
              │
              ▼
      helm search repo
              │
              ▼
       helm show values
              │
              ▼
        Customize values
              │
              ▼
         helm install
              │
              ▼
        helm status
              │
              ▼
        helm upgrade
              │
              ▼
        helm history
              │
              ▼
        helm rollback
              │
              ▼
        helm uninstall

> Tip: helm template + helm lint should become part of your normal workflow before installing or upgrading charts. They catch a lot of problems before those problems hit the cluster.
