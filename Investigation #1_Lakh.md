# Investigating Azure Policy Misconfiguration and Governance Failures

## Scenario
A junior intern was granted temporary Contributor access within a live, multi-user Azure training tenant to deploy a test environment. Following the discovery of a non-compliant deployment, an investigation was initiated to assess resource configuration, identify deviations from organisational naming and tagging standards, and determine why Azure Policy enforcement failed to prevent such a deployment.

## Environment
Platform: Microsoft Azure    
Cloud environment: Live multi-user Azure training tenant    
Services: Azure Policy, Resource Groups, Azure Resource Manager (ARM)   
Tools: Azure Portal    
Access level: Reader (read-only)    
Scope: Assigned training subscription and associated resource groups

## Documentation & Redaction  
Screenshots included in this report have been selectively censored to remove sensitive environment identifiers and preserve the confidentiality of the training tenant. Lab flags and challenge-specific identifiers have also been redacted to maintain the integrity of the exercise and avoid disclosing solutions.

## Investigation Procedure
The core. Numbered steps IN YOUR OWN WORDS: what you looked at, what you found, what you concluded at each step. 6 to 12 screenshots of meaningful moments (portal views, query results, before/after).
### Step One: Finding the Culprit - An Improper Naming Convention
The first step was to discover the offending deployment. One such deployment was immediately suspect, as it was the only one that did not follow the recommended Microsoft RG naming convention. 
2. 

## What broke / what surprised me
The most credible section in the document. Dead ends, wrong guesses, the thing that took an hour. Employers know real work is messy. This section separates you from certificate collectors.

## Findings and recommendations
What you determined, plus 2 or 3 recommendations as if you were reporting to the resource owner.

## What I learned
3 to 5 bullets. At least one technical, one "what I'd do differently."
