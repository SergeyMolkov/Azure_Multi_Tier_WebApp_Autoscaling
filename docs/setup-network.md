# Network Setup

## Introduction

For security purposes, we will configure a Virtual Network (VNet) with subnets for AKS, App Service, and SQL. Private Endpoints will ensure private access.

## Creating VNet

`az network vnet create -g "My3TierAppRG" -n "My3TierVNet" --address-prefix "10.0.0.0/16" --location eastus`

## Creating Subnets

### For App Service (Frontend)

`az network vnet subnet create --resource-group My3TierAppRG --vnet-name My3TierVNet -n AppServiceSubnet --address-prefixes 10.0.2.0/24`

### For AKS (Backend)
`az network vnet subnet create --resource-group My3TierAppRG --vnet-name My3TierVNet --name AKSSubnet --address-prefixes 10.0.1.0/24`

### For Private Endpoints (SQL)

`az network vnet subnet create --resource-group My3TierAppRG --vnet-name My3TierVNet --name PrivateEndpointSubnet --address-prefixes 10.0.3.0/24 --private-endpoint-network-policies Disabled`

Explanation: This command disables network policies for private endpoints.

