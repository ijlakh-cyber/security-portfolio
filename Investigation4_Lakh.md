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

[Explain screenshot censorship, removal of environment identifiers, and flag redaction.]

## Review Methodology

[Explain the approach: comparing the intern's deployment against an existing production deployment to establish a working configuration baseline.]

[Introduce the five review areas.]

## The Deployment Review

### Step 1: The Where — Regional Deployment

[Investigation, evidence, finding and impact.]

### Step 2: The Who — Workload Identity

[Investigation, evidence, finding and impact.]

### Step 3: The Leak — Storage Exposure

[Investigation, evidence, verification and impact.]

### Step 4: The Door — Inbound Network Access

[Investigation, evidence, finding and impact.]

### Step 5: The Call — Risk Prioritisation

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
