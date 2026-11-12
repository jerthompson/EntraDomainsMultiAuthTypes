# Entra Domains Multi Authentication Types (Per Domains)
### Research Environment Requirements
## Server Setup
### On-Premises Active Directory 
### Entra Connect Setup
## Network Setup
### Firewall Changes
## Azure Account Setup
### Custom Domains
### Cloudflare Changes 
### Promote Sub Domain to root
<img width="2767" height="1747" alt="image" src="https://github.com/user-attachments/assets/41845df8-26cb-45e3-9dae-84b29a40b6d4" />
<img width="1875" height="1750" alt="image" src="https://github.com/user-attachments/assets/8d91caed-0c36-4d18-909f-ffbec2e08140" />

### Convert to Federated Domain
```
# Configure SAML Federation in Microsoft Entra ID

#Run the following PowerShell commands using the **Microsoft Graph PowerShell SDK** to convert a managed domain to federated and verify the configuration.

#1. Connect and Apply SAML Configuration

# **Note:** Sign in using a `*.onmicrosoft.com` Global Administrator account. Ensure there are no trailing spaces after the backticks (`` ` ``).

powershell
# Connect to Microsoft Graph
Connect-MgGraph -Scopes "Domain.ReadWrite.All", "Directory.AccessAsUser.All"

# Apply SAML federation settings and convert the domain
New-MgDomainFederationConfiguration `
  -DomainId "yourdomain.com" `
  -DisplayName "Your IdP Name" `
  -IssuerUri "https://yourdomain.com" `
  -PassiveSignInUri "https://yourdomain.com" `
  -SignOutUri "https://yourdomain.com" `
  -SigningCertificate "MIIC3jCCAcagAwIBAgIQFsO0R8deG4h..." `
  -PreferredAuthenticationProtocol "saml" `
  -FederatedIdpMfaBehavior "acceptIfMfaDoneByFederatedIdp"
```

### 2. Verify the Configuration

```powershell
# Confirm AuthenticationType is now "Federated"
Get-MgDomain -DomainId "yourdomain.com" | Select-Object Id, AuthenticationType, IsVerified

# Inspect applied SAML endpoints and certificate details
Get-MgDomainFederationConfiguration -DomainId "yourdomain.com" | Format-List
```

Connect-MGGraph -Scopes "Domain.ReadWrite.All", "Directory.AccessAsUser.All"
Update-MgDomain -DomainId "ciam.jettech.cc" -BodyParameter @{AuthenticationType="Federated"}
