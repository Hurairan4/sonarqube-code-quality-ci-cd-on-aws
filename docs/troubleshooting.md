# Troubleshooting Guide

## Overview

During the deployment and configuration of SonarQube on AWS EC2, several issues were encountered involving the SonarQube service, PostgreSQL connectivity, and the SonarQube web server.

This document records the main troubleshooting steps used during the project.

---

## Issue 1: SonarQube Service Not Starting Correctly

### Symptoms

The SonarQube systemd service appeared to start but later stopped.

The service status showed that the main SonarQube process was no longer running.

### Investigation

The service status was checked using:

```bash
sudo systemctl status sonarqube --no-pager
```

SonarQube logs were also inspected to determine which internal process was stopping.

### Resolution

The SonarQube service and its internal processes were checked and restarted.

The service configuration was also reviewed to ensure that the systemd unit file correctly matched the SonarQube installation.

---

## Issue 2: SonarQube Web Server Not Accessible

### Symptoms

SonarQube was running, but the web interface was not immediately accessible through the browser.

### Investigation

The server was checked to determine whether SonarQube was listening on port `9000`.

```bash
sudo ss -tlnp | grep 9000
```

SonarQube logs were also reviewed to determine whether the Web Server process had started successfully.

### Resolution

The SonarQube service was restarted and its logs were monitored until the Web Server process successfully started and listened on port `9000`.

---

## Issue 3: PostgreSQL Database Configuration

### Symptoms

SonarQube required a properly configured PostgreSQL database before it could operate correctly.

### Investigation

The PostgreSQL database and dedicated user were verified.

The SonarQube database configuration was checked in:

```text
/opt/sonarqube/conf/sonar.properties
```

### Resolution

A dedicated PostgreSQL database and user were configured for SonarQube.

The required permissions were granted to the SonarQube database user, including access to the PostgreSQL `public` schema.

---

## Issue 4: SonarQube Database Connectivity

### Symptoms

SonarQube could not operate correctly when the database configuration was incomplete or incorrect.

### Investigation

The following configuration values were reviewed:

```properties
sonar.jdbc.url=jdbc:postgresql://localhost/sonarqubee
sonar.jdbc.username=sonarr_user
```

The PostgreSQL JDBC driver was also verified as part of the SonarQube installation.

### Resolution

The PostgreSQL connection settings were corrected and SonarQube was restarted.

Database-related SonarQube logs were reviewed to confirm successful startup.

---

## Issue 5: SonarQube Internal Processes Stopping

### Symptoms

SonarQube logs showed internal processes starting and then stopping.

Examples included the Elasticsearch process and Web Server process stopping during startup.

### Investigation

SonarQube logs were reviewed to identify which process was exiting.

The service status and process state were also checked using systemd and Linux networking commands.

### Resolution

The SonarQube service was stopped and restarted while monitoring the logs.

The server configuration and available resources were also reviewed because SonarQube requires sufficient system resources for its internal processes.

---

## Issue 6: systemd Unit File Changes

### Symptoms

After modifying the SonarQube systemd service configuration, systemd reported that the unit file had changed on disk.

### Resolution

The systemd configuration was reloaded before restarting SonarQube:

```bash
sudo systemctl daemon-reload
```

The SonarQube service was then restarted and its status was verified.

---

## Useful Diagnostic Commands

### Check SonarQube Service

```bash
sudo systemctl status sonarqube --no-pager
```

### Start SonarQube

```bash
sudo systemctl start sonarqube
```

### Restart SonarQube

```bash
sudo systemctl restart sonarqube
```

### Stop SonarQube

```bash
sudo systemctl stop sonarqube
```

### Reload systemd

```bash
sudo systemctl daemon-reload
```

### Check Port 9000

```bash
sudo ss -tlnp | grep 9000
```

### Check PostgreSQL

```bash
sudo systemctl status postgresql
```

---

## Log Investigation

SonarQube logs were an important part of troubleshooting the deployment.

The main SonarQube log files include:

```text
/opt/sonarqube/logs/sonar.log
/opt/sonarqube/logs/web.log
/opt/sonarqube/logs/es.log
```

These logs can be used to investigate:

- Startup failures
- Database connection problems
- Web Server issues
- Elasticsearch problems
- Configuration errors

---

## Lessons Learned

The troubleshooting process provided practical experience with:

- Linux systemd service management
- PostgreSQL configuration
- SonarQube administration
- Application log analysis
- Network port verification
- Database connectivity troubleshooting
- AWS EC2 resource management

---

## Conclusion

Troubleshooting the SonarQube deployment demonstrated the importance of checking application logs, systemd service status, database configuration, and network ports when diagnosing DevOps infrastructure problems.

The experience provided practical understanding of how multiple services must work together for a successful SonarQube deployment.
