---
title: Tutorial to prepare Azure portal, datacenter environment to deploy Azure Stack Edge Pro GPU | Microsoft Docs
description: The first tutorial about deploying Azure Stack Edge Pro GPU involves preparing the Azure portal.
services: databox
author: alkohli

ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 12/20/2021
ms.author: alkohli
# Customer intent: As an IT admin, I need to understand how to prepare the portal to deploy Azure Stack Edge Pro so I can use it to transfer data to Azure. 
---
# Tutorial: Prepare to deploy Azure Stack Edge Pro with GPU 

This tutorial is the first in the series of deployment tutorials that are required to completely deploy Azure Stack Edge Pro with GPU. This tutorial describes how to prepare the Azure portal to deploy an Azure Stack Edge resource.

You need administrator privileges to complete the setup and configuration process. The portal preparation takes less than 10 minutes.

In this tutorial, you learn how to:

> [!div class="checklist"]
> * Create a new resource
> * Get the activation key

### Get started

For Azure Stack Edge Pro deployment, you need to first prepare your environment. Once the environment is ready, follow the required steps and if needed, optional steps and procedures to fully deploy the device. The step-by-step deployment instructions indicate when you should perform each of these required and optional steps.

| Step | Description |
| --- | --- |
| **Preparation** |These steps must be completed in preparation for the upcoming deployment. |
| **[Deployment configuration checklist](#deployment-configuration-checklist)** |Use this checklist to gather and record information before and during the deployment. |
| **[Deployment prerequisites](#prerequisites)** |These prerequisites validate that the environment is ready for deployment. |
|  | |
|**Deployment tutorials** |These tutorials are required to deploy your Azure Stack Edge Pro device in production. |
|**[1. Prepare the Azure portal for Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-prep.md)** |Create and configure your Azure Stack Edge resource before you install an Azure Stack Box Edge physical device. |
|**[2. Install Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-install.md)**|Unpack, rack, and cable the Azure Stack Edge Pro physical device.  |
|**[3. Connect to Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-connect.md)** |Once the device is installed, connect to device local web UI.  |
|**[4. Configure network settings for Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-configure-network-compute-web-proxy.md)** |Configure network including the compute network and web proxy settings for your device.   |
|**[5. Configure device settings for Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-set-up-device-update-time.md)** |Assign a device name and DNS domain, configure update server and device time. |
|**[6. Configure security settings for Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-configure-certificates.md)** |Configure certificates for your device. Use device-generated certificates or bring your own certificates.   |
|**[7. Activate Azure Stack Edge Pro](azure-stack-edge-gpu-deploy-activate.md)** |Use the activation key from service to activate the device. The device is ready to set up SMB or NFS shares or connect via REST. |
|**[8. Configure compute](azure-stack-edge-gpu-deploy-configure-compute.md)** |Configure the compute role on your device. A Kubernetes cluster is also created. |
|**[9A. Transfer data with Edge shares](./azure-stack-edge-gpu-deploy-add-shares.md)** |Add shares and connect to shares via SMB or NFS. |
|**[9B. Transfer data with Edge storage accounts](./azure-stack-edge-gpu-deploy-add-storage-accounts.md)** |Add storage accounts and connect to blob storage via REST APIs. |


You can now begin to gather information regarding the software configuration for your Azure Stack Edge Pro device.

## Deployment configuration checklist

Before you deploy your device, you need to collect information to configure the software on your Azure Stack Edge Pro device. Preparing some of this information ahead of time helps streamline the process of deploying the device in your environment. Use the [Azure Stack Edge Pro deployment configuration checklist](azure-stack-edge-gpu-deploy-checklist.md) to note down the configuration details as you deploy your device.


## Prerequisites

Following are the configuration prerequisites for your Azure Stack Edge resource, your Azure Stack Edge Pro device, and the datacenter network.

### For the Azure Stack Edge resource

Before you begin, make sure that:

- Your Microsoft Azure subscription is enabled for an Azure Stack Edge resource. Make sure that you used a supported subscription such as [Microsoft Enterprise Agreement (EA)](https://azure.microsoft.com/overview/sales-number/), [Cloud Solution Provider (CSP)](/partner-center/azure-plan-lp), or [Microsoft Azure Sponsorship](https://azure.microsoft.com/offers/ms-azr-0036p/). Pay-as-you-go subscriptions aren't supported. To identify the type of Azure subscription you have, see [What is an Azure offer?](../cost-management-billing/manage/switch-azure-offer.md#what-is-an-azure-offer).
- You have owner or contributor access at resource group level for the Azure Stack Edge Pro, IoT Hub, and Azure Storage resources.

    - To create any Azure Stack Edge resource, you should have permissions as a contributor (or higher) scoped at resource group level. 
    - You also need to make sure that the `Microsoft.DataBoxEdge` and `Microsoft.KeyVault` resource providers are registered. To create any IoT Hub resource, `Microsoft.Devices` provider should be registered. 
        - To register a resource provider, in the Azure portal, go to **Home > Subscriptions > Your-subscription > Resource providers**. 
        - Search for the specific resource provider, for example, `Microsoft.DataBoxEdge`, and register the resource provider. 
    - To create a Storage account resource, again you need contributor or higher access scoped at the resource group level. Azure Storage is by default a registered resource provider.
- To create an order in the Azure Edge Hardware Center, you need to make sure that the `Microsoft.EdgeOrder` provider is registered. For information on how to register, go to [Register resource provider](azure-stack-edge-gpu-manage-access-power-connectivity-mode.md#register-resource-providers).
- You have admin or user access to Azure Active Directory Graph API for generating activation key or credential operations such as share creation that uses a storage account. For more information, see [Azure Active Directory Graph API](/previous-versions/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes#default-access-for-administrators-users-and-guest-users-).

### For the Azure Stack Edge Pro device

Before you deploy a physical device, make sure that:

- You've reviewed the safety information that was included in the shipment package.
- You have a 1U slot available in a standard 19" rack in your datacenter for rack mounting the device.
- You have access to a flat, stable, and level work surface where the device can rest safely.
- The site where you intend to set up the device has standard AC power from an independent source or a rack power distribution unit (PDU) with an uninterruptible power supply (UPS).
- You have access to a physical device.


### For the datacenter network

Before you begin, make sure that:

- The network in your datacenter is configured per the networking requirements for your Azure Stack Edge Pro device. For more information, see [Azure Stack Edge Pro System Requirements](azure-stack-edge-system-requirements.md).

- For normal operating conditions of your Azure Stack Edge Pro, you have:

    - A minimum of 10-Mbps download bandwidth to ensure the device stays updated.
    - A minimum of 20-Mbps dedicated upload and download bandwidth to transfer files.

## Create a new resource

If you have an existing Azure Stack Edge resource to manage your physical device, skip this step and go to [Get the activation key](#get-the-activation-key).

### Create an order resource

To create an order resource, use the Azure Edge Hardware Center. [Azure Edge Hardware Center](../azure-edge-hardware-center/azure-edge-hardware-center-overview.md) lets you explore and order a variety of hardware from the Azure hybrid portfolio including Azure Stack Edge Pro devices.

When you place an order through the Edge Hardware Center, you can order multiple devices, to be shipped to more than one address, and you can reuse ship to addresses from other orders.

Ordering through Edge Hardware Center will create an Azure resource that will contain all your order-related information. One resource each will be created for each of the units ordered. You will have to create an Azure Stack Edge resource after you receive the device to activate and manage it.

[!INCLUDE [Create order in Azure Edge Hardware Center](../../includes/azure-edge-hardware-center-new-order.md)]

### Create a management resource for each device

[!INCLUDE [Create management resource](../../includes/azure-edge-hardware-center-create-management-resource.md)]

<!--### [Azure CLI](#tab/azure-cli)

If necessary, prepare your environment for Azure CLI.

[!INCLUDE [azure-cli-prepare-your-environment-no-header.md](../../includes/azure-cli-prepare-your-environment-no-header.md)]

To create an Azure Stack Edge resource, run the following commands in Azure CLI.

1. Create a resource group by using the [az group create](/cli/azure/group#az_group_create) command, or use an existing resource group:

   ```azurecli
   az group create --name myasepgpu1 --location eastus
   ```

1. To create a device, use the [az databoxedge device create](/cli/azure/databoxedge/device#az_databoxedge_device_create) command:

   ```azurecli
   az databoxedge device create --resource-group myasepgpu1 \
      --device-name myasegpu1 --location eastus --sku EdgeP_Base
   ```

   Choose a location closest to the geographical region where you want to deploy your device. The region stores only the metadata for device management. The actual data can be stored in any storage account.

   For a list of all the regions where the Azure Stack Edge resource is available, see [Azure products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=databox&regions=all). If using Azure Government, all the government regions are available as shown in the [Azure regions](https://azure.microsoft.com/global-infrastructure/regions/).

1. To create an order, run the [az databoxedge order create](/cli/azure/databoxedge/order#az_databoxedge_order_create) command:

   ```azurecli 
   az databoxedge order create --resource-group myasepgpu1 \
      --device-name myasegpu1 --company-name "Contoso" \
      --address-line1 "1020 Enterprise Way" --city "Sunnyvale" \
      --state "California" --country "United States" --postal-code 94089 \
      --contact-person "Gus Poland" --email-list gus@contoso.com --phone 4085555555
   ```

The resource creation takes a few minutes. Run the [az databoxedge order show](/cli/azure/databoxedge/order#az_databoxedge_order_show) command to see the order:

```azurecli
az databoxedge order show --resource-group myasepgpu1 --device-name myasegpu1 
```

After you place an order, Microsoft reviews the order and contacts you by email with shipping details.-->

---

## Get the activation key

After the Azure Stack Edge resource is up and running, you'll need to get the activation key. This key is used to activate and connect your Azure Stack Edge Pro device with the resource. You can get this key now while you are in the Azure portal.

1. Select the resource you created, and select **Overview**.

2. In the right pane, enter a name for the Azure Key Vault or accept the default name. The key vault name can be between 3 and 24 characters.

   A key vault is created for each Azure Stack Edge resource that is activated with your device. The key vault lets you store and access secrets, for example, the Channel Integrity Key (CIK) for the service is stored in the key vault. 

   Once you've specified a key vault name, select **Generate key** to create an activation key. 

   ![Screenshot of the Overview pane for a newly created Azure Stack Edge resource. The Generate Activation Key button is highlighted.](media/azure-stack-edge-gpu-deploy-prep/azure-stack-edge-resource-3.png)

   Wait a few minutes while the key vault and activation key are created. Select the copy icon to copy the key and save it for later use.


> [!IMPORTANT]
> - The activation key expires three days after it is generated.
> - If the key has expired, generate a new key. The older key is not valid.

## Next steps

In this tutorial, you learned about Azure Stack Edge Pro topics such as:

> [!div class="checklist"]
> * Create a new resource
> * Get the activation key

Advance to the next tutorial to learn how to install Azure Stack Edge Pro.

> [!div class="nextstepaction"]
> [Install Azure Stack Edge Pro](./azure-stack-edge-gpu-deploy-install.md)
