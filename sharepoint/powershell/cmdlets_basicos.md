# Powershell. Cmdlets básicos de Sharepoint

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
## Crear y eliminar listas

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
