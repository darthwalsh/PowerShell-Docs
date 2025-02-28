---
external help file: PSModule-help.xml
Locale: en-US
Module Name: PowerShellGet
ms.date: 10/04/2021
online version: https://docs.microsoft.com/powershell/module/powershellget/get-installedscript?view=powershell-7.3&WT.mc_id=ps-gethelp
schema: 2.0.0
title: Get-InstalledScript
---
# Get-InstalledScript

## Synopsis
Gets an installed script.

## Syntax

```
Get-InstalledScript [[-Name] <String[]>] [-MinimumVersion <String>] [-RequiredVersion <String>]
 [-MaximumVersion <String>] [-AllowPrerelease] [<CommonParameters>]
```

## Description

The `Get-InstalledScript` cmdlet gets installed scripts for **CurrentUser** and **AllUsers** scopes.

## Examples

### Example 1: Get all installed scripts

```powershell
Get-InstalledScript
```

This command gets all installed scripts.

### Example 2: Get installed scripts by name

```powershell
Get-InstalledScript -Name "Required-Scri*"
```

```Output
Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Required-Script1                    Script     local1               Description for the Required-Script1 script
2.5        Required-Script2                    Script     local1               Description for the Required-Script2 script
2.5        Required-Script3                    Script     local1               Description for the Required-Script3 script
```

This command gets scripts where the name begins with **Required-Scri**.

## Parameters

### -AllowPrerelease

Includes in the results scripts marked as a prerelease.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -MaximumVersion

Specifies the maximum, or latest, version of a script to get. The **MaximumVersion** and
**RequiredVersion** parameters are mutually exclusive; you cannot use both parameters in the same
command.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -MinimumVersion

Specifies the minimum version of a script to get. The **MinimumVersion** and **RequiredVersion**
parameters are mutually exclusive; you cannot use both parameters in the same command.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name

Specifies an array of names of scripts to get. Wildcards are accepted.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -RequiredVersion

Specifies the exact version of a script to get.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## Inputs

### System.String[]

### System.String

## Outputs

### System.Object

## Notes

## Related links

[Install-Script](Install-Script.md)

[Uninstall-Script](Uninstall-Script.md)
