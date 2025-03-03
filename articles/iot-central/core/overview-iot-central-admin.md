---
title: Azure IoT Central administrator guide
description: Azure IoT Central is an IoT application platform that simplifies the creation of IoT solutions. This article provides an overview of the administrator role in IoT Central. 
author: dominicbetts 
ms.author: dobett 
ms.date: 12/22/2021
ms.topic: conceptual
ms.service: iot-central
services: iot-central
ms.custom: mvc

# This article applies to administrators.
---

# IoT Central administrator guide

An IoT Central application lets you monitor and manage millions of devices throughout their life cycle. This guide is for administrators who manage IoT Central applications.

In IoT Central, an administrator:

- Manages users and roles in the application.
- Creates and manages organizations.
- Manages security such as device authentication.
- Configures application settings.
- Upgrades applications.
- Exports and shares applications.
- Monitors application health.

## Users and roles

IoT Central uses a role-based access control system to manage user permissions within an application. IoT Central has three built-in roles for administrators, solution builders, and operators. An administrator can create custom roles with specific sets of permissions. An administrator is responsible for adding users to an application and assigning them to roles.

To learn more, see [Manage users and roles in your IoT Central application](howto-manage-users-roles.md).

## Organizations

Organizations let you define a hierarchy that you use to manage which users can see which devices in your IoT Central application. The user's role determines their permissions over the devices they see, and the experiences they can access.

To learn more, see [Create an IoT Central organization](howto-create-organizations.md).

## Application security

Devices that connect to your IoT Central application typically use X.509 certificates or shared access signatures (SAS) as credentials. The administrator manages the group certificates or keys that the device credentials are derived from.

To learn more, see [X.509 group enrollment](concepts-get-connected.md#x509-group-enrollment), [SAS group enrollment](concepts-get-connected.md#sas-group-enrollment), and [How to roll X.509 device certificates](how-to-connect-devices-x509.md).

The administrator can also create and manage the API tokens that a client application uses to authenticate with your IoT Central application. Client applications use the REST API to interact with IoT Central.

For data exports, the administrator can configure [managed identities](../../active-directory/managed-identities-azure-resources/overview.md) to secure the connections to the [export destinations](howto-export-data.md). To learn more, see:

- [Configure a managed identity (Azure portal)](howto-manage-iot-central-from-portal.md#configure-a-managed-identity)
- [Configure a managed identity (REST API)](howto-manage-iot-central-with-rest-api.md)
- [Configure a managed identity (Azure CLI)](howto-manage-iot-central-from-cli.md#configure-a-managed-identity)

## Configure an application

The administrator can configure the behavior and appearance of an IoT Central application. To learn more, see:

- [Change application name and URL](howto-administer.md#change-application-name-and-url)
- [Customize the UI](howto-customize-ui.md)
- [Move an application to a different pricing plans](howto-faq.yml#how-do-i-move-from-a-free-to-a-standard-pricing-plan-)
- [Configure file uploads](howto-configure-file-uploads.md)

## Export an application

An administrator can:

- Create a copy of an application if you just need a duplicate copy of your application. For example, you may need a duplicate copy for testing.
- Create an application template from an existing application if you plan to create multiple copies.

To learn more, see [Create and use a custom application template](howto-create-iot-central-application.md#create-and-use-a-custom-application-template) .

## Migrate to a new version

An administrator can migrate an application to a newer version. Currently, a newly created application is a V3 application. An administrator may need to migrate a V2 application to a V3 application.

To learn more, see [Migrate your V2 IoT Central application to V3](howto-migrate.md).

## Monitor application health

An administrator can use IoT Central metrics to assess the health of connected devices and the health of running data exports.

To view the metrics, an administrator can use charts in the Azure portal, a REST API, or PowerShell or Azure CLI queries.

To learn more, see [Monitor application health](howto-manage-iot-central-from-portal.md#monitor-application-health).

## Monitor connected IoT Edge devices

To learn how to remotely monitor your IoT Edge fleet using Azure Monitor and built-in metrics integration, see [Collect and transport metrics](../../iot-edge/how-to-collect-and-transport-metrics.md).

## Tools

Many of the tools you use as an administrator are available in the **Administration** section of each IoT Central application. You can also use the following tools to complete some administrative tasks:

- [Azure command line](howto-manage-iot-central-from-cli.md)
- [Azure portal](howto-manage-iot-central-from-portal.md)

## Next steps

Now that you've learned about how to administer your Azure IoT Central application, the suggested next step is to learn about [Manage users and roles](howto-manage-users-roles.md) in Azure IoT Central.
