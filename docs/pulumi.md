# IBM Cloud and Pulumi

[Pulumi](https://www.pulumi.com/docs/iac/get-started/) is an open-source Infrastructure as Code (IaC) platform that lets you automate, secure, and manage cloud resources, configurations, and secrets — all using real programming languages like Python, Go, .NET, TypeScript, C# etc.

With Pulumi, you can define cloud infrastructure using familiar coding practices such as loops, functions, and classes, making your cloud automation more powerful and maintainable than traditional declarative tools.

When used with IBM Cloud, Pulumi allows you to provision and manage a wide range of IBM Cloud services — such as VPCs, Kubernetes clusters, Object Storage, and Databases — using Python or any supported language.

This enables developers to:

- Write infrastructure code in a language they already know.
- Automate IBM Cloud environments using version control and CI/CD pipelines.
- Integrate IBM Terraform modules to reuse existing templates and best practices.

## Table of Contents

- [Introduction to Pulumi with Python](#introduction)
- [Installation](#installation)
- [Key Concepts](#concepts)
- [Pulumi Configuration](#pulumi-configuration)
- [Pulumi Commands](#commands)
- [Usage](#usage)
- [Python Examples](#python-examples)
- [Best Practices](#best-practices)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
- [References](#references)

## Introduction

Pulumi is an Infrastructure as Code (IaC) platform that allows you to define cloud infrastructure using various programming languages. This tutorial focuses on using Pulumi with IBM Cloud through Python.

**Why Pulumi with Python?**

- Familiar syntax: Use Python, one of the most popular programming languages.
- Rich ecosystem: Leverage Python's extensive library ecosystem.
- Strong typing: Benefit from type hints and IDE support.
- Reusable components: Create classes and modules for infrastructure.
- Testing: Write unit tests for your infrastructure code.


## Installation

Before starting, ensure you have the following:

1. **IBM Cloud Account**
   - Sign up at [https://cloud.ibm.com](https://cloud.ibm.com).  
   - Create and download the IBMCloud API key.

2. **Installed Tools**

   | Tool | Description | Installation |
   |------|--------------|---------------|
   | Pulumi | Infrastructure as Code tool | [Install Pulumi](https://www.pulumi.com/docs/install/) |
   | Python | Runtime for your Pulumi program | [Install Python 3.8+](https://www.python.org/downloads/) |
   | IBM Cloud CLI | To manage cloud resources | [Install IBM Cloud CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started) |
   | Terraform (optional) | For using IBM Terraform modules | [Install Terraform](https://developer.hashicorp.com/terraform/downloads) |

3. **Set Environment Variables**

   ```bash
    export IBMCLOUD_API_KEY=<your_ibmcloud_api_key>
    export PULUMI_CONFIG_PASSPHRASE=<your_secret_passphrase>
   
    # Install Pulumi
    curl -fsSL https://get.pulumi.com | sh

    # Install dependencies:
    pip install pulumi pulumi_ibm

    # Verify installation
    pulumi version
    python --version

    # Configure IBM Cloud:

    ibmcloud login
    pulumi config set ibm:region us-south

    # Create a new Pulumi Project:

    mkdir pulumi-ibmcloud-demo && cd pulumi-ibmcloud-demo
    pulumi new python -y
    ```

## Concepts

**Stack** - A Stack is an isolated instance of your Pulumi program, typically representing an environment (dev, staging, prod).

```py
import pulumi

# Get current stack name
stack = pulumi.get_stack()
print(f"Current stack: {stack}")
```

**Project** - A Project is a single Pulumi program containing your infrastructure definitions.

**Configuration** - Stack-specific settings that can be changed without modifying code.

**State** - Pulumi maintains state to track current infrastructure and manage updates.


## Pulumi Configuration

Configuration Files - Configure IBM Cloud Provider in Pulumi

In `Pulumi.yaml`, add:

```yaml
name: pulumi-ibmcloud-demo
runtime: python
description: IBM Cloud infrastructure example using Python
```

In `Pulumi.dev.yaml` add the Stack-specific configuration:

```py
config:
    pulumi-ibmcloud-demo::apiKey: ${IBMCLOUD_API_KEY}
    pulumi-ibmcloud-demo:region: us-south
    pulumi-ibmcloud-demo:resource-group: default
    pulumi-ibmcloud-demo:cos-instance-name: my-dev-cos
```

The IBM Cloud provider must be installed as a Local Package. Use below command to successfully generate a Python SDK for the ibm package:

```bash
pulumi package add terraform-provider ibm-cloud/ibm
```

Setting Configuration

```bash
# Set configuration values
pulumi config set region us-south
pulumi config set resource-group default --secret
pulumi config set --path tags '["env:dev", "team:platform"]'
```

Accessing Configuration in Python

```py
import pulumi
import json

config = pulumi.Config()

# Get configuration values
region = config.require("region")
resource_group = config.get("resource-group") or "default"
tags = config.get_object("tags") or ["environment:dev"]

# Type-safe configuration with classes
class AppConfig:
    def __init__(self):
        self.region = config.require("region")
        self.resource_group = config.get("resource-group") or "default"
        self.environment = pulumi.get_stack()
        
app_config = AppConfig()
```

## Commands

```bash
# Initialize a new Pulumi project with Python
pulumi new python

# Create a new stack
pulumi stack init dev

# Install dependencies
pip install -r requirements.txt

# Preview infrastructure changes
pulumi preview

# Deploy infrastructure
pulumi up

# Destroy infrastructure
pulumi destroy

# View stack outputs
pulumi stack output

# View stack configuration
pulumi config

# Refresh state
pulumi refresh
```

## Usage

**Using Terraform IBM Modules (TIM) with Python**

While Pulumi doesn't directly use Terraform modules, you can achieve similar patterns using Pulumi components and the IBM Cloud provider.

Environment Setup

```bash
# Set IBM Cloud API key
export IBMCLOUD_API_KEY=your_actual_api_key

# Or configure via Pulumi config
pulumi config set ibm:apiKey --secret
```

Setting up IBM Cloud Provider in Python

```py
import pulumi
import pulumi_ibm as ibm

# Configure IBM Cloud provider
provider = ibm.Provider(
    "ibm-provider",
    region="us-south"
    # Credentials are automatically picked from:
    # 1. IBMCLOUD_API_KEY environment variable
    # 2. IBM Cloud CLI configuration
    # 3. Pulumi configuration
)
```

## Python Examples

To grasp the core concepts and workflow of Pulumi, here are a few foundational examples to help you get started.

<details>
<summary> Example 1: Simple Cloud Object Storage Instance </summary>
<br/>

```py
import pulumi
import pulumi_ibm as ibm

config = pulumi.Config()
region = config.require("region")
resource_group = config.get("resource-group") or "default"

# Create a Cloud Object Storage instance
cos_instance = ibm.resource.Instance(
    "my-cos-instance",
    name="my-dev-cos-instance",
    service="cloud-object-storage",
    plan="lite",
    location="global",
    resource_group_name=resource_group,
    tags=["environment:dev", "managed-by:pulumi"]
)

# Create a bucket in the COS instance
cos_bucket = ibm.cos.Bucket(
    "my-bucket",
    bucket_name="my-unique-bucket-name",
    resource_instance_id=cos_instance.id,
    region=region,
    storage_class="standard",
    endpoint_type="public"
)

# Export the bucket details
pulumi.export("bucket_name", cos_bucket.bucket_name)
pulumi.export("bucket_region", cos_bucket.region)
pulumi.export("cos_instance_id", cos_instance.id)
```

</details>

<details>
<summary> Example 2: VPC with Subnets and Security Groups </summary>
<br/>

```py
import pulumi
import pulumi_ibm as ibm

config = pulumi.Config()
region = config.require("region")

# Create a VPC
vpc = ibm.is.Vpc(
    "my-vpc",
    name="my-development-vpc",
    resource_group=config.get("resource-group"),
    tags=["environment:dev"]
)

# Create a subnet
subnet = ibm.is.Subnet(
    "my-subnet",
    name="my-subnet",
    vpc=vpc.id,
    zone=f"{region}-1",
    ipv4_cidr_block="10.240.0.0/24",
    tags=["environment:dev"]
)

# Create a security group
security_group = ibm.is.SecurityGroup(
    "my-security-group",
    name="my-security-group",
    vpc=vpc.id,
    rules=[
        ibm.is.SecurityGroupRuleArgs(
            direction="inbound",
            ip_version="ipv4",
            protocol="tcp",
            port_min=22,
            port_max=22,
            remote="0.0.0.0/0"
        ),
        ibm.is.SecurityGroupRuleArgs(
            direction="inbound",
            ip_version="ipv4",
            protocol="tcp",
            port_min=80,
            port_max=80,
            remote="0.0.0.0/0"
        )
    ]
)

# Export VPC details
pulumi.export("vpc_id", vpc.id)
pulumi.export("vpc_name", vpc.name)
pulumi.export("subnet_id", subnet.id)
pulumi.export("security_group_id", security_group.id)

```

</details>


<details>
<summary> Example 3: IAM Service ID and API Key</summary>
<br/>

```py
import pulumi
import pulumi_ibm as ibm

# Create a service ID
service_id = ibm.iam.ServiceId(
    "my-service-id",
    name="my-app-service-id",
    description="Service ID for my application"
)

# Create an API key for the service ID
api_key = ibm.iam.ServiceApiKey(
    "my-api-key",
    name="my-app-api-key",
    iam_service_id=service_id.iam_id,
    description="API key for my application"
)

# Export the API key (be careful with this in production!)
pulumi.export("api_key_value", api_key.apikey)
```

</details>

<details>
<summary> Example 4: Kubernetes Cluster with Node Pool </summary>
<br/>

```py
import pulumi
import pulumi_ibm as ibm

config = pulumi.Config()

# Create a Kubernetes cluster
cluster = ibm.container.VpcCluster(
    "my-cluster",
    name="my-k8s-cluster",
    vpc_id=config.require("vpc_id"),
    subnet_ids=config.require_object("subnet_ids"),
    kube_version=config.get("kube_version") or "1.28",
    flavor=config.get("flavor") or "bx2.4x16",
    worker_count=config.get_int("worker_count") or 2,
    resource_group_id=config.get("resource_group_id"),
    tags=["environment:dev", "managed-by:pulumi"]
)

# Create a worker pool
worker_pool = ibm.container.VpcWorkerPool(
    "my-worker-pool",
    cluster=cluster.id,
    flavor=config.get("worker_pool_flavor") or "bx2.4x16",
    worker_count=config.get_int("worker_pool_count") or 3,
    name="additional-worker-pool",
    vpc_id=config.require("vpc_id"),
    subnet_ids=config.require_object("subnet_ids")
)

# Export cluster details
pulumi.export("cluster_id", cluster.id)
pulumi.export("cluster_name", cluster.name)
pulumi.export("kube_version", cluster.kube_version)
```

</details>

## Best Practices

**(a) Configuration Management with Dataclasses**

Instead of scattering configuration access throughout your code, create dedicated configuration classes that centralize all your configuration needs. This provides several benefits:

- Type Safety: Catch configuration errors at development time rather than deployment time.
- Documentation: The configuration structure serves as documentation for what settings are available
- Validation: You can add validation logic to ensure configuration values are correct
- Reusability: The same configuration pattern can be used across multiple projects

This dataclass example shows how to create a clean, typed configuration interface that validates required settings and provides sensible defaults for optional ones.

```py
from dataclasses import dataclass
from typing import List, Optional
import pulumi

@dataclass
class AppConfig:
    region: str
    resource_group: str
    environment: str
    tags: List[str]
    
    @classmethod
    def from_pulumi_config(cls):
        config = pulumi.Config()
        return cls(
            region=config.require("region"),
            resource_group=config.get("resource-group") or "default",
            environment=pulumi.get_stack(),
            tags=config.get_object("tags") or ["managed-by:pulumi"]
        )

app_config = AppConfig.from_pulumi_config()
```

**(b) Error Handling and Validation**

Resource naming constraints vary across cloud providers, and IBM Cloud has specific requirements for resource names. Instead of discovering naming issues during deployment, implement proactive validation:

 - Consistency: Ensure all resources follow a consistent naming pattern across your organization
 - Compliance: Enforce naming conventions that include environment, project, and team information
 - Uniqueness: Prevent naming collisions by incorporating stack names and timestamps
 - Readability: Make resource names meaningful for operations teams

The validation function below demonstrates how to programmatically enforce naming standards, ensuring your infrastructure remains organized and maintainable.


```py
import re
import pulumi

def validate_resource_name(name: str) -> str:
    """Validate and format resource names."""
    stack = pulumi.get_stack()
    formatted_name = f"{name}-{stack}".lower()
    # Remove invalid characters
    cleaned_name = re.sub(r'[^a-z0-9-]', '-', formatted_name)
    # Ensure it starts with a letter
    if not cleaned_name[0].isalpha():
        cleaned_name = f"res-{cleaned_name}"
    return cleaned_name

# Usage
cos_instance = ibm.resource.Instance(
    "cos",
    name=validate_resource_name("my-app-cos"),
    # ... other properties
)
```

**(c) Tagging Strategy**

Tags are crucial for cost management, operations, and security in cloud environments. A well-designed tagging strategy helps:

- Cost Allocation: Track spending by department, project, or environment.
- Operations: Filter and search resources during incident response.
- Automation: Enable automated policies based on tag values.
- Compliance: Demonstrate resource ownership and purpose.

The tagging utility functions below shows how to implement a consistent tagging approach that combines base tags (applied to all resources) with resource-specific tags, making your infrastructure self-documenting.

```py
from typing import Dict
import pulumi

def get_base_tags() -> Dict[str, str]:
    """Get base tags for all resources."""
    return {
        "Environment": pulumi.get_stack(),
        "ManagedBy": "pulumi",
        "Project": "my-project",
        "Created": "2024-01-01"  # In real code, use datetime
    }

def apply_tags(tags: Dict[str, str]) -> pulumi.Input[list]:
    """Convert tag dictionary to IBM Cloud tag format."""
    base_tags = get_base_tags()
    all_tags = {**base_tags, **tags}
    return [f"{k}:{v}" for k, v in all_tags.items()]

# Usage
cos_instance = ibm.resource.Instance(
    "cos",
    name="my-cos",
    service="cloud-object-storage",
    plan="standard",
    tags=apply_tags({"Purpose": "application-data"})
)
```

**(d) Resource Dependencies and Ordering**

While Pulumi can often infer dependencies automatically, explicit dependency declaration is crucial for:

- Predictable Deployments: Ensure resources are created in the correct order
- Error Prevention: Avoid race conditions where resources reference others that don't exist yet
- Clear Intent: Make the resource relationships obvious to other developers
- Performance: Optimize deployment parallelism where safe

The dependency example below demonstrates how to explicitly declare relationships between resources, particularly important when dealing with networking components that must exist before dependent resources.

```py
import pulumi
import pulumi_ibm as ibm

# Explicit dependency management
vpc = ibm.is.Vpc("main-vpc", name="main-vpc")

# Subnet depends on VPC
subnet = ibm.is.Subnet(
    "main-subnet",
    name="main-subnet",
    vpc=vpc.id,
    zone="us-south-1",
    ipv4_cidr_block="10.240.0.0/24",
    # Explicit dependency
    opts=pulumi.ResourceOptions(depends_on=[vpc])
)

# Security group depends on VPC
security_group = ibm.is.SecurityGroup(
    "main-sg",
    name="main-security-group",
    vpc=vpc.id,
    opts=pulumi.ResourceOptions(depends_on=[vpc])
)
```

**(e) Output Processing and Transformation**

Pulumi's Output system handles the asynchronous nature of cloud resource creation. Proper output management enables:

- Data Transformation: Process resource attributes into useful formats
- Cross-Resource References: Safely use outputs from one resource as inputs to another
- Runtime Configuration: Generate configuration files, connection strings, or URLs based on created resources
- Monitoring: Export meaningful information for operations teams

The output processing examples show how to work with Pulumi's functional programming model to transform and combine resource outputs, creating valuable derived information from your infrastructure.

```py
import pulumi
import pulumi_ibm as ibm

cos_instance = ibm.resource.Instance("cos", ...)

# Process outputs
cos_endpoint = cos_instance.id.apply(
    lambda id: f"https://{id}.s3.us-south.cloud-object-storage.appdomain.cloud"
)

# Combine multiple outputs
cluster_details = pulumi.Output.all(
    cluster.id, 
    cluster.name, 
    cluster.kube_version
).apply(lambda args: {
    "id": args[0],
    "name": args[1],
    "version": args[2]
})

pulumi.export("cos_endpoint", cos_endpoint)
pulumi.export("cluster_details", cluster_details)
```

**(f) Security Practices**

When working with IBM Cloud IAM, follow security best practices:

- **Secrets**:  Store sensitive data using `pulumi config set --secret <key>`
- **State Management**: Use Pulumi Cloud or IBM COS bucket for secure state storage.
- Commit only code, not `.pulumi/` state directories.
- Follow Principle of Least Privilege.

**(g) Cleanup: Implement automated cleanup of unused resources.**

**(h) Wrap patterns in reusable functions or classes.**

## Troubleshooting Common Issues

a) Authentication Problems

```bash
# Verify IBM Cloud login
ibmcloud account show

# Check API key
echo ${IBMCLOUD_API_KEY}

# Test with Pulumi preview
pulumi preview
```

b) Python Dependency Issues

```bash
# Ensure you're in the virtual environment
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Update Pulumi
pulumi update
```

c) Resource Naming Conflicts

```py
# Use unique names with stack suffix
def get_resource_name(base_name: str) -> str:
    stack = pulumi.get_stack()
    return f"{base_name}-{stack}"
````

## References

- [Pulumi IBM Cloud Provider](https://www.pulumi.com/registry/packages/ibm/)
- [IBM Cloud Terraform Modules](https://github.com/terraform-ibm-modules)
- [Pulumi Terraform Conversion Guide](https://www.pulumi.com/docs/using-pulumi/adopting-pulumi/migrating/terraform/)
- [terraform-ibm-base-ocp-vpc Module](https://github.com/terraform-ibm-modules/terraform-ibm-base-ocp-vpc)
