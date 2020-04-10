# Example

This sample contains loops, json manipulation and `az` command

**example json parameter**
```
{
"1": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"2": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"3": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"4": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",          
}  
```

**example app id parameter**
````
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

**code snippet**
```
if [ $# -ne 2 ]; then
    echo "ERROR: [Incorrect arguments provided"]
    echo -e "eg: ${0} <json> <application-id>\n"
    exit 1
fi

json=$1
appId=$2

for destAppId in $(echo "${json}" | jq -r '.[] | values'); 
do   
    echo $destAppId
    echo "Provisioning ${appId} permission to ${destAppId} api"
    
    apiPermission=$(az ad app show --id "${destAppId}" --output tsv --query "oauth2Permissions[?value=='user_impersonation'].{id:id}")
    # apiRolePermission=$(az ad app show --id $destAppId --output tsv --query "appRoles[?value=='My.Role'].{id:id}")
   
    az ad app permission delete --id "${appId}" --api "${destAppId}"
    az ad app permission add --id "${appId}" --api "${destAppId}" --api-permissions "${apiPermission}=Scope"
    # az ad app permission add --id "${appId}" --api "${destAppId}" --api-permissions "${apiRolePermission}=Role"
done

echo "##vso[task.logissue type=warning]Must run the following commands manually to grant admin access"

echo "az ad app permission admin-consent --id ${appId}"

```
