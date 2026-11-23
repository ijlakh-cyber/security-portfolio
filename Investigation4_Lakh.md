# The Friday Deploy
## PLACEHOLDER
_________________

## Scenario

The organisation, now wary following a recent security breach, has requested an audit of its Azure tenant to identify any violations of least-privilege that require remediation.

## Environment
Platform: Microsoft Azure  
Cloud environment: Live multi-user Azure training tenant  
Services: Azure Resource Manager (RBAC), Microsoft Entra ID, Privileged Identity Management (PIM), Azure Resource Graph  
Tools: Azure Portal, Azure CLI, Resource Graph Explorer (KQL), PIM  
Access level: Reader (read-only), with one PIM-eligible Azure role  
Scope: Assigned training tenant, including Azure resource role assignments across management groups, subscriptions, resource groups, and individual resources.  

## Documentation & Redaction  
Screenshots included in this report have been selectively censored to remove sensitive environment identifiers and preserve the confidentiality of the training tenant. Lab flags and challenge-specific identifiers have also been redacted to maintain the integrity of the exercise and avoid disclosing solutions.


## Methodology

[Explain how you approached the review.]

[Describe how you used the existing production deployment as a baseline, despite having no written configuration standard.]

[Briefly explain the five areas examined.]

## Findings

### The Where — Regional Deployment

**Observation:**  
[What did you discover about the deployment's location?]

**Evidence:**  
[What configuration did you examine, and what did you compare it against?]

**Impact:**  
[Why does this matter?]

**Recommendation:**  
[What should be changed?]

### The Who — Workload Identity

**Observation:**  
[What did you discover about the Function App's identity?]

**Evidence:**  
[What did you find when comparing the intern's deployment against production?]

**Impact:**  
[What are the security implications?]

**Recommendation:**  
[What should be changed?]

### The Leak — Storage Exposure

**Observation:**  
[What did you discover about the storage configuration?]

**Evidence:**  
[How did you verify the exposure?]

**Impact:**  
[What data could be accessed, and under what conditions?]

**Recommendation:**  
[What needs to be secured?]

### The Door — Inbound Network Access

**Observation:**  
[What did you discover about inbound access restrictions?]

**Evidence:**  
[What did you find when comparing the Function Apps?]

**Impact:**  
[Why does this matter for the service?]

**Recommendation:**  
[What should be changed?]

## The Call — Risk Prioritisation

[Identify the finding requiring immediate remediation.]

[Explain why it takes priority over the other findings.]

**Prioritisation principle:**  
Exposure beats hygiene. Active beats potential.

[Explain how you ranked the remaining findings and why.]

## Recommendations and Remediation

[List the actions required before production promotion.]

- [Immediate remediation]
- [Identity and authentication improvements]
- [Regional deployment correction]
- [Inbound access restrictions]
- [Additional deployment review/checklist]

## Conclusion

[Summarise the review, its outcome, and whether the deployment should be approved for production promotion.]
