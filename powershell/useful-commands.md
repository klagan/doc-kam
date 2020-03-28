# Useful commands

### Elevate execution policy
```
Set-ExecutionPolicy Bypass -Scope Process
```

## Write-XXX

`Write-Host` directly to the console, not included in function/cmdlet output. Allows foreground and background colour to be set.

`Write-Debug` directly to the console, if $DebugPreference set to Continue or Stop.

`Write-Verbose` Write directly to the console, if $VerbosePreference set to Continue or Stop.

### Test network connection

```
nc google.com -port 80
```

### List environment variables
```
gci env:* | sort-object name
```