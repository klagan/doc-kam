# Usful commands

{{TOC}}

## Create a key pair

```
ssh-keygen -t rsa -b 4096
```

## Cache credentials locally

```
eval `ssh-agent -s`
ssh-add
```

## List local cached credentials

```
ssh-add -l
```

## Add key to remote machine
```
ssh-copy-id -i ~/.ssh/id_rsa.pub klagan@000.111.222.333 -p 22
```
> [source](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/use-remote-desktop)

## Upload SSH key into Azure key vault
```
az keyvault secret set --vault-name my-vault --name my-secret-key-name --file ~/desktop/id_rsa
```

## Download SSH key from Azure key vault
```
az keyvault secret download --vault-name my-vault --name my-secret-key-name --file ~/desktop/my-file
```

install docker and then add user to docker group on build box
```
 sudo usermod -a -G docker klagan
```
