
Este repositório contém cmdlets do PowerShell para desenvolvedores e administradores desenvolverem, implantarem,
administrar e gerenciar recursos do Microsoft Azure.

O módulo Az PowerShell está pré-instalado em [Azure Cloud Shell][AzureCloudShell].

## Modulos

A tabela a seguir contém uma lista dos módulos cumulativos do Azure PowerShell.

Description       | Module Name  | PowerShell Gallery Link
----------------- | ------------ | -----------------------
Azure PowerShell  | `Az`         | [![Az]][AzGallery]
Azure PowerShell with preview modules | `AzPreview`                             | [![AzPreview]][AzPreviewGallery]

Para a lista completa de módulos segue o link:
[Azure PowerShell Modules][AzurePowerShellModules].

## Instalação

### PowerShell Galeria

Execute o seguinte comando numa sessão PowerShell para instalar o módulo Az PowerShell:

```powershell
Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
```

The `Az` module replaces `AzureRM`. You should not install `Az` side-by-side with `AzureRM`.

Se você tiver uma versão anterior do módulo Azure PowerShell instalada na Galeria do PowerShell
e gostaria de atualizar para a versão mais recente, execute o seguinte comando em uma sessão do PowerShell:

```powershell
Update-Module -Name Az -Scope CurrentUser -Force
```

`Update-Module` instala a nova versão lado a lado com as versões anteriores. Não desinstala
as versões anteriores.

Para mais informações de instalação:
[installation guide][InstallationGuide].

## Uso

### Log into Azure

To connect to Azure, use the [`Connect-AzAccount`][ConnectAzAccount] cmdlet:

```powershell
# Opens a new browser window to log into your Azure account.
Connect-AzAccount

# Log in with a previously created service principal. Use the application ID as the username, and the secret as password.
$Credential = Get-Credential
Connect-AzAccount -ServicePrincipal -Credential $Credential -TenantId $TenantId
```

To log into a specific cloud (_AzureChinaCloud_, _AzureCloud_, _AzureUSGovernment_), use the
`Environment` parameter:

```powershell
# Log into a specific cloud, for example the Azure China cloud.
Connect-AzAccount -Environment AzureChinaCloud
```

### Session context

Um contexto de sessão persiste informações de login nos módulos do Azure PowerShell e no PowerShell
instâncias. Use the [`Get-AzContext`][GetAzContext] cmdlet para visualizar o contexto que você está usando no
sessão atual. Os resultados contêm o inquilino e a subscrição do Azure.

```powershell
# Get the Azure PowerShell context for the current PowerShell session
Get-AzContext

# Lists all available Azure PowerShell contexts in the current PowerShell session
Get-AzContext -ListAvailable
```

To get the subscriptions in a tenant, use the [`Get-AzSubscription`][GetAzSubscription] cmdlet:

```powershell
# Get all of the Azure subscriptions in your current Azure tenant
Get-AzSubscription

# Get all of the Azure subscriptions in a specific Azure tenant
Get-AzSubscription -TenantId $TenantId
```

To change the subscription that you are using for your current context, use the
[`Set-AzContext`][SetAzContext] cmdlet:

```powershell
# Set the Azure PowerShell context to a specific Azure subscription
Set-AzContext -Subscription $SubscriptionName -Name 'MyContext'

# Set the Azure PowerShell context using piping
Get-AzSubscription -SubscriptionName $SubscriptionName | Set-AzContext -Name 'MyContext'
```

For details on Azure PowerShell contexts, see [Azure PowerShell context objects][PersistedCredentialsGuide].

### Discovering cmdlets

Use `Get-Command` para descobrir cmdlets dentro de um módulo específico ou cmdlets que seguem um módulo específico
padrão de pesquisa:

```powershell
# List all cmdlets in the Az.Accounts module
Get-Command -Module Az.Accounts

# List all cmdlets that contain VirtualNetwork in their name
Get-Command -Name '*VirtualNetwork*'

# List all cmdlets that contain VM in their name in the Az.Compute module
Get-Command -Module Az.Compute -Name '*VM*'
```

### Cmdlet Exemplos e ajuda:

Para visualizar o conteúdo de ajuda de um cmdlet, use o cmdlet `Get-Help`:

```powershell
# View basic help information for Get-AzSubscription
Get-Help -Name Get-AzSubscription

# View the examples for Get-AzSubscription
Get-Help -Name Get-AzSubscription -Examples

# View the full help for Get-AzSubscription
Get-Help -Name Get-AzSubscription -Full

# View the online version of the help from https://learn.microsoft.com for Get-AzSubscription
Get-Help -Name Get-AzSubscription -Online
```

Para obter instruções detalhadas sobre como usar o Azure PowerShell, consulte o [getting started guide][GettingStartedGuide].


## Leia Mais

* [Microsoft Azure Documentation][MicrosoftAzureDocs]
* [PowerShell Documentation][PowerShellDocs]

---

<!-- References -->

<!-- Local -->
[GitHubRepo]: https://github.com/Azure/azure-powershell/issues

[Contributing]: CONTRIBUTING.md

[AzureIcon]: documentation/images/MicrosoftAzure-32px.png
[PowershellIcon]: documentation/images/MicrosoftPowerShellCore-32px.png
[AzurePowerShellModules]: documentation/azure-powershell-modules.md
[DeveloperGuide]: documentation/development-docs/azure-powershell-developer-guide.md

<!-- External -->
[Az]: https://img.shields.io/powershellgallery/v/Az.svg?style=flat-square&label=Az
[AzPreview]: https://img.shields.io/powershellgallery/v/AzPreview.svg?style=flat-square&label=AzPreview
[AzGallery]: https://www.powershellgallery.com/packages/Az/
[AzPreviewGallery]: https://www.powershellgallery.com/packages/AzPreview/

[DotNetFramework]: https://dotnet.microsoft.com/download/dotnet-framework-runtime
[PowerShellCore]: https://github.com/PowerShell/PowerShell/releases/latest

[ContributionGuidelines]: https://opensource.microsoft.com/collaborate/
[CodeOfConduct]: https://opensource.microsoft.com/codeofconduct/
[CodeOfConductFaq]: https://opensource.microsoft.com/codeofconduct/faq/
[OpenCodeEmail]: mailto:opencode@microsoft.com

[AzureCloudShell]: https://shell.azure.com/
[AzureCommunitySupport]: https://azure.microsoft.com/support/community/
[PrivacyStatement]: https://privacy.microsoft.com/privacystatement

<!-- Docs -->
[MicrosoftAzureDocs]: https://learn.microsoft.com/azure/
[PowerShellDocs]: https://learn.microsoft.com/powershell/

[InstallationGuide]: https://learn.microsoft.com/powershell/azure/install-az-ps
[GettingStartedGuide]: https://learn.microsoft.com/powershell/azure/get-started-azureps
[PersistedCredentialsGuide]: https://learn.microsoft.com/powershell/azure/context-persistence

[ConnectAzAccount]: https://learn.microsoft.com/powershell/module/az.accounts/connect-azaccount
[GetAzContext]: https://learn.microsoft.com/powershell/module/az.accounts/get-azcontext
[GetAzSubscription]: https://learn.microsoft.com/powershell/module/az.accounts/get-azsubscription
[SetAzContext]: https://learn.microsoft.com/powershell/module/az.accounts/set-azcontext
[SendFeedback]: https://learn.microsoft.com/powershell/module/az.accounts/send-feedback
[DisableAzDataCollection]: https://learn.microsoft.com/powershell/module/az.accounts/disable-azdatacollection
