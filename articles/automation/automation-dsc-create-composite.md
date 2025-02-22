---
title: Convert configurations to composite resources for Azure Automation State Configuration
description: This article tells how to convert configurations to composite resources for Azure Automation State Configuration.
keywords: dsc,powershell,configuration,setup
services: automation
ms.subservice: dsc
ms.date: 08/08/2019
ms.topic: conceptual
---

# Convert configurations to composite resources

> Applies To: Windows PowerShell 5.1

Once you get started authoring configurations,
you can quickly create "scenarios" that manage
groups of settings.
Examples would be:

- create a web server
- create a DNS server
- create a server that runs SharePoint
- configure a SQL cluster
- manage firewall settings
- manage password settings

If you are interested in sharing this work with others,
the best option is to package the configuration as a
[Composite Resource](/powershell/scripting/dsc/resources/authoringresourcecomposite).
Creating composite resources for the first time can be overwhelming.

> [!NOTE]
> This article refers to a solution that is maintained by the Open Source community.
> Support is only available in the form of GitHub collaboration, not from Microsoft.

## Community project: CompositeResource

A community maintained solution named
[CompositeResource](https://github.com/microsoft/compositeresource)
has been created to resolve this challenge.

CompositeResource automates the process of creating a new module from your configuration.
You start by
[dot sourcing](https://devblogs.microsoft.com/scripting/how-to-reuse-windows-powershell-functions-in-scripts/)
the configuration script on your workstation (or build server)
so it is loaded in memory.
Next, rather than running the configuration to generate a MOF file,
use the function provided by the CompositeResource module to automate a conversion.
The cmdlet will load the contents of your configuration,
get the list of parameters,
and generate a new module with everything you need.

Once you have generated a module,
you can increment the version and add release notes each time you make changes
and publish it to your own
[PowerShellGet repository](https://powershellexplained.com/2018-03-03-Powershell-Using-a-NuGet-server-for-a-PSRepository/?utm_source=blog&utm_medium=blog&utm_content=psscriptrepo).

Once you have created a composite resource module containing your configuration
(or multiple configurations),
you can use them in the
[Composable Authoring Experience](./compose-configurationwithcompositeresources.md)
in Azure,
or add them to 
[DSC Configuration scripts](/powershell/scripting/dsc/configurations/configurations)
to generate MOF files
and
[upload the MOF files to Azure Automation](./tutorial-configure-servers-desired-state.md#create-and-upload-a-configuration-to-azure-automation).
Then register your servers from either
[on-premises](./automation-dsc-onboarding.md#enable-physicalvirtual-linux-machines)
or [in Azure](./automation-dsc-onboarding.md#enable-azure-vms)
to pull configurations.
The latest update to the project has also published
[runbooks](https://www.powershellgallery.com/packages?q=DscGallerySamples)
for Azure Automation to automate the process of importing configurations
from the PowerShell Gallery.

To try out automating creation of composite resources for DSC, visit the
[PowerShell Gallery](https://www.powershellgallery.com/packages/compositeresource/)
and download the solution or click "Project Site"
to view the
[documentation](https://github.com/microsoft/compositeresource).

## Next steps

- To understand PowerShell DSC, see [Windows PowerShell Desired State Configuration overview](/powershell/scripting/dsc/overview/overview).
- Find out about PowerShell DSC resources in [DSC Resources](/powershell/scripting/dsc/resources/resources).
- For details of Local Configuration Manager configuration, see [Configuring the Local Configuration Manager](/powershell/scripting/dsc/managing-nodes/metaconfig).
