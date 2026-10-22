# Awesome-Infrastructure-Control-Planes

# Top Infrastructure Control Planes Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Infrastructure as Code Orchestration, Continuous Reconciliation & Self-Hosted Control Planes*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Infrastructure Control Planes**. These tools provide the orchestration layer for managing cloud infrastructure—handling state, enforcing policy, detecting drift, and executing changes—whether through triggered CLI runs (Terraform-style) or continuous reconciliation loops (Kubernetes-native).

**Examples** include Terraform Cloud, Pulumi Cloud, Spacelift, env0, Scalr, Crossplane, AWS CloudFormation, Azure Bicep, Google Cloud Deployment Manager, and Morpheus Data (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, avoiding per-resource SaaS pricing, and retaining full control over infrastructure state and policy. The open-source landscape is anchored by **OpenTofu** (the MPL-licensed Terraform fork), **Crossplane** (the Kubernetes-native control plane with continuous reconciliation), **Pulumi** (the multi-language IaC engine with self-managed backend), **Atlantis** (the self-hosted PR automation tool), and **CloudFormation** (AWS's native IaC, free with AWS usage). Note: Google Cloud Deployment Manager is effectively deprecated, with Terraform and Config Controller as the recommended paths .

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Terraform Cloud (HCP Terraform)](https://www.hashicorp.com/products/terraform)**  
  HashiCorp's managed platform for Terraform. Provides remote state, plan/apply execution, policy enforcement (Sentinel), and team collaboration. **Pricing is resource-based** (resources under management), which can become expensive at scale . **Licensing note**: Terraform moved from open-source to BSL in 2023, prompting the OpenTofu fork . Best for teams that want HashiCorp-backed managed Terraform with minimal operational overhead.

- **[Pulumi Cloud](https://www.pulumi.com/cloud/)**  
  The default state backend and managed platform for Pulumi. Adds RBAC with SAML/SSO, reusable configuration and secrets via Pulumi ESC, policy as code enforcement, cloud resource inventory, scheduled drift detection, managed deployments, and an AI agent (Pulumi Neo) for debugging and writing IaC . **Self-hosted edition available**. Best for teams using Pulumi that want a managed backend without running their own state infrastructure.

- **[Spacelift](https://spacelift.io/)**  
  IaC orchestration platform supporting Terraform, OpenTofu, Pulumi, CloudFormation, Kubernetes, and Ansible. **Concurrency-based pricing** (charges for parallel runs regardless of utilization) . **Starter tier** includes policy features but caps users at 10 and gates drift detection and SAML SSO to higher tiers . Best for teams running multiple IaC tools that want one control plane and deep workflow customization.

- **[env0](https://www.env0.com/)**  
  Multi-IaC platform with strong FinOps capabilities—cost tracking, budget controls, and per-environment cost attribution . **Free-forever tier**: 250 runs/month across up to 30 active environments with unlimited users (as of August 2026) . Best for teams where cost management and developer self-service are primary concerns.

- **[Scalr](https://scalr.com/)**  
  Terraform/OpenTofu-focused platform positioned as a drop-in Terraform Cloud replacement. **Usage-based pricing** (per-run) . Governance features (OPA policy enforcement with advisory/soft-mandatory/hard-mandatory levels, drift detection) are available on the **free tier**, unlike Spacelift where they're gated . Supports `/scalr plan` and `/scalr apply` PR comment commands . Best for Terraform-only teams migrating from Terraform Cloud that want deeper governance without enterprise-tier pricing.

- **[Morpheus Data](https://www.morpheusdata.com/)**  
  Cloud management platform for hybrid cloud environments. Provides unified provisioning, app lifecycle management, migration, self-service catalogs, and compliance controls across bare metal, VMs, and containers . **Quote-based pricing**; users note a learning curve for beginners and lack of visual drag-and-drop deployment . Best for mid-market and enterprise teams managing hybrid infrastructure that need a single control plane for cloud operations.

- **[AWS CloudFormation](https://aws.amazon.com/cloudformation/)**  
  AWS's native IaC service. **Free** (you pay only for provisioned resources). JSON/YAML templates with change sets for preview, automatic rollback on failure, drift detection, and StackSets for multi-account/multi-region deployment . Best for AWS-native teams that want zero-cost IaC with deep AWS integration.

- **[Azure Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/)**  
  Microsoft's purpose-built DSL that compiles to ARM JSON. **Free** with Azure usage. VS Code extension with IntelliSense, what-if for preview, and module registry . Best for Azure-native teams that want a cleaner alternative to raw ARM templates.

## Open-Source GitHub Projects

- **[OpenTofu](https://github.com/opentofu/opentofu)**  
  **The MPL-2.0 licensed Terraform fork.** Community-governed under the Linux Foundation, created after HashiCorp's BSL switch . **Terraform-compatible**: same HCL syntax, same providers, same modules. **New features beyond Terraform**: state and plan encryption, skip resources during plan/apply, provider iteration (`for_each`), early variable evaluation . **Migration is mechanical** for most workspaces—run `tofu init -upgrade` and `tofu plan` to verify . Best for teams that want Terraform compatibility with true open-source licensing and community governance.

- **[Crossplane](https://github.com/crossplane/crossplane)**  
  **The Kubernetes-native control plane.** CNCF Graduated project that extends Kubernetes with custom resources for cloud services (RDS, S3, Azure SQL, etc.) and platform abstractions . **Key architectural difference from Terraform**: continuous reconciliation rather than triggered runs—controllers observe live infrastructure and correct drift automatically, typically within a minute . **Crossplane v2** (August 2025) made composite resources and managed resources namespaced by default, removed claims for new XRs, and allowed compositions to include any Kubernetes resource . **Trade-offs**: no `plan` step (review happens on manifests, not diffs); the control-plane cluster becomes critical infrastructure; provider CRDs are heavy on the API server . Best for teams already running Kubernetes that want self-service infrastructure with GitOps-native workflows and continuous drift correction.

- **[Pulumi](https://github.com/pulumi/pulumi)**  
  Multi-language IaC engine with SDKs for TypeScript, Python, Go, C#, and Java. **Self-managed backend** available (DIY state storage) if you don't use Pulumi Cloud . Supports ephemeral environments (Review Stacks, TTL Stacks) and policy as code. **Trade-off**: some advanced features (AI agent, managed deployments) are Pulumi Cloud-specific. Best for teams that want general-purpose programming languages for infrastructure and are willing to manage their own state backend if avoiding SaaS.

- **[Atlantis](https://github.com/runatlantis/atlantis)**  
  **Self-hosted PR automation for Terraform.** Runs `terraform plan` on pull requests and applies on merge, with PR comments for control. **Free and open-source**. **Total cost includes operations**: hosting, scaling, patching, and upgrades typically consume 0.5–1 FTE; RBAC, audit trails, and drift detection must be assembled from other tools . Best for single teams that want plan/apply automation in PRs and have someone willing to operate it.

- **[AWS CloudFormation (Open Source Components)](https://github.com/aws-cloudformation)**  
  While the CloudFormation service is proprietary, AWS open-sources components like `cfn-lint` (template validation), `cfn-guard` (policy as code), and the CloudFormation CLI for resource providers. Best for teams building custom tooling around AWS-native IaC.

### Additional Strong Open-Source Options

- **Terragrunt** — A thin wrapper for Terraform/OpenTofu that provides DRY configurations, remote state management, and dependency handling between modules. Best for teams managing many Terraform workspaces.
- **Config Controller (GCP)** — Google's recommended replacement for Deployment Manager, providing Kubernetes-native management of GCP resources via Config Connector. Best for GCP teams that want a Crossplane-like experience .
- **Frameworks for building custom systems**: Use **OpenTofu** as the IaC engine with **Atlantis** for PR automation if self-hosting, or **Scalr** if you want managed governance without enterprise pricing. Choose **Crossplane** when Kubernetes-native continuous reconciliation and GitOps are priorities, potentially alongside OpenTofu for stable foundation layers . Use **Pulumi** when application developers need to define infrastructure in general-purpose languages.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **Execution model matters more than tool name**: Terraform/OpenTofu/Pulumi use triggered runs with a `plan` preview; Crossplane uses continuous reconciliation without a `plan` step . Choose based on whether you want explicit approval gates or automatic drift correction.
- **Pricing models vary significantly**: Spacelift charges by concurrency (costly for bursty workloads); Terraform Cloud charges by resources under management (costly at scale); Scalr charges per-run; env0 offers a generous free tier . Model your actual usage pattern before committing.
- **Google Cloud Deployment Manager is effectively deprecated**: GCP recommends Terraform or Config Controller for new IaC deployments .
- **Terraform's BSL license restricts commercial redistribution**: OpenTofu (MPL-2.0) is the community-governed alternative for teams requiring OSI-approved open-source licensing .

---

**Made for platform engineers, DevOps teams, and organizations building declarative infrastructure management.**  
Let's make infrastructure control planes more open, appropriately scoped, and understandable.
