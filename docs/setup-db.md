# Creating Azure SQL Server with Private Endpoint

This guide shows how to create an Azure SQL Server, database and configure Private Endpoint access using Azure CLI.

**Important notes before you start:**

- Replace `SecurePassword123!` with a **strong, unique password**
- Never store passwords in scripts / git / documentation
- Use Azure Key Vault

## Create SQL Server

```powershell
az sql server create `
    --resource-group My3TierAppRG `
    --name My3TierSqlServer `
    --location eastus `
    --admin-user sqladmin `
    --admin-password SecurePassword123!`
```
## Create Database

```powershell
az sql db create `
--resource-group My3TierAppRG `
--server My3TierSqlServer `
--name MyAppDB `
--service-objective S0
```

**I chose the S0 tier, but in the real case you need to choose the S1-S12 or P1-P15 tier, depending on your tasks.**

## Configure Private Endpoint for Azure AQL

### Create Private DNS Zone

`az network private-dns zone create --resource-group My3TierAppRG --name privatelink.database.windows.net`

### Link the DNS Zone to VNet

```powershell
az network private-dns link vnet create `
    --resource-group My3TierAppRG `
    --zone-name privatelink.database.windows.net `
    --name MyDnsLink `
    --virtual-network My3TierVNet `
    --registration-enabled false`
```

### Create Private Endpoint

```powershell
az network private-endpoint create `
    --resource-group My3TierAppRG `
    --name SqlPrivateEndpoint `
    --vnet-name My3TierVNet `
    --subnet PrivateEndpointSubnet `
    --private-connection-resource-id $(az sql server show `
                                        --resource-group My3TierAppRG `
                                        --name My3TierSqlServer `
                                        --query id -o tsv) `
    --group-id sqlServer `
    --connection-name SqlConnection`
```

### Create A-record in Private DNS Zone

```powershell
az network private-dns record-set a create `
  --resource-group My3TierAppRG `
  --zone-name privatelink.database.windows.net `
  --name My3TierSqlServer
```
