---
category: general
date: 2026-02-20
description: Aprenda a instalar pacotes NuGet usando PowerShell, execute o PowerShell
  como administrador, liste os pacotes instalados e verifique o pacote instalado em
  minutos.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: pt
og_description: como instalar pacotes NuGet usando PowerShell, executar o PowerShell
  como administrador, listar pacotes instalados e verificar o pacote instalado — tutorial
  completo.
og_title: como instalar pacotes NuGet via PowerShell – guia rápido
tags:
- PowerShell
- NuGet
- Package Management
title: Como instalar pacotes NuGet via PowerShell – passo a passo
url: /pt/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como instalar pacotes nuget via PowerShell – passo a passo

Já se perguntou **como instalar pacotes nuget** sem abrir o Visual Studio? Você não está sozinho. Em muitas pipelines de CI ou em máquinas recém‑configuradas, a rota mais rápida é entrar no PowerShell — de preferência *executar powershell como admin* — e deixar o gerenciador de pacotes fazer o seu trabalho.

Neste tutorial vamos percorrer todo o processo: abrir o console correto, baixar uma versão específica de uma biblioteca e, finalmente, confirmar que o pacote realmente chegou ao seu sistema. Ao final, você será capaz de **listar pacotes instalados**, saber **como verificar a integridade do pacote** e sentir confiança de que a etapa **verificar pacote instalado** foi bem‑sucedida todas as vezes.

## O que você vai aprender

- Como iniciar o PowerShell com os privilégios corretos.  
- A sintaxe exata do comando `Install-Package` para NuGet.  
- Formas de **listar pacotes instalados** e confirmar números de versão.  
- Armadilhas comuns (faltam direitos de admin, incompatibilidade de versões) e como evitá‑las.  

Nenhuma experiência prévia com NuGet é necessária, apenas uma máquina Windows funcional e um pouco de curiosidade.

---

## Como instalar pacotes NuGet usando PowerShell

> **Dica de especialista:** Se você costuma adicionar os mesmos pacotes, considere colocá‑los em um arquivo de script e executá‑lo com `-File`. Isso evita digitar a mesma linha repetidamente.

### Passo 1: Abra o PowerShell com as permissões necessárias

A primeira coisa que você precisa fazer é **executar powershell como admin**. Sem direitos elevados, o cmdlet `Install-Package` pode falhar silenciosamente ou solicitar uma confirmação que você não quer lidar.

1. Clique no botão Iniciar.  
2. Digite **PowerShell**.  
3. Clique com o botão direito em *Windows PowerShell* e escolha **Executar como administrador**.  

Você verá um prompt de UAC; clique em **Sim**. Agora você tem uma sessão privilegiada pronta para a instalação de pacotes.

> *Por que admin?*  
> O NuGet grava arquivos na pasta global de pacotes (`C:\Program Files\PackageManagement\NuGet\Packages` por padrão). Essa localização é protegida, portanto somente um processo elevado pode gravar lá.

### Passo 2: Instale o pacote NuGet desejado e a versão específica

Com o console aberto, o comando principal é simples:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` é o wrapper do PowerShell ao cliente NuGet.  
- `-Version` fixa a compilação exata que você precisa, evitando atualizações acidentais.  

Se você omitir `-Version`, o PowerShell buscará a versão estável mais recente — às vezes isso é suficiente, outras vezes você quer a versão exata que testou.

#### O que acontece nos bastidores?

O PowerShell contata a fonte de pacotes configurada (por padrão `https://www.nuget.org/api/v2`) e baixa o arquivo `.nupkg`. Em seguida, extrai os DLLs para a pasta global de pacotes e registra o pacote no provedor de pacotes local. Todo o processo costuma terminar em poucos segundos, a menos que você esteja em uma rede lenta.

### Passo 3: Verifique se o pacote foi instalado com sucesso

Agora que o pacote está no disco, você provavelmente vai se perguntar: **“Como verifico o pacote?”** A resposta está em uma consulta simples:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Executar isso retorna algo como:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Essa saída confirma duas coisas:

1. O pacote **Aspose.PDF** está presente.  
2. Sua versão corresponde à que você solicitou, atendendo ao requisito de **verificar pacote instalado**.

Se quiser ver *todos* os pacotes na máquina, remova o filtro `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Essa visualização de **listar pacotes instalados** é útil para auditorias ou quando você precisa limpar bibliotecas antigas.

### Passo 4: Opcional – lidando com casos extremos

#### a) Pacote não encontrado ou versão incompatível

Se o PowerShell responder com *“Package not found”* ou *“Version not available”*, verifique a ortografia e o número da versão. O NuGet não diferencia maiúsculas de minúsculas, mas um espaço extra quebra o comando.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Executando sem direitos de admin

Caso você esqueça de **executar powershell como admin**, o cmdlet lançará um erro de permissão. A solução é simplesmente fechar a janela e reabri‑la com direitos elevados — não há necessidade de reinstalar nada.

#### c) Usando uma fonte personalizada

Em ambientes corporativos você pode ter um feed NuGet interno:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

A etapa de verificação permanece a mesma; apenas lembre‑se de incluir `-Source` ao instalar.

---

## Tabela de referência rápida

| Ação                                 | Comando PowerShell                                          | Por que importa |
|--------------------------------------|-------------------------------------------------------------|-----------------|
| Abrir console elevado                | *Run PowerShell as Administrator*                           | Necessário para instalação global |
| Instalar uma versão específica       | `Install-Package <pkg> -Version <x.y.z>`                    | Garante builds reproduzíveis |
| Listar um único pacote               | `Get-Package -Name <pkg>`                                    | Confirma **como verificar o pacote** |
| Listar todos os pacotes NuGet        | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Útil para **listar pacotes instalados** |
| Buscar versões disponíveis           | `Find-Package <pkg> -AllVersions`                           | Ajuda quando a versão é desconhecida |

---

## Conclusão

Cobremos **como instalar pacotes nuget** usando PowerShell do início ao fim — abrindo o console **executar powershell como admin**, baixando uma versão específica e, finalmente, **listando pacotes instalados** para **verificar pacote instalado**. Com esses comandos no seu arsenal, você pode automatizar o gerenciamento de bibliotecas em qualquer máquina Windows, seja scriptando uma pipeline de CI ou simplesmente corrigindo um DLL ausente na sua estação de desenvolvimento.

Próximos passos? Experimente adicionar vários pacotes a um único script, explore o parâmetro `-Scope` para instalar localmente em um projeto, ou combine esses comandos com `Invoke-Expression` para criar um instalador leve para sua equipe. E se encontrar algum obstáculo, lembre‑se da etapa **como verificar o pacote** — ver a versão em `Get-Package` costuma ser a maneira mais rápida de identificar o problema.

Boa codificação com PowerShell! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}