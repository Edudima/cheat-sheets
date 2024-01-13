# Recuperar sitio eliminado de Sharepoint mediante Powershell

Como recuperar sitio de Sharepoint mediante Powershell cuando no aparece en el panel de Office 365.

#### 1. Descargar herramienta "Sharepoint Online Management Shell"

Esta herramienta se encuentra en el sitio oficial de Microsoft. Dejo el enlace aquí: [Sharepoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588 "Sharepoint Online Management Shell")

#### 2. Nos conectamos al tenant de Office 365 mediante Powershell ISE

Abrimos Powershell ISE con permisos de administrador, y nos conectamos al tenant de Office 365 con el siguiente comando:

`Connect-SPOService https://nombredetutenant.sharepoint.com/`

#### 3. Comprobar sitios eliminados

Comprobamos el listado de sitios de Sharepoint eliminados:

`Get-SPODeletedSite`

#### 4. Restauramos el sitio de Sharepoint eliminado

`Restore-SPODeletedSite  https://nombredetutenant.sharepoint.com/sites/nombre-de-sitio-eliminado`
