# Lock and Key Application – Infrastructure

## Overview

This repository contains the Infrastructure as Code (IaC) implementation for the **Lock and Key application**.

The infrastructure is designed using an **environment-specific approach**, allowing each environment to have its own configuration, resources, and deployment lifecycle while maintaining reusable and standardized infrastructure components.

The infrastructure is provisioned and managed using **Terraform** and can be deployed through the CI/CD pipeline.

---

## Environments

The infrastructure is separated based on application environments:

- **Development (`dev`)** – Used for development and initial testing.
- **Pre-Production (`preprod`)** – Used for integration, validation, and pre-production testing.
- **Production (`prod`)** – Used for production workloads.

Each environment maintains its own Terraform configuration and variables.

### Environment Isolation

Each environment is independently managed to provide:

- Environment-specific resource configuration
- Independent Terraform state
- Environment-specific variables
- Controlled deployment
- Reduced risk of changes affecting other environments

---

## Repository Structure

```text
.
├── environment/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   ├── outputs.tf
│   │   ├── provider.tf
│   │   └── backend.tf
│   │
│   ├── preprod/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── terraform.tfvars
│   │   ├── outputs.tf
│   │   ├── provider.tf
│   │   └── backend.tf
│   │
│   └── prod/
│       ├── main.tf
│       ├── variables.tf
│       ├── terraform.tfvars
│       ├── outputs.tf
│       ├── provider.tf
│       └── backend.tf
│
├── modules/
│   ├── networking/
│   ├── compute/
│   ├── storage/
│   ├── security/
│   └── ...
│
├── .gitignore
├── README.md
└── ...
```

> The actual module names may vary depending on the resources used by the Lock and Key application.

---

## Infrastructure Design

The infrastructure follows a modular and environment-specific design.

```text
                    Lock and Key Infrastructure
                              |
              +---------------+---------------+
              |               |               |
             DEV           PRE-PROD          PROD
              |               |               |
        Terraform        Terraform        Terraform
              |               |               |
        Azure Resources Azure Resources Azure Resources
```

Reusable Terraform modules are maintained separately from environment configurations.

```text
                    Terraform Modules
                           |
          +----------------+----------------+
          |                |                |
       Network          Security         Compute
          |                |                |
          +----------------+----------------+
                           |
                  Environment
