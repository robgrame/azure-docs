---
title: Configure virtual network integration with application routing.
description: This how-to article will walk you through configure app routing on a regional VNet integration.
author: madsd
ms.author: madsd
ms.topic: how-to
ms.date: 10/20/2021
---

# Manage Azure App Service virtual network integration routing

When configuring application routing, you can either route all traffic or only private traffic (also known as [RFC1918](https://datatracker.ietf.org/doc/html/rfc1918#section-3) traffic) into your Azure virtual network (VNet). This how-to article will describe how to configure application routing.

## Prerequisites

Your app is already integrated using the regional VNet integration feature.

## Configure in the Azure portal

You can use the following steps to disable Route All in your app through the portal: 

:::image type="content" source="./media/configure-vnet-integration-routing/vnetint-route-all-enabled.png" alt-text="Route All enabled":::

1. Go to the **Networking** > **VNet integration** UI in your app portal.
1. Set **Route All** to Disabled.
    
    :::image type="content" source="./media/configure-vnet-integration-routing/vnetint-route-all-disabling.png" alt-text="Disable Route All":::

1. Select **Yes** to confirm.

## Configure with Azure CLI

You can also configure Route All using Azure CLI (the minimum `az version` required is 2.27.0):

```azurecli-interactive
az webapp config set --resource-group <group-name> --name <app-name> --vnet-route-all-enabled [true|false]
```

## Configure with Azure PowerShell

```azurepowershell
# Parameters
$siteName = '<app-name>'
$resourceGroupName = '<group-name>'

# Configure VNet Integration
$webApp = Get-AzResource -ResourceType Microsoft.Web/sites -ResourceGroupName $resourceGroupName -ResourceName $siteName
Set-AzResource -ResourceId ($webApp.Id + "/config/web") -Properties @{ vnetRouteAllEnabled = $true } -Force
```

## Next steps

- [Enable VNet integration](./configure-vnet-integration-enable.md)
- [General Networking overview](./networking-features.md)