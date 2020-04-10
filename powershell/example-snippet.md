# Example

Sample snippet exhibiting loops, json and `az`

**example json parameter**
```
{
"1": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"2": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"3": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"4": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",          
} 
```

**example appId parameter**
```
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

```
param(
    [parameter(mandatory=$true)][string]$json,
    [parameter(mandatory=$true)][string]$appId
  )

if (([string]::IsNullOrEmpty($json)))
{
    Write-Error "Endpoint json parameter is empty"
    Exit 1
}

if (([string]::IsNullOrEmpty($appId)))
{
    Write-Error "The app id parameter is empty"
    Exit 1
}

# Install-Module -Name AzureAD -Force 

$ids = $json | ConvertFrom-Json

foreach ($id in $ids.PsObject.Properties) {

    $id=$endpoint.Value
    $apiPermission=$(az ad app show --id "$($id)" --output tsv --query "oauth2Permissions[?value=='user_impersonation'].{id:id}")
    az ad app permission delete --id "$($appId)" --api "$($id)"
    az ad app permission add --id "$($appId)" --api "$($id)" --api-permissions "$($apiPermission)=Scope"
}

Write-Host "##vso[task.logissue type=warning]Must run the following commands manually to grant admin access"

Write-Host "az ad app permission admin-consent --id $($appId)"
```

## Example login

```
Install-Module -Name AzureAD -Force 

# should use service principal and not a user principal
$User = "$(my-upn)"
$PWord = ConvertTo-SecureString -String $(my-pwd) -AsPlainText -Force
$Credential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $User, $PWord
$response=(Connect-AzureAD -Credential $credential)

# ./run-script
```
