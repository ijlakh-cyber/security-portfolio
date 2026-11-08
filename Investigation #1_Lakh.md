# Investigating Azure Policy Misconfiguration and Governance Failures

## Scenario
A junior intern was granted temporary Contributor access within a live, multi-user Azure training tenant to deploy a test environment. Following the discovery of a non-compliant deployment, an investigation was initiated to assess resource configuration, identify deviations from organisational naming and tagging standards, and determine why Azure Policy enforcement failed to prevent such a deployment.

## Environment
Platform: Microsoft Azure    
Cloud environment: Live multi-user Azure training tenant    
Services: Resource Groups, Azure Resource Manager (ARM), Azure Policy
Tools: Azure Portal    
Access level: Reader (read-only)    
Scope: Assigned training subscription and associated resource groups

## Documentation & Redaction  
Screenshots included in this report have been selectively censored to remove sensitive environment identifiers and preserve the confidentiality of the training tenant. Lab flags and challenge-specific identifiers have also been redacted to maintain the integrity of the exercise and avoid disclosing solutions.

## Investigation Procedure
The core. Numbered steps IN YOUR OWN WORDS: what you looked at, what you found, what you concluded at each step. 6 to 12 screenshots of meaningful moments (portal views, query results, before/after).
### Step One: Finding the Non-Compliant Deployment - An Improper Naming Convention
The first step was to discover the offending deployment. Upon navigating through the Azure Portal into the Resource Manager and then accessing the list of Resource Groups, one such RG became immediately suspect, as it was only one that did not follow the recommended Microsoft RG naming convention. [Microsoft Naming Conventions](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming). This was the first flag of the lab, and thus it shall not be shown to preserve the integrity of the exercise. 

### Step Two: Confirming the Culprit - The Flag in the Tags

The next step was to investigate the suspect resource group. In it was only one resource. Upon expanding its Tags blade, the 'intern-tag' was discovered.
IMAGE
The intern was previously instructed to use this identifying tag whenever they documented resources. This confirms the suspicions that the intern was the one associated with this suspect deployment.

### Step Three: Establishing a Timeline of Events - Following the Trail

As the intern is being implicated as the culprit behind this mistake, let us look for timestamps to create a clear picture of when this happened. We can then compare this to our incident logs, to confirm without a shadow of a doubt that the intern made this deployment. Thus the next step is to examine the ARM deployment. In the respective blades is found information such as the timestamp below.

Furthermore, it is revealed that the deployment 


## What broke / what surprised me
The most credible section in the document. Dead ends, wrong guesses, the thing that took an hour. Employers know real work is messy. This section separates you from certificate collectors.

## Findings and recommendations
What you determined, plus 2 or 3 recommendations as if you were reporting to the resource owner.

## What I learned
3 to 5 bullets. At least one technical, one "what I'd do differently."
