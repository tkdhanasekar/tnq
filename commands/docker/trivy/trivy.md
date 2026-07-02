install **Trivy** and scanning container images.

### Ubuntu/Debian

Follow the official installation instructions:

[Trivy Installation Guide](https://trivy.dev/latest/getting-started/installation/?utm_source=chatgpt.com)

Or install using the official repository:

```bash
sudo apt-get update
sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb \
$(lsb_release -sc) main" | \
sudo tee /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy
```

Verify:

```bash
trivy --version
```

---

## Step 2: Install Docker

Trivy scans container images stored locally or in remote registries. Ensure you have Docker installed and running.

Verify:

```bash
docker --version
docker images
```

---

## Step 3: Pull an image

Example:

```bash
docker pull nginx:latest
```

List images:

```bash
docker images
```

Example output:

```text
REPOSITORY   TAG      IMAGE ID
nginx        latest   abc123...
```

---

## Step 4: Scan an image

Basic scan:

```bash
trivy image nginx:latest
```

On the first run, Trivy downloads its vulnerability database. This may take a minute or two.

Example output:

```text
nginx:latest

Total: 25

CRITICAL: 1
HIGH: 8
MEDIUM: 10
LOW: 6
```

---

## Step 5: Scan a remote image

You don't need to pull the image first.

```bash
trivy image python:3.12
```

or

```bash
trivy image ubuntu:22.04
```

---

## Step 6: Scan only HIGH and CRITICAL vulnerabilities

```bash
trivy image --severity HIGH,CRITICAL nginx:latest
```

---

## Step 7: Ignore vulnerabilities without fixes

```bash
trivy image --ignore-unfixed nginx:latest
```

---

## Step 8: Save results to a file

JSON:

```bash
trivy image -f json -o report.json nginx:latest
```

Table:

```bash
trivy image -f table -o report.txt nginx:latest
```

SARIF:

```bash
trivy image -f sarif -o report.sarif nginx:latest
```

---

## Step 9: Fail a CI/CD pipeline if vulnerabilities are found

Exit with a non-zero status if HIGH or CRITICAL vulnerabilities exist:

```bash
trivy image \
  --severity HIGH,CRITICAL \
  --exit-code 1 \
  nginx:latest
```

---

## Step 10: Understand the report

A typical finding includes:

```text
Package          openssl
Installed        3.0.2
Fixed Version    3.0.12
Severity         HIGH
Vulnerability    CVE-XXXX-YYYY
```

Key fields:

* **Package**: The affected software package.
* **Installed**: Version currently in the image.
* **Fixed Version**: Version that resolves the vulnerability.
* **Severity**: LOW, MEDIUM, HIGH, or CRITICAL.
* **Vulnerability**: The associated CVE identifier.

---

## Example workflow

```bash
# Pull an image
docker pull nginx:latest

# Scan it
trivy image nginx:latest

# Scan only HIGH and CRITICAL issues
trivy image --severity HIGH,CRITICAL nginx:latest

# Save results as JSON
trivy image -f json -o report.json nginx:latest
```

**Trivy CLI commands** available in current releases. Some commands are marked experimental or may depend on the Trivy version you're using. ([Trivy][1])

| Command                     | Purpose                                                                     | Example                                    |
| --------------------------- | --------------------------------------------------------------------------- | ------------------------------------------ |
| `trivy image`               | Scan container images                                                       | `trivy image nginx:latest`                 |
| `trivy fs` (`filesystem`)   | Scan a local filesystem                                                     | `trivy fs .`                               |
| `trivy repo` (`repository`) | Scan a Git repository                                                       | `trivy repo https://github.com/org/repo`   |
| `trivy config`              | Scan Infrastructure as Code (IaC) files                                     | `trivy config .`                           |
| `trivy rootfs`              | Scan a mounted Linux root filesystem                                        | `trivy rootfs /mnt/rootfs`                 |
| `trivy sbom`                | Scan an SBOM for vulnerabilities and licenses                               | `trivy sbom sbom.json`                     |
| `trivy kubernetes` (`k8s`)  | Scan Kubernetes resources or clusters                                       | `trivy kubernetes cluster`                 |
| `trivy vm`                  | Scan virtual machine images *(experimental)*                                | `trivy vm disk.vmdk`                       |
| `trivy server`              | Run Trivy in server mode                                                    | `trivy server`                             |
| `trivy clean`               | Remove caches and vulnerability databases                                   | `trivy clean --all`                        |
| `trivy convert`             | Convert JSON reports to other formats                                       | `trivy convert --format table report.json` |
| `trivy plugin`              | Install and manage plugins                                                  | `trivy plugin install <plugin>`            |
| `trivy module`              | Manage Trivy modules                                                        | `trivy module list`                        |
| `trivy registry`            | Manage registry authentication                                              | `trivy registry login`                     |
| `trivy version`             | Display the installed version                                               | `trivy version`                            |
| `trivy completion`          | Generate shell completion scripts                                           | `trivy completion bash`                    |
| `trivy help`                | Show help information                                                       | `trivy help image`                         |
| `trivy vex`                 | Work with Vulnerability Exploitability eXchange (VEX) data *(experimental)* | `trivy vex`                                |
| `trivy cloud`               | Configure Trivy Cloud integration (newer versions)                          | `trivy cloud`                              |
| `trivy login`               | Log in to Trivy Cloud                                                       | `trivy login`                              |
| `trivy logout`              | Log out of Trivy Cloud                                                      | `trivy logout`                             |

### Common options for scanning

These flags work with many scan commands:

```bash
--severity HIGH,CRITICAL
--ignore-unfixed
--format table
--format json
--format sarif
--output report.json
--exit-code 1
--scanners vuln
--scanners vuln,secret,misconfig
--timeout 10m
--quiet
--debug
```

### Frequently used commands

```bash
# Scan a Docker image
trivy image nginx:latest

# Scan current directory
trivy fs .

# Scan Kubernetes manifests
trivy config .

# Scan a Git repository
trivy repo https://github.com/aquasecurity/trivy

# Scan a root filesystem
trivy rootfs /

# Scan an SBOM
trivy sbom sbom.json

# Remove cache
trivy clean --all

# Check version
trivy version
```

### Get help for any command

```bash
trivy --help
trivy image --help
trivy fs --help
trivy config --help
trivy kubernetes --help
```

**Trivy examples** 

---

# 1. Scan a Docker image

```bash
trivy image nginx:latest
```

Scan an Ubuntu image:

```bash
trivy image ubuntu:22.04
```

Scan a Python image:

```bash
trivy image python:3.12
```

---

# 2. Scan an image from Docker Hub

```bash
trivy image node:20
```

---

# 3. Scan an image by image ID

```bash
docker images

trivy image <IMAGE_ID>
```

Example:

```bash
trivy image a8c1e8d5c123
```

---

# 4. Show only HIGH and CRITICAL vulnerabilities

```bash
trivy image --severity HIGH,CRITICAL nginx
```

---

# 5. Ignore vulnerabilities without fixes

```bash
trivy image --ignore-unfixed nginx
```

---

# 6. Exit with error if vulnerabilities exist

Useful in CI/CD.

```bash
trivy image --exit-code 1 nginx
```

Only HIGH and CRITICAL:

```bash
trivy image \
--severity HIGH,CRITICAL \
--exit-code 1 \
nginx
```

---

# 7. Save report as JSON

```bash
trivy image -f json -o report.json nginx
```

---

# 8. Save report as Table

```bash
trivy image -f table -o report.txt nginx
```

---

# 9. Save report as SARIF

```bash
trivy image -f sarif -o report.sarif nginx
```

---

# 10. Save report as HTML (using a template)

```bash
trivy image \
--format template \
--template "@contrib/html.tpl" \
-o report.html \
nginx
```

---

# 11. Scan local filesystem

Current directory:

```bash
trivy fs .
```

Specific folder:

```bash
trivy fs /home/user/project
```

---

# 12. Scan only secrets

```bash
trivy fs \
--scanners secret \
.
```

---

# 13. Scan only vulnerabilities

```bash
trivy fs \
--scanners vuln \
.
```

---

# 14. Scan only misconfigurations

```bash
trivy config .
```

---

# 15. Scan Dockerfile

```bash
trivy config Dockerfile
```

---

# 16. Scan Kubernetes YAML

```bash
trivy config deployment.yaml
```

---

# 17. Scan multiple YAML files

```bash
trivy config manifests/
```

---

# 18. Scan a Git repository

Remote repository:

```bash
trivy repo https://github.com/aquasecurity/trivy
```

---

# 19. Scan a local Git project

```bash
trivy fs .
```

---

# 20. Scan Kubernetes cluster

```bash
trivy kubernetes cluster
```

---

# 21. Scan a namespace

```bash
trivy kubernetes namespace default
```

---

# 22. Scan SBOM

```bash
trivy sbom sbom.json
```

---

# 23. Generate CycloneDX SBOM

```bash
trivy image \
--format cyclonedx \
-o sbom.json \
nginx
```

---

# 24. Generate SPDX SBOM

```bash
trivy image \
--format spdx-json \
-o spdx.json \
nginx
```

---

# 25. Scan root filesystem

```bash
trivy rootfs /
```

---

# 26. Scan with timeout

```bash
trivy image \
--timeout 10m \
ubuntu
```

---

# 27. Skip database update

```bash
trivy image \
--skip-db-update \
nginx
```

---

# 28. Update vulnerability database

```bash
trivy image --download-db-only
```

---

# 29. Clear cache

```bash
trivy clean --all
```

---

# 30. Show version

```bash
trivy version
```

---

# 31. Show help

```bash
trivy --help
```

Specific help:

```bash
trivy image --help
```

---

# 32. Scan a private image (after Docker login)

```bash
docker login

trivy image mycompany/app:v1
```

---

# 33. Scan an image tar archive

```bash
docker save nginx -o nginx.tar

trivy image --input nginx.tar
```

---

# 34. Quiet mode

```bash
trivy image --quiet nginx
```

---

# 35. Debug mode

```bash
trivy image --debug nginx
```

---

# 36. Scan with multiple scanners

```bash
trivy fs \
--scanners vuln,secret,misconfig \
.
```

---

# 37. Ignore a vulnerability

Create `.trivyignore`:

```text
CVE-2024-12345
CVE-2023-98765
```

Run:

```bash
trivy image nginx
```

---

# 38. Scan only OS packages

```bash
trivy image \
--pkg-types os \
nginx
```

---

# 39. Scan only application dependencies

```bash
trivy image \
--pkg-types library \
python:3.12
```

---

# 40. Complete CI/CD example

```bash
trivy image \
--severity HIGH,CRITICAL \
--ignore-unfixed \
--exit-code 1 \
--format json \
-o report.json \
myapp:latest
```

## Common options reference

| Option             | Purpose                                                        |
| ------------------ | -------------------------------------------------------------- |
| `--severity`       | Filter by severity (e.g., `LOW`, `MEDIUM`, `HIGH`, `CRITICAL`) |
| `--ignore-unfixed` | Skip vulnerabilities with no available fix                     |
| `--exit-code`      | Return a specified exit code when findings are present         |
| `--format`         | Choose output format (`table`, `json`, `sarif`, etc.)          |
| `--output` (`-o`)  | Save output to a file                                          |
| `--scanners`       | Select scanners (`vuln`, `secret`, `misconfig`, `license`)     |
| `--timeout`        | Set a scan timeout                                             |
| `--debug`          | Enable debug logging                                           |
| `--quiet`          | Suppress progress and non-essential output                     |

