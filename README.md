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


Connect-MGGraph -Scopes "Domain.ReadWrite.All", "Directory.AccessAsUser.All"
Update-MgDomain -DomainId "ciam.jettech.cc" -BodyParameter @{AuthenticationType="Federated"}
