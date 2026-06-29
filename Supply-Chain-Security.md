## OpenSSF Scorecards

This section describes how OpenSSF Scorecards are implemented.

Scorecards provide an automated assessment of repository security, including checks such as:
- Use of branch protection rules and repository rules
- Dependency update practices
- Code review enforcement
- Security policy presence

These results help maintainers track improvements and identify potential gaps in supply chain security.

### Implementation and triggers

Scorecards are implemented using CI/CD workflow in major Wren Security repositories. Here is [example implementation](https://github.com/WrenSecurity/wrensec-commons/blob/main/.github/workflows/scorecard.yml).

Scorecards run automatically:
- On **push** to the `main` branch.
- On a **weekly schedule** for continuous monitoring.
- On **branch protection rule**, when branch protection rules are changed.

### Developer visibility

Each repository publishes its Scorecards report to a public dashboard:
- reports can be found at https://securityscorecards.dev/viewer/?uri=github.com/WrenSecurity/<*repository name*> or searched at https://securityscorecards.dev/viewer/
- example of scorecard report: [wrensec-commons Scorecard](https://securityscorecards.dev/viewer/?uri=github.com/WrenSecurity/wrensec-commons)

## SonarQube / SonarCloud integration

This section provides a technical description of how SonarQube analysis is implemented across repositories, how developers interact with it,
and the steps required to enable it for new repositories.
SonarQube provides **static code analysis** to identify bugs, security vulnerabilities, code duplication, and insufficient test coverage.  
Reports are available on SonarCloud, which enables developers to monitor code quality during pull requests and helps monitor and maintain security across repositories and over time.

###  Implementation and triggers

SonarQube is implemented using CI/CD-based analysis. Repositories call reusable workflows located in [`.github/.github/workflows`](https://github.com/wrensecurity/.github/tree/main/.github/workflows).
**Reference implementation:**  
The [wrensec-commons](https://github.com/WrenSecurity/wrensec-commons) repository demonstrates the standard setup with these workflows:
- `build-project.yml`
- `sonar-trigger.yml`

Analyses are triggered by:
- Opening a new pull request
- Force-pushing to an existing pull request
- Merging a pull request into the `main` branch

### Enabling Sonar for a new repository

1. **Create a project in SonarCloud** for the repository.
2. **Obtain required credentials:**
    - **Sonar Token** – used in the CI/CD pipeline for authentication and sending analysis results.
    - **Project Key** – unique identifier of the repository in SonarCloud.
3. **Configure GitHub Actions:**
    - Add workflow YAML files that reference the reusable workflows.
    - Provide the correct project key in configuration.
    - Store the Sonar token in the repository’s **GitHub Secrets**.
4. Once configured, every pull request and every push to the `main` branch will trigger a SonarCloud analysis.

### Developer visibility

#### Pull request comments

When a pull request is submitted, SonarCloud analysis runs automatically.
After successful analysis, developers receive a **SonarCloud bot comment** directly on the pull request.
The comment contains metrics relevant to the changes in that pull request, including:
- Code coverage of new tests
- Code duplication rate
- Potential security vulnerabilities

The comment also provides a link to the **full SonarCloud report** for that pull request.

#### Analysis results in SonarCloud

All project analyses are publicly available at:  
[SonarCloud – Wren Security Projects](https://sonarcloud.io/organizations/wrensecurity/projects?sort=name).


## CodeQL analysis

This section describes the CodeQL configuration used across repositories.
CodeQL detects potential security vulnerabilities (e.g., insecure API usage, injection risks, unsafe coding patterns).  
Findings are primarily used by the security team for ongoing monitoring and improvement.

### Implementation overview

- **Integration:** Default GitHub CodeQL setup.
- **Scope:** Enabled on all repositories in the organization.

### Schedule and triggers

CodeQL runs automatically:
- On **push** and **pull requests** to `main` and other protected branches.
- On a **weekly schedule**.

### Developer visibility

- Results are collected under each repository’s **Security > Code scanning alerts**.
- Access to CodeQL alerts is limited to selected organization members.
- Developers contributing code do not need to configure anything; the analysis runs automatically.

## Dependabot

### Implementation Overview

An example configuration can be found in the [WrenSecurity .github repository](https://github.com/WrenSecurity/.github/blob/main/.github/dependabot.yml).

The configuration is scheduled to run once a month. It is set up to check only for major version updates of the GitHub Actions within the `.github/workflows` directory. When updates are available, Dependabot automatically generates a pull request with the proposed changes.

### Version Notation

For enhanced security, all GitHub Actions are pinned to a specific commit SHA. The semantic version number is maintained as an inline comment for clarity. This notation is accepted and followed by Dependabot.

The format for this notation is as follows:

```yaml

uses: actions/checkout@de0fac2e4500dabe0009e67214ff5f5447ce83dd # v6.0.2

```

### Manual Updates

GitHub Actions can still be updated manually, which is particularly important for immediately patching compromised versions or addressing urgent security advisories. When performing a manual update, the above-described notation must be followed.

### Security Context

Pinning actions to a specific commit SHA and enforcing regular, automated updates are critical steps toward maintaining a secure and controlled CI/CD pipeline. Combined with CodeQL and Sonar analysis, this approach actively minimizes the risk of supply-chain attacks.