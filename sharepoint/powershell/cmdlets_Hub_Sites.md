# Cmdlets para gestionar Hub Site

Install-Module Microsoft.Online.SharePoint.PowerShell -Force

# Conectar con PowerShell
```PowerShell
Connect-SPOService `
    -Url https://zg7wc-admin.sharepoint.com
```
# Ver los Hub Sites

```PowerShell
Get-SPOHubSite
```
