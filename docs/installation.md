# Installation Guide

## Overview

This document describes the deployment of SonarQube and its PostgreSQL database on an Ubuntu 24.04 LTS AWS EC2 instance.

The deployment provides a centralized platform for performing static code analysis and evaluating software quality.

## Prerequisites

- AWS account
- Ubuntu 24.04 LTS EC2 instance
- SSH access to the EC2 instance
- Security Group configured for required access
- Java 17
- PostgreSQL
- SonarQube

## AWS EC2 Setup

An Ubuntu 24.04 LTS EC2 instance was created on AWS and used as the server for the SonarQube deployment.

The instance was accessed through SSH and prepared for the installation of the required software.

## Java Installation

SonarQube requires a compatible Java runtime environment.

Java 17 was installed and configured on the Ubuntu server.

The Java installation was verified before proceeding with the SonarQube deployment.

## PostgreSQL Installation

PostgreSQL was installed to provide the database backend required by SonarQube.

A dedicated PostgreSQL database and user were created for SonarQube.

The database configuration included:

- SonarQube database
- Dedicated database user
- Database permissions
- PostgreSQL schema access

## SonarQube Installation

SonarQube was installed on the EC2 instance and configured to use PostgreSQL as its database backend.

The installation included:

- Downloading and extracting SonarQube
- Creating the SonarQube system user
- Configuring SonarQube
- Connecting SonarQube to PostgreSQL
- Creating a systemd service
- Starting the SonarQube service

## Service Configuration

SonarQube was configured as a systemd service so that it could be managed using standard Linux service commands.

The service was configured to start automatically with the server.

## Verification

After installation, the deployment was verified by checking:

- Java installation
- PostgreSQL availability
- SonarQube database connectivity
- SonarQube service status
- SonarQube web server availability
- SonarQube web interface

## Result

SonarQube was successfully deployed on the AWS EC2 instance and configured with PostgreSQL as its persistent database backend.

The resulting environment provided a working platform for static code analysis and code quality management.
