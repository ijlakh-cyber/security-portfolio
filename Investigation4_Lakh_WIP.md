# The Friday Deploy
## Pre-Production Security Review of an Azure Function App

## Scenario

An intern at the organisation, unfamiliar with deployment best practices, completed the deployment of a new notification service at the end-of-day Friday. Before the service is released to production, a senior engineer will review the deployment.

## Environment

Platform: Microsoft Azure  
Cloud environment: Live multi-user Azure training tenant  
Services: Azure Functions, Azure Storage, Managed Identities, App Service Networking  
Tools: Azure Portal  
Access level: Reader (read-only)  
Scope: func-intern-notify and its associated storage account, compared against the production compute baseline.

## Documentation & Redaction

Screenshots included in this report have been selectively censored to remove sensitive environment identifiers and preserve the confidentiality of the training tenant. Lab flags and challenge-specific identifiers have also been redacted to maintain the integrity of the exercise and avoid disclosing solutions.

## Review Methodology

The review followed a baseline comparison approach, rather than working from a predefined list of deployment requirements. The intern's deployment was directly compared against a healthy production deployment, which served as a working configuration baseline. This provided a reference point for identifying differences in how the two deployments were configured and highlighted potential security or operational weaknesses.

The review examined four areas of the deployment, focusing on regional placement, workload identity, storage security, and inbound network access. Any findings were then assessed to determine their potential impact and establish remediation priorities where necessary.

## The Deployment Review

### Step 1: The Where — Regional Placement

[Investigation, evidence, finding and impact.]

### Step 2: The Who — Workload Identity

[Investigation, evidence, finding and impact.]

### Step 3: The Leak — Storage Exposure

[Investigation, evidence, verification and impact.]

### Step 4: The Door — Inbound Network Access

[Investigation, evidence, finding and impact.]

### Step 5: The Call — Risk Assessment

[Identify the finding requiring immediate remediation.]

[Explain the reasoning behind prioritising active exposure over configuration hygiene and potential risks.]

## Summary of Findings

[Consolidate the four findings, their significance, and their respective priorities.]

## Recommendations

- [Immediate remediation of the active exposure.]
- [Workload identity and credential improvements.]
- [Correct regional deployment.]
- [Inbound network access restrictions.]
- [Introduce a pre-production deployment checklist.]

## Key Takeaways
- [Lessons about reviewing deployments against an established baseline.]
- [Importance of verifying exposure rather than assuming it.]
- [Risk prioritisation and proactive security reviews.]
- [Cloud security considerations, including regional placement and egress costs.]
