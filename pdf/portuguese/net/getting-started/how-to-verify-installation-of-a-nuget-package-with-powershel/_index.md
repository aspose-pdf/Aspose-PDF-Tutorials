---
category: general
date: 2026-03-03
description: Como verificar a instalação de um pacote NuGet no PowerShell. Aprenda
  a executar o PowerShell como administrador, instalar uma versão específica e gerenciar
  pacotes de forma eficiente.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: pt
og_description: Como verificar a instalação de um pacote NuGet no PowerShell. Este
  guia passo a passo mostra como executar o PowerShell como administrador, instalar
  uma versão específica e confirmar que o pacote está presente.
og_title: Como Verificar a Instalação de um Pacote NuGet com PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Como Verificar a Instalação de um Pacote NuGet com PowerShell
url: /pt/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Verificar a Instalação de um Pacote NuGet com PowerShell

Verificar a instalação de um pacote NuGet no PowerShell é uma tarefa comum para administradores Windows. Se você já se perguntou se o pacote realmente foi instalado no seu sistema, este guia mostra exatamente como verificar a instalação — sem adivinhações.  

Nos próximos minutos, vamos percorrer a execução do PowerShell como administrador, obter uma versão específica de um pacote e, finalmente, confirmar que o pacote existe na sua máquina. Você também aprenderá algumas dicas para o **gerenciamento de pacotes PowerShell** do dia a dia que mantêm seu ambiente organizado.  

Antes de começarmos, certifique-se de que você tem uma máquina Windows com PowerShell 7 (ou Windows PowerShell 5.1) e uma conexão à internet. Nenhuma ferramenta extra é necessária; tudo roda diretamente do provedor integrado PackageManagement.

---

![Captura de tela de uma janela do PowerShell elevada com o comando Get-Package](/images/verify-installation.png "Captura de tela mostrando como verificar a instalação em uma janela do PowerShell elevada")

## Etapa 1: Executar o PowerShell como Administrador  

Executar o PowerShell com direitos administrativos é a primeira linha de defesa contra problemas relacionados a permissões. Quando você **executa o PowerShell como administrador**, o cmdlet `Install-Package` pode gravar na pasta Program Files e registrar o pacote no catálogo de todo o sistema.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Dica profissional:** Fixe o atalho “Windows PowerShell (Admin)” na sua barra de tarefas. Um clique e você está pronto para usar.

### Por que a elevação importa  

Sem elevação, `Install-Package` pode silenciosamente recair para um local com escopo de usuário, o que pode confundir `Get-Package` posteriormente porque ele procura no escopo do sistema por padrão. Elevar garante que o pacote apareça onde a maioria dos scripts espera.

---

## Etapa 2: Instalar uma Versão Específica do Pacote NuGet  

Frequentemente você não quer a versão mais recente, mas uma versão conhecida que seu projeto já testou. O padrão **install specific version** é simples com a flag `-Version`.  

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Detalhando o comando  

| Parameter | O que faz | Por que você precisa |
|-----------|-----------|----------------------|
| `-Version 25.3` | Define o número exato da build | Garante builds reproduzíveis |
| `-ProviderName NuGet` | Informa ao PowerShell qual provedor usar | Evita ambiguidades se múltiplos provedores estiverem registrados |
| `-Scope AllUsers` | Instala para todas as contas na máquina | Funciona com consultas ao `Get-Package` em todo o sistema |
| `-Force` | Suprime prompts (útil em scripts) | Mantém a automação fluida |

> **Cuidado:** Se você omitir `-Version`, o PowerShell buscará o pacote mais recente, o que pode introduzir mudanças incompatíveis.

---

## Etapa 3: Verificar a Instalação  

Chegou o momento da verdade: **como verificar a instalação**. A maneira mais direta é solicitar ao PowerShell o pacote que você acabou de instalar.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Você deve ver uma saída semelhante a:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Se o comando não retornar nada, tente a consulta com escopo de usuário:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Métodos alternativos de verificação  

1. **Verificar a pasta do módulo** – Os pacotes são armazenados em `C:\Program Files\PackageManagement\Packages\`. Procure uma pasta chamada `Aspose.PDF.25.3`.  
2. **Usar `Find-Package`** – Isso pesquisa o repositório e pode confirmar que a versão está disponível:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Validar com .NET** – Carregue o assembly no PowerShell para garantir que o DLL pode ser carregado:

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Se alguma dessas verificações for bem-sucedida, você **verificou a instalação** com sucesso.

---

## Armadilhas Comuns e Como Evitá‑las  

- **Provedor NuGet ausente** – Execute `Install-PackageProvider -Name NuGet -Force` primeiro.  
- **Bloqueios de ExecutionPolicy** – Defina temporariamente `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` para a sessão.  
- **Problemas de proxy de rede** – Use os parâmetros `-Proxy` e `-ProxyCredential` se o seu ambiente estiver atrás de um proxy corporativo.  
- **Conflitos de versão** – Quando múltiplas versões existirem, especifique `-RequiredVersion` no `Get-Package` para desambiguar.

---

## Juntando Tudo – Um Script Completo  

Abaixo está um script pronto‑para‑executar que encapsula as três etapas, inclui tratamento de erros e exibe uma mensagem amigável de sucesso.

```powershell
<# 
.SYNOPSIS
    Installs a specific version of a NuGet package and verifies the installation.
.DESCRIPTION
    Demonstrates how to run PowerShell as admin, install a specific version, 
    and confirm that the package is present using Get-Package.
#>

# Ensure we are running elevated
if (-not ([Security.Principal.WindowsPrincipal] `
        [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole(`
        [Security.Principal.WindowsBuiltInRole]::Administrator)) {
    Write-Warning "Please run this script in an elevated PowerShell session."
    exit 1
}

$packageName = 'Aspose.PDF'
$packageVersion = '25.3'

try {
    Write-Host "Installing $packageName version $packageVersion..."
    Install-Package $packageName -Version $packageVersion `
        -ProviderName NuGet -Scope AllUsers -Force -ErrorAction Stop

    Write-Host "Installation completed. Verifying..."
    $pkg = Get-Package -Name $packageName -ProviderName NuGet -ErrorAction Stop

    if ($pkg.Version -eq $packageVersion) {
        Write-Host "`n✅ Successfully verified installation of $packageName $packageVersion."
    } else {
        Write-Error "Version mismatch: Expected $packageVersion but got $($pkg.Version)."
    }
}
catch {
    Write-Error "An error occurred: $_"
}
```

Executar o script gera uma linha clara “✅ Successfully verified installation…” confirmando que **como verificar a instalação** funciona de ponta a ponta.

---

## Conclusão  

Agora você sabe **como verificar a instalação** de qualquer pacote NuGet usando PowerShell, desde iniciar uma sessão elevada até instalar uma versão específica e, finalmente, confirmar a presença do pacote. Dominar essas etapas lhe dá confiança no seu fluxo de **gerenciamento de pacotes PowerShell** e evita as dores de cabeça do “parece instalado, mas não está” que frequentemente afligem desenvolvedores Windows.

O que vem a seguir? Experimente substituir `Aspose.PDF` por outra biblioteca, experimente `-Scope CurrentUser`, ou crie um script de instalação em massa de vários pacotes para uma nova estação de trabalho. E se você encontrar peculiaridades, lembre‑se das dicas de solução de problemas acima — especialmente as verificações de provedor e de execution‑policy.

Feliz scripting, e que suas instalações estejam sempre verificáveis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}