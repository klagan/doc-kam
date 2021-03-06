# Useful examples

### Set defaults for the devops extension

```
az devops configure --defaults organization=https://dev.azure.com/<organisation>/ project=<project-name>
```

> The formatting syntax is [jmespath](https://jmespath.org/). 

### Limit the properties that are returned

This command returns the display name as an alias of `customDisplayName`

```
az ad app show --id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --query "{customDisplayName:displayName}"
```

This command formats the results of an array.  The `[]` indicate the response is an array.

```
az ad app list --query "[].{displayName:displayName, appId:appId, objectId:objectId}
```

This command queries whether a reply url exist in the collection property `replyUrls` of an applciation

```
az ad app show --id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --query "length(replyUrls[?contains(@,'http://kam.comp')])"
```

This command queries whether the role `Reader` exists in the `appRoles` collection property of an applicaton.  It then returns only the `id` property of the result

```
az ad app show --id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --output json --query "appRoles[?value=='Reader'].{id:id}"
```

> Filters use the [odata](https://www.odata.org/) specification.  

This command queries all applications that have a `displayName` that `startswith` `my-app`
 
```
az ad app list --query "[].{appId:appId, displayName:displayName}" --filter "startswith(displayName, 'my-app')"
```

This command will retrieve all application registrations ending in 'api'
```
az ad app list --query "[?ends_with(displayName, 'api')].{displayName:displayName}" --all
```
This command will retrieve all application registrations starting in 'developer' and ending in 'api'
```
az ad app list --query "[?starts_with(displayName, 'developer')].{displayName:displayName} | [?ends_with(displayName, 'api')]" --all
```
This command creates projections by prefixing 'kam' to the webapp name.
```
az webapp list --query "[].{name:join('-', ['kam', name])}"
```
This command finds applications with the pattern `testclient` in.
```
searchTerm="testClient"
az ad app list --query "[?contains(displayName, '${searchTerm}')].{appId:appId, displayName:displayName}" --all --output table
```

This command lists attributes of the databases in a specific resource group
```
my_resource_group=my_group
my_sqlserver=my_sqlserver
az sql db list --resource-group $my_resource_group --server $my_sqlserver --query "[].{databaseId:databaseId, name:name, skuTier:currentSku.tier, skuSize:currentSku.size, skuCapacity:currentSku.capacity, skuName:currentSku.name, skuFamily:currentSku.family}" --output table
```

This command lists attributes of the appservice plans

```
az appservice plan list --query "[].{resourceGroup:resourceGroup, name:name, location:location, skuTier:sku.tier, skuSize:sku.size, skuCapacity:sku.capacity, skuName:sku.name, skuFamily:sku.family}" --output table
```

This command list the service principals starting with 'sample'

```
az ad sp list --filter "startswith(displayName, 'sample')"
```

This command lists specific attributes of the service principals starting with 'sample'

```
az ad sp list --query "[].{id:appId, tenant:appOwnerTenantId, name: appDisplayName, appId: appId}" --filter "startswith(displayName, 'sample')"
```

This command lists specific attributes of the resources in a tab separated values list

```
az resource list --query "[].{Name:Name, ResourceGroup:ResourceGroup, Location:Location, Type:Type, Status:Status}" --output tsv
```
