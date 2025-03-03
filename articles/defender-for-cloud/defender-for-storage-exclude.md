---
title: Microsoft Defender for Storage - excluding a storage account 
description: Excluding a specific storage account from a subscription with Microsoft Defender for Storage enabled.
ms.date: 01/16/2022
ms.topic: how-to
---
# Exclude a storage account from Microsoft Defender for Storage protections

> [!CAUTION]
> Excluding resources from advanced threat protection is not recommended and leaves your cloud workload exposed.

When you [enable Microsoft Defender for Storage](../storage/common/azure-defender-storage-configure.md#set-up-microsoft-defender-for-cloud) on a subscription, all existing Azure Storage accounts will be protected and any storage resources added to that subscription in the future will also be automatically protected.

If you need to exempt a specific Azure Storage account from this Defender plan, use the instructions on this page.

> [!TIP]
> We recommend enabling [Microsoft Defender for Resource Manager](defender-for-resource-manager-introduction.md) for any accounts with unprotected Azure Storage resources. Defender for Resource Manager automatically monitors your organization's resource management operations, whether they're performed through the Azure portal, Azure REST APIs, Azure CLI, or other Azure programmatic clients.


## Exclude a specific storage account 

To exclude specific storage accounts from Microsoft Defender for Storage when the plan is enabled on a subscription: 

### [**PowerShell**](#tab/enable-storage-protection-ps)

### Use PowerShell to exclude an Azure Storage account

1. If you don't have the Azure Az PowerShell module installed, install it using [the instructions from the Azure PowerShell documentation](/powershell/azure/install-az-ps).

1. Using an authenticated account, connect to Azure with the ``Connect-AzAccount`` cmdlet, as explained in [Sign in with Azure PowerShell](/powershell/azure/authenticate-azureps). 

1. Define the AzDefenderPlanAutoEnable tag on the storage account with the ``Update-AzTag`` cmdlet (replace the ResourceId with the resource ID of the relevant storage account):

    ```azurepowershell    
    Update-AzTag -ResourceId <resourceID> -Tag @{"AzDefenderPlanAutoEnable" = "off"} -Operation Merge 
    ```

    If you skip this stage, your untagged resources will continue receiving daily updates from the subscription level enablement policy. That policy will enable Defender for Storage again on the account.

    > [!TIP]
    > Learn more about tags in [Use tags to organize your Azure resources and management hierarchy](/azure/azure-resource-manager/management/tag-resources).

1. Disable Microsoft Defender for Storage for the desired account on the relevant subscription with the ``Disable-AzSecurityAdvancedThreatProtection`` cmdlet (using the same resource ID): 

    ```azurepowershell    
    Disable-AzSecurityAdvancedThreatProtection -ResourceId <resourceId> 
    ```

    [Learn more about this cmdlet](/powershell/module/az.security/disable-azsecurityadvancedthreatprotection).


### [**Azure CLI**](#tab/enable-storage-protection-cli)

### Use Azure CLI to exclude an Azure Storage account

1. If you don't have Azure CLI installed, install it using [the instructions from the Azure CLI documentation](/cli/azure/install-azure-cli).

1. Using an authenticated account, connect to Azure with the ``login`` command as explained in [Sign in with Azure CLI](/cli/azure/authenticate-azure-cli) and enter your account credentials when prompted:

    ```azurecli
    az login
    ```

1. Define the AzDefenderPlanAutoEnable tag on the storage account with the ``tag update`` command (replace the ResourceId with the resource ID of the relevant storage account):

    ```azurecli    
    az tag update --resource-id MyResourceId --operation merge --tags AzDefenderPlanAutoEnable=off
    ```

    If you skip this stage, your untagged resources will continue receiving daily updates from the subscription level enablement policy. That policy will enable Defender for Storage again on the account.

    > [!TIP]
    > Learn more about tags in [az tag](/cli/azure/tag).

1. Disable Microsoft Defender for Storage for the desired account on the relevant subscription with the ``security atp storage`` command (using the same resource ID): 

    ```azurecli    
    az security atp storage update --resource-group MyResourceGroup  --storage-account MyStorageAccount --is-enabled false 
    ```

    [Learn more about this command](/cli/azure/security/atp/storage).


### [**Azure portal**](#tab/enable-storage-protection-portal)

### Use the Azure portal to exclude an Azure Storage account

1. Define the AzDefenderPlanAutoEnable tag on the storage account:

    1. From the Azure portal, open the storage account and select the **Tags** page.
    1. Enter the tag name **AzDefenderPlanAutoEnable** and set the value to **off**.
    1. Select **Apply**.

    :::image type="content" source="media/defender-for-storage-exclude/define-tag-storage-account.png" alt-text="Screenshot of how to add a tag to a storage account in the Azure portal." lightbox="media/defender-for-storage-exclude/define-tag-storage-account.png":::
    
1. Verify that the tag has been added successfully. It should look similar to this:

    :::image type="content" source="media/defender-for-storage-exclude/define-tag-storage-account-success.png" alt-text="Screenshot of a tag on a storage account in the Azure portal." lightbox="media/defender-for-storage-exclude/define-tag-storage-account-success.png":::

1. Disable and then enable the Microsoft Defender for Storage on the subscription: 

    1. From the Azure portal, open **Microsoft Defender for Cloud**. 
    1. Open **Environment settings** > select the relevant subscription > **Defender plans** > toggle the Defender for Storage plan off > select **Save** > turn it back on > select **Save**. 

    :::image type="content" source="media/defender-for-storage-exclude/defender-plan-toggle.png" alt-text="Screenshot of disabling and enabling the Microsoft Defender for Storage plan from Microsoft Defender for Cloud." lightbox="media/defender-for-storage-exclude/defender-plan-toggle.png":::

---


## Exclude an Azure Databricks Storage account

When Defender for Storage is enabled on a subscription, it's not currently possible to exclude a Storage account if it belongs to an Azure Databricks workspace.

Instead, you can disable Defender for Storage on the subscription and enable Defender for Storage for each Azure Storage account from the **Security** page:

:::image type="content" source="media/defender-for-storage-exclude/defender-plan-enable-resource.png" alt-text="Screenshot of enabling Microsoft Defender for Storage from the security page of an Azure Storage account." lightbox="media/defender-for-storage-exclude/defender-plan-enable-resource.png":::


## Next steps

- Explore the [Microsoft Defender for Storage – Price Estimation Dashboard](https://techcommunity.microsoft.com/t5/microsoft-defender-for-cloud/microsoft-defender-for-storage-price-estimation-dashboard/ba-p/2429724)
