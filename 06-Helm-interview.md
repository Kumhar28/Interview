# Kubernetes Helm Basics:
## Commands
## HELM Commands Cheat Sheet

**Table of Contents:**
- [HELM Commands Cheat Sheet](#helm-commands-cheat-sheet)
  - [Helm Basics](#helm-basics)
  - [Chart Configuration](#chart-configuration)
  - [Working with Repositories](#working-with-repositories)
  - [Hooks and Lifecycle Management](#hooks-and-lifecycle-management)
  - [Helm Security](#helm-security)

### Helm Basics

- `helm create <chart-name>`: Create a new Helm chart.
- `helm install <release-name> <chart-name>`: Install a chart and create a release. 
- `helm upgrade <release-name> <chart-name> --dry-run` : dryrun
- `helm uninstall <release-name>`: Uninstall a release and remove the associated resources.
- `helm list`: List all installed releases.
- `helm status <release-name>`: Show the status of a release.
- `helm rollback <release-name> <revision-number>`: Rollback a release to a specific revision.
- `helm history <release-name>`: Show the revision history of a release.
- `helm dependency update`: Update the dependencies of a chart.
- `helm dependency build`: Build the dependencies of a chart.
- `helm template <chart-name>`: Render the templates of a chart without installing it.
- `helm lint <chart-name>`: Lint a chart for best practices and errors.
- `helm package <chart-directory>`: Package a chart into a compressed tarball.
- `helm install <tarball>`: Install a chart directly from a tarball.
- `helm get <resource> <release-name>`: Get information about a specific resource in a release.
- `helm repo add <repository-name> <repository-url>`: Add a new Helm repository.
- `helm repo update`: Update the local cache of Helm repositories.

### Chart Configuration

- `helm show chart <chart-name>`: Show the chart details and metadata.
- `helm show values <chart-name>`: Show the default values of a chart.
- `helm get values <release-name>`: Get the overridden values of a release.
- `helm install --set <key=value>`: Override values during installation.
- `helm upgrade --set <key=value>`: Override values during upgrade.
- `helm upgrade --reuse-values`: Reuse the previous release's values during upgrade.
- `helm install --values <values-file>`: Specify custom values file during installation.
- `helm upgrade --values <values-file>`: Specify custom values file during upgrade.
- `helm install --set-file <key=file>`: Specify values from a file during installation.
- `helm upgrade --set-file <key=file>`: Specify values from a file during upgrade.
- `helm install --set-string <key=value>`: Override string values during installation.
- `helm upgrade --set-string <key=value>`: Override string values during upgrade.
- `helm install --set-file <key=file>`: Override values from a YAML file during installation.
- `helm upgrade --set-file <key=file>`: Override values from a YAML file during upgrade.
- `helm install --set-json <key=value>`: Override values using JSON syntax during installation.
- `helm upgrade --set-json <key=value>`: Override values using JSON syntax during upgrade.

### Working with Repositories

- `helm repo list`: List all added Helm repositories.
- `helm repo update`: Update the local cache of Helm repositories.
- `helm repo remove <repository-name>`: Remove a Helm repository from the local configuration.
- `helm search <chart-name>`: Search for charts in the added repositories.
- `helm search repo <keyword>`: Search for charts in the added repositories based on a keyword.
- `helm pull <repository-name>/<chart-name>`: Download a chart from a repository without installing it.
- `helm repo index <chart-directory>`: Generate an index file for a local chart repository.

### Hooks and Lifecycle Management

- `helm test <release-name>`: Run tests defined in a chart.
- `helm plugin install <plugin-name>`: Install a Helm plugin.
- `helm plugin uninstall <plugin-name>`: Uninstall a Helm plugin.

### Helm Security

- `helm repo add <repository-name> <repository-url> --username <username> --password <password>`: Add a Helm repository with authentication credentials.
- `helm repo update --username <username> --password <password>`: Update the local cache of Helm repositories with authentication credentials.

# Chart Folder Structure

```
wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  requirements.yaml   # OPTIONAL: A YAML file listing dependencies for the chart
  values.yaml         # The default configuration values for this chart
  charts/             # A directory containing any charts upon which this chart depends.
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes
```
# Inportant Options

#### Helm work in background when you install chart
- Load the charts and its dependancy
- Parse/analyse/take the values.yaml
- Generate the yaml
- Parse the YAML to kube objects and validate
- Generate YAML and send to Kube 

#### --dry-run
- It wil load the chart but not send to kubernetes cluster
- and will get yaml format template the will apply

# Interview Questions

## What is Kubernetes Helm, and how does it simplify application deployment and management in Kubernetes clusters?

- Kubernetes Helm is a package manager for Kubernetes applications. 
- It simplifies application deployment and management by providing a templating system for defining, installing, and upgrading complex applications and their dependencies.

## Explain the key components of a Helm chart and their respective roles in application deployment.

- A Helm chart consists of the following components:
- `Chart.yaml`: Metadata about the chart.
-  `values.yaml`: Default configuration values.
-  `templates/`: Directory containing Kubernetes manifests with Helm templating.
-  `values/`: Directory for custom configuration values.
-  `charts/`: Directory for dependencies (sub-charts).

## How do you create a Helm chart, and what is the structure of a basic Helm chart directory?

- You can create a Helm chart using the `helm create` command. 
- The basic directory structure includes the `Chart.yaml`, `values.yaml`, `templates/`, and optionally the `values/` and `charts/` directories.

## What is the purpose of Helm’s templating engine, and how does it enable customization of Kubernetes manifests for different environments?

- Helm’s templating engine allows you to customize Kubernetes manifests by inserting variables and logic into them. 
- This enables you to define templates once and apply different configurations for development, staging, and production environments.

# Helm Commands and Operations:

## Explain the difference between `helm install`, `helm upgrade`, and `helm rollback` commands in Helm, and when would you use each of them?

- `helm install` is used to initially deploy a chart.
— `helm upgrade` is used to update an existing deployment with new chart versions or configuration changes.
— `helm rollback` is used to revert to a previous release in case of issues or failures.

## How can you list all installed Helm releases in a Kubernetes cluster, and what information is displayed for each release?

- You can list all installed Helm releases using the `helm list` or `helm ls` command. 
- The information displayed includes the release name, chart name, chart version, status, and more.

## Explain the purpose of Helm release management, including how to delete a Helm release and associated resources safely.

- Helm release management involves creating, updating, and deleting releases. 
- To delete a Helm release and associated resources, you can use the `helm uninstall` command, which cleans up the release and its dependencies.

# Chart Repository and Distribution:

## What is a Helm chart repository, and how does it facilitate the distribution and sharing of Helm charts?

- A Helm chart repository is a centralized location where Helm charts are stored and made available for distribution. 
- It facilitates the sharing of charts across teams and organizations.

## How can you add a custom Helm chart repository and install charts from it?

- You can add a custom Helm chart repository using the `helm repo add` command, specifying the repository name and URL. 
- Once added, you can install charts from the repository using `helm install`.

## Explain the process of packaging a Helm chart and creating a Helm chart archive for distribution.

- To package a Helm chart, use the `helm package` command. 
- This creates a Helm chart archive (`.tgz` file) containing all the necessary chart files and dependencies. 
- The archive can be distributed to others or added to a chart repository.

# Helm Best Practices:

## What are some best practices for versioning Helm charts, and how does semantic versioning (SemVer) play a role in Helm chart versioning?

- Best practices include following semantic versioning (SemVer) for chart versions, using clear release notes, and maintaining backward compatibility when making chart updates.

## Explain Helm’s “values.yaml” files and how they can be used to customize chart configurations. What is the role of “values.yaml” in Helm charts?

- “values.yaml” file contain default configuration values for Helm charts. 
- Users can override these values to customize chart configurations during installation or upgrade. 
- “values.yaml” is the primary way to customize Helm charts for different environments.

## What is the Helm “dependency” mechanism, and when would you use it in your Helm charts?

- The Helm “dependency” mechanism allows you to specify and manage chart dependencies in a Helm chart. 
- It’s useful when your chart relies on other charts or components that need to be installed alongside it.

# Helm Chart Customization:

## Explain the difference between Helm values passed via the command line (` — set`) and values provided through a separate YAML file (`-f`). When would you use one approach over the other for customizing Helm releases?

- Values passed via ` — set` are used to override individual Helm values, while values in a separate YAML file (`-f`) provide a structured way to customize multiple values. 
- Use ` — set` for one-off overrides and `-f` for managing comprehensive configurations.

## How can you define default values for Helm chart configurations, and what is the significance of the `values.yaml` file in this context?

- Default values for Helm chart configurations are defined in the `values.yaml` file. 
- This file serves as the template for configuration values and provides a structured way to specify defaults for chart values.

# Chart Dependencies:

## Explain Helm’s “requirements.yaml” file and how it is used to declare chart dependencies. What are the benefits of managing dependencies in a Helm chart?

- The “requirements.yaml” file is used to declare chart dependencies. 
- It specifies which charts are required for the current chart to function correctly. 
- Managing dependencies in a Helm chart simplifies the process of deploying complex applications with multiple components.

## How can you update and fetch chart dependencies defined in the “requirements.yaml” file? What command(s) would you use?

- To update and fetch chart dependencies, you can use the `helm dependency update` command. 
- This command retrieves the latest versions of chart dependencies specified in the “requirements.yaml” file and updates the “charts/” directory.

# Chart Versioning and Release Management:

## Explain how Helm handles chart versioning and upgrades. What steps are involved in upgrading a Helm release to a new chart version, and how does Helm ensure compatibility?

- Helm handles chart versioning by associating versions with charts and releases. 
- When upgrading a Helm release to a new chart version, Helm performs a diff of the old and new charts, ensuring that the upgrade process is compatible with existing release data.

## What is Helm’s release rollback feature, and when would you use it? How does Helm manage the state of releases during a rollback?

- Helm’s release rollback feature allows you to revert to a previous release version in case of issues.
- Helm manages the state of releases by storing a release’s history, including its configuration and versions. 
- During a rollback, Helm reverts to the specified release version.

# Chart Repository and Distribution:

## Explain how you can create and host a custom Helm chart repository. What steps are involved in making Helm charts available to your team or organization internally?

- To create a custom Helm chart repository, you need to package your Helm charts and host them in a web-accessible location, such as an HTTP server or cloud storage. You can use tools like ChartMuseum or GitHub Pages to set up a repository.

## What is the purpose of the “index.yaml” file in a Helm chart repository, and how is it generated and updated?

- The “index.yaml” file serves as the index of the Helm chart repository, listing available charts and their versions. 
- It is generated and updated using the `helm repo index` command after adding or updating charts in the repository.

# Helm Security and Best Practices:

## What security considerations should you take into account when using Helm to deploy applications in a Kubernetes cluster? How can you mitigate potential security risks?

- Security considerations include controlling access to the Helm server, validating chart sources, and ensuring that Helm charts are signed and verified. 
- Mitigations involve following security best practices and using tools like Helm Provenance and signing charts with GPG.

## What are some best practices for managing Helm releases and charts in a production Kubernetes environment?

- Best practices include using Helm chart versioning, maintaining clear release notes, implementing CI/CD pipelines for Helm releases, and following a structured directory layout for Helm charts. 
- Additionally, ensure that sensitive values are properly encrypted and secured.



https://helm.sh/docs/intro/cheatsheet/

helm create projevct1

