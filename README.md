# Awesome-Infrastructure-Control-Planes

## Top Infrastructure Control Planes Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on Infrastructure as Code Orchestration, Continuous Reconciliation & Self-Hosted Control Planes*  

**Last updated: October 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **Infrastructure Control Planes**. These tools provide the orchestration layer for managing cloud infrastructure—handling state, enforcing policy, detecting drift, and executing changes—whether through triggered CLI runs (Terraform-style) or continuous reconciliation loops (Kubernetes-native).



**Examples** include Terraform Cloud, Pulumi Cloud, Spacelift, env0, Scalr, Crossplane, AWS CloudFormation, Azure Bicep, Google Cloud Deployment Manager, and Morpheus Data (the category leaders).



**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, avoiding per-resource SaaS pricing, and retaining full control over infrastructure state and policy. The open-source landscape is anchored by **OpenTofu** (the MPL-licensed Terraform fork), **Crossplane** (the Kubernetes-native control plane with continuous reconciliation), **Pulumi** (the multi-language IaC engine with self-managed backend), **Atlantis** (the self-hosted PR automation tool), and **CloudFormation** (AWS's native IaC, free with AWS usage). Note: Google Cloud Deployment Manager is effectively deprecated, with Terraform and Config Controller as the recommended paths .



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [Sector Overview & Market Dynamics](#sector-overview--market-dynamics)
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## Sector Overview & Market Dynamics

The global Infrastructure as Code (IaC) and Cloud Systems Management market is estimated at **$1.5B to $7B+** (broad cloud automation software reaching upwards of $40B+), compounding at an annual growth rate (CAGR) of **~20–24%**. Market dynamics reflect a **moderately fragmented yet bifurcated sector**: hyperscalers dominate native workloads with free proprietary tooling, while independent orchestration is anchored by category champions alongside emerging multi-IaC orchestration startups, preventing a single "winner-take-all" outcome.

## SaaS/Hosted Platforms

| Platform | Company Valuation / Revenue | Pricing (Starting Tier) | Free Tier Limits | Key Highlights & Architecture |
| :--- | :--- | :--- | :--- | :--- |
| **[Microsoft (Azure Bicep)](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/)** | Market Cap: ~$3.1T+ / Revenue: ~$245B+ | **$0.00** (Included with Azure resource usage; no engine license fees) | **Free forever without operational limits** (Zero tool cost; standard Azure resource deployment quota limits apply) | Native domain-specific language compiling to ARM JSON; VS Code extension with IntelliSense and what-if preview. |
| **[Amazon AWS (CloudFormation)](https://aws.amazon.com/cloudformation/)** | Market Cap: ~$2.0T+ / Revenue: ~$100B+ (AWS) | **$0.00** for standard `AWS::*` resources; **$0.0009** per third-party/hook operation | **Free forever for all standard AWS resources**; 1,000 extension handler operations/month free for third-party extensions | Native JSON/YAML template engine, change sets, drift detection, and StackSets across multi-account/multi-region setups. |
| **[HashiCorp (Terraform Cloud / HCP Terraform)](https://www.hashicorp.com/products/terraform)** | Valuation: $6.4B (Acquired by IBM) / Revenue: ~$646M | **$0.10 / resource / month** (Essentials tier; Standard tier starts at $0.47 / resource / month) | **Up to 500 managed resources free forever**, 1 concurrent run, unlimited users, VCS integrations | Official managed platform for Terraform/OpenTofu; provides remote state, Sentinel/OPA policies, and team collaboration. |
| **[Pulumi (Pulumi Cloud)](https://www.pulumi.com/cloud/)** | Valuation: ~$1.5B (Series D) / Revenue: ~$15M–$20M+ ARR | **$40 / month** (Essentials tier, includes up to 500 managed resources and unlimited users) | **Free forever for 1 user**, unlimited resources and stacks, includes up to 500 deployment workflow minutes/month | Multi-language IaC engine (TypeScript, Python, Go, C#); managed state, Pulumi ESC secrets, drift detection, and Pulumi Neo AI. |
| **[Morpheus Data (HPE Morpheus Software)](https://www.morpheusdata.com/)** | Valuation: ~$83M+ prior to acquisition (Acquired by HPE) / Revenue: Enterprise multi-million ARR | Custom / **Per-socket software pricing** (Starting via HPE GreenLake private cloud plans) | **60-day free trial** (up to 6 sockets with VM Essentials evaluation) or **365-day Community Edition** (up to 3 sockets for non-production lab use) | Enterprise CMP for hybrid cloud & bare metal orchestration; self-service catalog, governance, and VMware-to-KVM migration. |
| **[env0](https://www.env0.com/)** | Valuation: ~$72M (Series A) / Revenue: ~$5M+ ARR | Custom annual contracts (Paid tiers: *Cloud Navigator* & *Cloud Pilot* with unlimited runs & concurrency) | **Free forever for up to 250 runs/month**, up to 30 active environments, unlimited users and agents | Multi-IaC platform supporting Terraform, OpenTofu, Terragrunt, and Pulumi; native FinOps cost tracking and role-based policies. |
| **[Spacelift](https://spacelift.io/)** | Funding: ~$73M raised (Series C) / Revenue: ~$5M–$10M ARR | **~$20,000 / year** (Starter+ entry paid tier with private workers & annual commitment) | **Free forever for up to 2 users**, 1 public worker (1 concurrent run), unlimited stacks & VCS integrations; 14-day full-feature trial for paid tier | Concurrency-driven multi-IaC orchestration supporting Terraform, OpenTofu, Pulumi, CloudFormation, and Kubernetes; OPA policies. |
| **[Scalr](https://scalr.com/)** | Funding: ~$7.35M raised / Revenue: ~$3M–$5M ARR | **$0.99 / run** (Pay-as-you-go Business plan for runs beyond monthly free quota) | **Free forever for up to 50 runs/month**, includes 5 concurrent runs, unlimited users, environments, OPA policies, and drift detection | Drop-in Terraform Cloud replacement; run-based billing, PR comment controls (`/scalr plan`, `/scalr apply`), and full OPA governance. |

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
