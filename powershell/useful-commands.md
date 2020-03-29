# Useful commands

### Elevate execution policy
```
Set-ExecutionPolicy Bypass -Scope Process
```

## Write-XXX

`Write-Host` directly to the console, not included in function/cmdlet output. Allows foreground and background colour to be set.

`Write-Debug` directly to the console, if $DebugPreference set to Continue or Stop.

`Write-Verbose` Write directly to the console, if $VerbosePreference set to Continue or Stop.

`Write-Information` Uses the `$InformationPreference` flag to determine how to handle the message.  `Write-Host` is a wrapper for this call. [(source)](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/write-information?view=powershell-7#parameters)

### Test network connection

```
nc google.com -port 80
```

### List environment variables
```
gci env:* | sort-object name
```

### Connect to Azure AD
> [source](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-credential?view=powershell-7#examples)
```
$User = "Domain01\User01"
$PWord = ConvertTo-SecureString -String "P@sSwOrd" -AsPlainText -Force
$Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $PWord
```
