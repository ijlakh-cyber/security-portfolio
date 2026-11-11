# The Stolen Identity
## Forensic reconstruction of a five-stage OAuth consent-phishing kill chain across two linked app registrations
_________________

## Scenario
An adversary was able to infiltrate the organisation's tenant. During the intrusion, no security alerts were raised, nor did monitoring systems in place identify any suspicious activity. The initial compromise reveals only that a company employee was phished and their session token stolen through a fake login page. The employee also fulfilled MFA, meaning that the attacker was able to use the stolen MFA-satisfied token to bypass Conditional Access policies in place. This investigation will first attempt to identify the point of entry, then retrace each stage of the attack path using uncovered evidence. The objective is thus: to uncover where the adversary got in, what they did, and what they took.  

## Environment
Platform: Microsoft Azure    
Cloud environment: Live multi-user Azure training tenant    
Services: Microsoft Entra ID (App registrations)
Tools: Azure Portal    
Access level: Reader (read-only)    
Scope: Assigned training tenant, including the two linked app registrations and their associated configuration and identity objects.

## Documentation & Redaction  
Screenshots included in this report have been selectively censored to remove sensitive environment identifiers and preserve the confidentiality of the training tenant. Lab flags and challenge-specific identifiers have also been redacted to maintain the integrity of the exercise and avoid disclosing solutions.

## Investigation Procedure
### Step One: Entry
The employee interacted with a fake login page. The employee, believing the integrity of the login portal, also fulfilled MFA. The attacker stole the MFA-satisfied session token, and used it to bypass the active Conditional Access policies. In other words, the attacker has taken control of an employee account. Under the guise of a legitimate employee, it is much harder to detect suspicious activity, perhaps somewhat explaining the failure of monitoring systems in place. Disastrously, the principle of least privilege had been neglected, leaving an employee account as the owner of a legacy application for which it had no apparent need. The power of an owner account should never be taken for granted.   

### Step Two: Escalation
By itself a standard account would not have much power in this scenario. However the problem is that the legacy application's service principal does. Through poor access control management, this standard employee account inadvertently has owner account power over this legacy application. If the attacker can assume control of the service principal, they will obtain the permissions of the service principal, which is (in this instance) far more powerful than the permissions of a standard account. 

To this end, the attacker modified the certificates and secrets by leveraging their owner privileges. This enabled them to add a new client secret to the application.  

![lab2-01](Screenshots/Lab2/lab2-01.png) 
<sup><sub> **Client secret created by the adversary. Note the abnormal expiration date.** </sub></sup>

The client secret is effectively the password that allows the attacker to prove they are the application. The secret doesn't grant the permissions itself, but rather allows the attacker to authenticate as the application using the client ID (like a username) and newly generated client secret (like a password). The application has an associated service principal in the tenant, which holds the application's granted permissions. By authenticating as this service principal, the attacker can exercise those permissions. In essence, the attacker has transitioned from operating under a compromised standard user identity to authenticating as a highly privileged application identity. Also note the abnormally long expiration date. Typically these secrets will exist for at most two years. This deliberate setting makes it less likely that the credential will expire naturally.

So what can the attacker do with their new application identity that they couldn't with the standard user identity? That is answered by assessing the legacy application permissions. The initial brief reveals that the legacy application had Microsoft Graph application permissions with admin consent. Thus, we can conclude that the attacker inherited the ability to exercise whatever Microsoft Graph application permissions have been granted to the legacy application.

### Step Three: Pivoting
Despite their new permissions, the attacker has a problem. Despite its long expiration date, the client secret as it stands can simply be revoked or rotated by the security team. This means the loss of the ability to masquerade as the application identity, and lose the authentication route therein.

To this end, the attacker used the initially compromised standard employee identity to register a new application. Standard users can register applications by default in many Entra tenants. This action by itself is not unusual. 

![lab2-02](Screenshots/Lab2/lab2-02.png) 
<sup><sub> **The adversary registered a new application.** </sub></sup>

<br>
<br> 


However, the attacker then added the service principal of this new application to the owners list of the legacy application (using the owner privileges mistakenly left on the standard employee account). 

![lab2-03](Screenshots/Lab2/lab2-03.png) 
<sup><sub> **The adversary added the new application to the owners list of the legacy application.** </sub></sup>

The implications of this are severe. Now the attacker can continuously mint credentials on a whim (assuming existing permissions do not change), negating the risks of losing authentication to the legacy application identity. 

### Step Four: Persistence

The attacker was inside the tenant, and had established some territory, but now needed a door to get in and out. They accomplished this task using Expose an API on the legacy application. In essence this enabled the legacy application to function as the door, by allowing other applications (such as the attacker's rogue application) to request access, provided they have the right permissions. 

This creates the door, but does not give the attacker permission to use it. That is accomplished using a custom permission called a scope on the legacy application.

![lab2-04](Screenshots/Lab2/lab2-04.png) 
<sup><sub> **The adversary added a custom scope to the legacy application.** </sub></sup>

The attacker has now established an alternative route for their rogue application to request access to the legacy application, independent of the original client secret. This provides another layer of persistence, should that original authentication method be revoked.

### Step Five: Looting

With the rogue application and custom scope in place, the attacker can now go after other users in the tenant. First, the attacker configured an attacker-controlled redirect URI on the rogue application. This is the address Microsoft sends the user back to after they approve a sign-in request, along with a code the app can exchange for an access token. Simply put, the attacker created a 'trap' redirect URI on their rogue application.

![lab2-05](Screenshots/Lab2/lab2-05.png) 
<sup><sub> **The adversary created a trap redirect URI on the rogue application.** </sub></sup>

Next, the attacker constructed a malicious OAuth URL piece by piece. The components of this URL are the attacker's client ID, the trap redirect URI, and the exposed scope. The attacker can then deliver that crafted URL to a targeted employee through a phishing email (among other methods).

![lab2-06](Screenshots/Lab2/lab2-06.png) 
<sup><sub> **An employee is prompted with this malicious consent request.** </sub></sup>

If an employee clicks this URL and approves the consent request, Microsoft sends the authorization code to the attacker's redirect URI. The attacker must exchange the code for the access token to the legacy application's exposed API, acting on behalf of the employee. In other words, the employee has effectively authorised the attacker's rogue application to access the legacy application, giving the attacker delegated access to the exposed API.

This approval also creates what is known as an OAuth permission grant. In essence, Entra ID records that the employee has authorised the rogue application to access the legacy application's exposed API on their behalf. The problem is that this grant exists independently of the employee's password and sign-in sessions. Even if the security team resets the employee's password or revokes their active sessions, the permission remains in place until explicitly removed. The attacker has not just stolen access to an account. They have convinced Microsoft to remember that their application is authorised to access another application. That is why the security team must separately remove the rogue application's permission grant.

## Summary of Findings

## Recommendations

## Key Takeaways

## Unexpected Findings
