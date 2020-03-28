# Useful commands

---

## Useful syntax

Run a command: `az ad app list`
Run a command and store the result: `result=$(az ad app list)`

---


### Add/remove a reply url

```
az ad app update --id xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx --add replyUrls "http://kam.com"
```

```
az ad app update --id xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx --remove replyUrls "http://kam.com"
```

## Application roles

### Find an application role

```
az ad app show --id <API-APPLICATION-ID> --output tsv --query "appRoles[?value=='God.Level'].{id:id}"
```

### Add an application role to an application client

```
az ad app permission add --id <TARGET-APPLICATION-ID> --api <SOURCE-APPLICATION-ID> --api-permissions <APPLICATION-ROLE-ID>=Role
```

### get a list of all applications

```azurecli
az rest --method get --uri https://graph.microsoft.com/v1.0/applications
```

### get the [appRoles] property of an application(use object id and NOT application id like the documentation says)

```azurecli
az rest --method get --uri https://graph.microsoft.com/v1.0/applications/<application-object-id>?$select=appRoles --query {appRoles:appRoles}
```

### update application property

```azurecli
az rest --method patch --uri https://graph.microsoft.com/v1.0/applications/{application-object-id} --body @<filename>
```

*Example filename*

```json
{
    "propertyName" : {}
}
```
