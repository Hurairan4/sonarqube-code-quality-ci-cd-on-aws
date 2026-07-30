# Configuration Guide

## Overview

This document describes the configuration of SonarQube, PostgreSQL, and the supporting Linux services used in the project.

The configuration connects SonarQube to PostgreSQL and prepares the environment for static code analysis.

---

## PostgreSQL Configuration

PostgreSQL was configured as the database backend for SonarQube.

A dedicated database and user were created for the SonarQube installation.

The database configuration included:

- Dedicated SonarQube database
- Dedicated PostgreSQL user
- Database permissions
- Schema permissions
- PostgreSQL JDBC connectivity

The SonarQube database connection was configured using the PostgreSQL JDBC URL.

---

## SonarQube Configuration

SonarQube was configured through its main configuration file:

```text
/opt/sonarqube/conf/sonar.properties
```

The configuration connects SonarQube to PostgreSQL.

The important database settings include:

```properties
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqubee
sonar.jdbc.username=sonarr_user
```

The database password was configured on the server and is **not included in this repository**.

> **Security note:** Never commit database passwords, API tokens, SSH keys, or other credentials to a public GitHub repository.

---

## Java Configuration

SonarQube was configured to use Java 17.

The Java runtime used by the installation was:

```text
/usr/lib/jvm/java-17-openjdk-amd64/bin/java
```

Java compatibility was verified as part of the SonarQube deployment.

---

## SonarQube Service Configuration

SonarQube was configured as a Linux systemd service.

This allows the application to be managed using standard systemd commands.

Examples:

```bash
sudo systemctl start sonarqube
sudo systemctl stop sonarqube
sudo systemctl restart sonarqube
sudo systemctl status sonarqube
```

The service was also configured to start automatically when the EC2 instance boots.

---

## SonarQube Web Interface

SonarQube uses port:

```text
9000
```

The web server was configured to listen on the EC2 instance so that the SonarQube interface could be accessed through a web browser.

AWS Security Group rules were configured to provide the required network access.

---

## SonarQube and PostgreSQL Workflow

The relationship between the components is:

```text
Source Code
     │
     ▼
SonarQube
     │
     ▼
PostgreSQL
     │
     ▼
Analysis Results
     │
     ▼
SonarQube Web Interface
```

SonarQube performs the analysis while PostgreSQL provides persistent storage for the SonarQube application data.

---

## Code Quality Analysis

SonarQube analyzes source code and provides information about several quality and security categories, including:

- Bugs
- Vulnerabilities
- Code Smells
- Security-related issues
- Maintainability
- Reliability
- Overall code quality

The analysis results can be reviewed through the SonarQube web interface.

---

## Quality Gates

Quality Gates provide an automated way to evaluate whether analyzed code meets defined quality requirements.

A Quality Gate can evaluate conditions related to:

- Reliability
- Security
- Maintainability
- Coverage
- Duplicated code

This allows code quality to become part of the development and CI/CD workflow rather than being checked manually.

---

## GitHub Actions Integration

The project also uses GitHub Actions as part of the CI/CD workflow.

The intended workflow is:

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ▼
SonarQube Analysis
    │
    ▼
Quality Gate
    │
    ▼
Analysis Result
```

This approach allows code quality analysis to be incorporated into the software development lifecycle.

---

## Security Considerations

The following information should never be committed to the public repository:

- PostgreSQL passwords
- SonarQube authentication tokens
- GitHub tokens
- AWS access keys
- SSH private keys
- Gmail or SMTP credentials

Configuration examples in this repository should use placeholders instead of real credentials.

---

## Configuration Validation

After configuration, the following checks were performed:

- PostgreSQL was running correctly.
- The SonarQube database was accessible.
- SonarQube was connected to PostgreSQL.
- SonarQube was running as a systemd service.
- The SonarQube web server was listening on port 9000.
- The SonarQube web interface was accessible.
- Code analysis functionality was available.

---

## Summary

The completed configuration provides a SonarQube environment running on AWS EC2 with PostgreSQL as its database backend and GitHub Actions available for CI/CD integration.

This setup demonstrates how static code analysis and Quality Gates can be incorporated into a DevOps workflow.
