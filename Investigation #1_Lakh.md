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

### Step Two: Establishing a Suspect - The Flag in the Tags

The next step was to investigate the misnamed resource group. In it was only one resource. Upon expanding its Tags blade, the 'intern-tag' was discovered.
IMAGE
The intern was previously instructed to use this identifying tag whenever they documented resources. This certainly establishes the intern as a prime suspect.

### Step Three: Confirming the Culprit - Establishing a Timeline of Events

The intern is being implicated as the culprit behind this mistake. Timestamps can help create a clearer picture of when this happened.Thus the next step is to examine the ARM deployment. In the respective blades is found information such as the timestamp below.
IMAGE
Furthermore, it is revealed that the deployment was also misnamed. 
IMAGE
Through the flag discovery and the timestamps pointing to them, the conclusion can be made that the intern was indeed the culprit.

### Step Four: Establishing the Why - Governance Mistakes

It is now necessary to understand why this deployment was allowed to go through at all. Policy should prevent such things from happening. Upon analysis of the policies blade, it is confirmed that this resource is non-compliant. 
IMAGE
Upon inspecting its parameters, it is revealed that the non-compliant effect is set to 'audit'. And therein is the rub. 
IMAGE
Thus, it can be assumed that a governance misconfiguration error has occurred. 

## What broke / what surprised me
It is fascinating that an 'audit' policy, despite flagging the mistake, is not a sufficient control to stop this seemingly benign yet potentially costly incident. The importance of correctly assigning azure policies and resource locks must therefore be an extremely meticulous and painstaking endeavour. 

## Findings and recommendations
What you determined, plus 2 or 3 recommendations as if you were reporting to the resource owner.

## What I learned
3 to 5 bullets. At least one technical, one "what I'd do differently."
