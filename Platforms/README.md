> **General**
> - These scripts use REST API and can support v10.4 of PVWA and up.
> - The goal is to allow easy Export and Import of Platforms and Getting Platform details.
> - In these example scripts you will find examples of `Get-PlatformDetails`, Import and Export of Platforms.

# Export/Import Platform

>The Tool supports two modes: [*Import*](#import-command) and [*Export*](#export-command). It can support a single import/export of a single Platform or a list of Platforms using a .csv file.

## Usage
```powershell
Export-Import-Platform.ps1 -PVWAURL <string> -Export -PlatformID <string> -PlatformZipPath <string> [<CommonParameters>]

Export-Import-Platform.ps1 -PVWAURL <string> -ExportFile -ListFile <string> -PlatformZipPath <string> [<CommonParameters>]

Export-Import-Platform.ps1 -PVWAURL <string> -ExportActive -PlatformZipPath <string> [<CommonParameters>]

Export-Import-Platform.ps1 -PVWAURL <string> -ExportAll -PlatformZipPath <string> [<CommonParameters>]

Export-Import-Platform.ps1 -PVWAURL <string> -Import -PlatformZipPath <string> [<CommonParameters>]

Export-Import-Platform.ps1 -PVWAURL <string> -ImportFile -ListFile <string> [<CommonParameters>]
```


### Export Command:
```powershell
Export-Import-Platform.ps1 -Export -PVWAURL <PVWA URL> -PlatformID <Platform ID> -PlatformZipPath <The path to save the Platform ZIP output>
```
### ExportFile Command:
```powershell
Export-Import-Platform.ps1 -ExportFile -PVWAURL <PVWA URL> -ListFile <The path to the txt file with the PlatformID to export> -PlatformZipPath <The path to save the Platform ZIP output>
```

### ExportActive Command:
- During the export process a file named "_Export.txt" is created in the PlatformZipPath location. This file can be updated to only include the .zip files you wish to import and then leveraged by the `-ImportFile` command.
- Requires PVWA v11.1 or higher.

```powershell
Export-Import-Platform.ps1 -ExportActive -PVWAURL <PVWA URL> -PlatformZipPath <The path to save the Platform ZIP files>
```

### ExportAll Command:
- During the export process a file named "_Export.txt" is created in the PlatformZipPath location. This file can be updated to only include the .zip files you wish to import and then leveraged by the `-ImportFile` command.
- Requires PVWA v11.1 or higher.

```powershell
Export-Import-Platform.ps1 -ExportAll -PVWAURL <PVWA URL> -PlatformZipPath <The path to save the Platform ZIP files>
```

### Import Command:
```powershell
Export-Import-Platform.ps1 -Import -PVWAURL <PVWA URL> [-AuthType <string>] -PlatformZipPath <The path of the Platform ZIP to import> [<CommonParameters>]
Export-Import-Platform.ps1 -Import -PVWAURL <PVWA URL> [-AuthType <string>] -CSVPath <The path of the CSV for import> [<CommonParameters>]
```

### ImportFile Command:
```powershell
Export-Import-Platform.ps1 -ImportFile -PVWAURL <PVWA URL> -ListFile <The path to the txt file with the ZIP files to import>
```

## Examples
### Export Sample Platform
```powershell
Export-Import-Platform.ps1 -Export -PVWAURL https://PAS.mydomain.com/PasswordVault -PlatformID SamplePlatform -PlatformZipPath C:\Temp\
```

### ExportFile Sample Platform
```powershell
Export-Import-Platform.ps1 -Export -PVWAURL https://PAS.mydomain.com/PasswordVault -ListFile C:\Temp\ListFileExport.txt -PlatformZipPath C:\Temp\
```

### ExportActive Sample Platform
```powershell
Export-Import-Platform.ps1 -ExportActive -PVWAURL https://PAS.mydomain.com/PasswordVault -PlatformZipPath C:\Temp\
```

### ExportAll Sample Platform
```powershell
Export-Import-Platform.ps1 -ExportAll -PVWAURL https://PAS.mydomain.com/PasswordVault  -PlatformZipPath C:\Temp\
```

### Import Sample Platform
```powershell
Export-Import-Platform.ps1 -Import -PVWAURL https://PAS.mydomain.com/PasswordVault -PlatformZipPath C:\Temp\SamplePlatform.zip
```

```powershell
Export-Import-Platform.ps1 -ImportFile -PVWAURL https://PAS.mydomain.com/PasswordVault -ListFile C:\Temp\ListFileImport.txt
```

# Import Connection Component

Moved to folder named "Connection Component"

# Import Platform and Connection Component
## Main capabilities
- Import a Platform and a PSM Connection component and link them.
- Set the PSM Server ID for the new imported Platform.

## Usage
```powershell
Import-Platform-ConnectionComponent.ps1 [-PVWAURL] <string> -PlatformZipPath <string> -ConnectionComponentZipPath <string> [-PSMServerID] <string> [<CommonParameters>]
```

## Example
Import a sample Platform and connect it to a relevant sample PSM connection component using a custom PSM Server ID:
```powershell
Import-Platform-ConnectionComponent.ps1 -PVWAURL https://PAS.mydomain.com/PasswordVault -PlatformZipPath C:\Temp\SamplePlatform.zip -ConnectionComponentZipPath C:\Temp\SampleConnectionComponent.zip -PSMServerID PSMServer_MyPSMSRV
```

# Get Platform Details
## Usage
```powershell
Get-PlatformDetails.ps1 -PVWAURL <string> -PlatformID <string> [<CommonParameters>]
```

## Example
Get Windows Server Local Platform details:
```powershell
Get-PlatformDetails.ps1 -PVWAURL https://PAS.mydomain.com/PasswordVault -PlatformID WinServerLocal
```

# Platforms Report
- Creates a report on all target Platforms and their connection components.
- Produces a report of active target platforms by default.
- Supported version: PVWA 11.6 and above.

## Usage
```powershell
Get-PlatformReport.ps1 [-PVWAURL] <string> [[-AuthType] <string>] [[-CSVPath] <string>] [-ExtendedReport] [-IncludeInactive] [-DisableSSLVerify] [<CommonParameters>]
```

## Examples
Printing the report for all Active Platforms on screen:
```powershell
Get-PlatformReport.ps1 -PVWAURL https://PAS.mydomain.com/PasswordVault
```

Printing the extended report for all Platforms to a .csv file (including all connection components):
```powershell
Get-PlatformReport.ps1 -PVWAURL https://PAS.mydomain.com/PasswordVault -ExtendedReport -IncludeInactive -CSVPath "C:\CyberArk\Platforms\Active_Platforms_August-2020.csv"
```
