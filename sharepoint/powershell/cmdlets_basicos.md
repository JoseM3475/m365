# Powershell PnP. Cmdlets básicos de Sharepoint

## Instalar PnP PowerShell

```Powershell
Install-Module PnP.PowerShell -Scope CurrentUser
```

## Crear App Registration 
[Register an Entra ID Application to use with PnP PowerShell](https://pnp.github.io/powershell/articles/registerapplication.html)
1. Ir a EntraID.
2. Ir a App Registrations.
3. Hacer clic en New registration.
4. Configurar la aplicación.
5. Obtener ID

## API Permissions

Sharepoint/manage

## Redirect URI (Reply URL) para el flujo interactivo de autenticación.

1. Ir a Authentication.
2. Add Redirect URI.
3. Mobile and Desktop Applications.
4. Marcar:
- https://login.microsoftonline.com/common/oauth2/nativeclient
6. http://localhost
7. Settings: Allow public client flows
  
## Definir variable de entorno para acceder al ID de la App Registration

```Powershell
$env:ENTRAID_APP_ID="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```


## Conectarse al sitio

```Powershell
Connect-PnPOnline `
    -Url "https://zg7wc.sharepoint.com/sites/CursoSharepointSPFx" `
    -Interactive
```
## Ver las carpetas que hay en Documents
```PowerShell
Get-PnPFolderItem `
    -FolderSiteRelativeUrl "Shared Documents" `
    -ItemType Folder |
Select-Object Name
```

## Listas

### Ver listas

##### Listar todas las listas del sitio
```PowerShell
Get-PnPList
```
#### Ver las listas bajo /Lists
```PowerShell
Get-PnPList | Where-Object {`
    $_.RootFolder.ServerRelativeUrl -match "/Lists/"`
} | Select-Object Title, RootFolder
```
#### Obtener una lista concreta
```PowerShell
Get-PnPList -Identity "Countries"
```
#### Ver propiedades de una lista
```PowerShell
Get-PnPList -Identity "Countries" | Format-List *
```
### Crear listas
#### Crear una lista personalizada
```PowerShell
New-PnPList `
-Title "Clientes" `
-Template GenericList
```
#### Crear una biblioteca de documentos
```PowerShell
New-PnPList `
-Title "Contratos" `
-Template DocumentLibrary
```

Plantillas habituales:

Plantilla	Tipo
GenericList	Lista personalizada
DocumentLibrary	Biblioteca documental
Tasks	Tareas
Contacts	Contactos
Events	Calendario
Announcements	Anuncios

Ver plantillas disponibles:

PowerShell
Get-PnPWebTemplates


Eliminar listas
PowerShell
Remove-PnPList `
-Identity "Clientes" `
-Force
Gestionar columnas
Ver columnas
PowerShell
Get-PnPField -List "Clientes"
Crear columna de texto
PowerShell
Add-PnPField `
-List "Clientes" `
-DisplayName "Telefono" `
-InternalName "Telefono" `
-Type Text
Crear columna numérica
PowerShell
Add-PnPField `
-List "Clientes" `
-DisplayName "Importe" `
-InternalName "Importe" `
-Type Number
Crear columna fecha
PowerShell
Add-PnPField `
-List "Clientes" `
-DisplayName "FechaAlta" `
-InternalName "FechaAlta" `
-Type DateTime
Eliminar columna
PowerShell
Remove-PnPField `
-List "Clientes" `
-Identity "Telefono"
Gestionar elementos
Ver elementos
PowerShell
Get-PnPListItem `
-List "Clientes"
Obtener un elemento concreto
PowerShell
Get-PnPListItem `
-List "Clientes" `
-Id 1
Crear elemento
PowerShell
Add-PnPListItem `
-List "Clientes" `
-Values @{
Title="Contoso"
Telefono="600123456"
}
Modificar elemento
PowerShell
Set-PnPListItem `
-List "Clientes" `
-Identity 1 `
-Values @{
Telefono="699999999"
}
Eliminar elemento
PowerShell
Remove-PnPListItem `
-List "Clientes" `
-Identity 1 `
-Force
Gestionar vistas
Ver vistas
PowerShell
Get-PnPView `
-List "Clientes"
Crear vista
PowerShell
Add-PnPView `
-List "Clientes" `
-Title "Vista Comercial"
Establecer vista predeterminada
PowerShell
Set-PnPView `
-List "Clientes" `
-Identity "Vista Comercial" `
-Values @{DefaultView=$true}
Gestionar permisos
Romper herencia
PowerShell
Set-PnPList `
-Identity "Clientes" `
-BreakRoleInheritance
Ver permisos
PowerShell
Get-PnPProperty `
-ClientObject (Get-PnPList "Clientes") `
-Property RoleAssignments
 
Gestionar carpetas en listas
Crear carpeta
PowerShell
Add-PnPFolder `
-Name "2026" `
-Folder "Clientes"
Ver carpetas
PowerShell
Get-PnPFolderItem `
-FolderSiteRelativeUrl "Clientes" `
-ItemType Folder
Configuración de la lista
Habilitar versiones
PowerShell
Set-PnPList `
-Identity "Clientes" `
-EnableVersioning $true
Deshabilitar versiones
PowerShell
Set-PnPList `
-Identity "Clientes" `
-EnableVersioning $false
Ocultar lista
PowerShell
Set-PnPList `
-Identity "Clientes" `
-Hidden $true
Mostrar lista
PowerShell
Set-PnPList `
-Identity "Clientes" `
-Hidden $false
Exportación masiva
Obtener todos los elementos
PowerShell
Get-PnPListItem `
-List "Clientes" `
-PageSize 1000
Exportar a CSV
PowerShell
Get-PnPListItem -List "Clientes" |
ForEach-Object {
[PSCustomObject]@{
ID = $_["ID"]
Nombre = $_["Title"]
}
} | Export-Csv clientes.csv -NoTypeInformation

## Crear y eliminar bibliotecas

## Crear una carpeta
```PowerShell
Add-PnPFolder `
    -Name "Carpeta_PnP" `
    -Folder "Casos de Uso"
```
## Subir, descargar y eliminar documentos

## Crear, modificar y borrar elementos de listas

## Crear columnas

## Leer información del sitio.

## Gestionar vistas

## Aplicar plantillas PnP
