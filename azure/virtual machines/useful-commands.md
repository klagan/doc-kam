# Useful commands

### Get list of storage image reference publisher
```
$locName = "uksouth"
Get-AzVMImagePublisher -Location $locName | Select PublisherName
```

### Get list of offers
```
$pubName="MicrosoftWindowsDesktop"
Get-AzVMImageOffer -Location $locName -PublisherName $pubName | Select Offer
```

### Get list of SKUs
```
$offerName="windows-10-1803-vhd-client-prod-stage"
Get-AzVMImageSku -Location $locName -PublisherName $pubName -Offer $offerName | Select Skus
```

### Get list of vm extensions
```
az vm extension image list --location uksouth -o table 
```

### Backing up a vm
[source](https://docs.microsoft.com/en-us/cli/azure/ext/vm-repair/vm/repair?view=azure-cli-latest)
```
az extension add -n vm-repair
az extension update -n vm-repair
az vm repair create -g sdt -n "<backup-vm-name>" --repair-username vmadmin --repair-password mypassword0123456789!
```