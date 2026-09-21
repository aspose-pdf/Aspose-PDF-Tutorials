---
category: general
date: 2026-03-03
description: Jak ověřit instalaci NuGet balíčku v PowerShellu. Naučte se spustit PowerShell
  jako administrátor, nainstalovat konkrétní verzi a efektivně spravovat balíčky.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: cs
og_description: Jak ověřit instalaci balíčku NuGet v PowerShellu. Tento krok‑za‑krokem
  průvodce vám ukáže, jak spustit PowerShell jako administrátor, nainstalovat konkrétní
  verzi a potvrdit, že je balíček přítomen.
og_title: Jak ověřit instalaci balíčku NuGet pomocí PowerShellu
tags:
- PowerShell
- NuGet
- Package Management
title: Jak ověřit instalaci balíčku NuGet pomocí PowerShellu
url: /cs/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ověřit instalaci NuGet balíčku pomocí PowerShell

Ověřit instalaci NuGet balíčku v PowerShellu je běžný úkol pro správce Windows. Pokud jste se někdy ptali, zda se balíček skutečně nainstaloval ve vašem systému, tento průvodce vám přesně ukáže, jak instalaci ověřit – bez hádání.  

V následujících několika minutách vás provedeme spuštěním PowerShellu jako administrátor, stažením konkrétní verze balíčku a nakonec potvrzením, že balíček existuje ve vašem počítači. Také se dozvíte několik tipů pro každodenní **PowerShell package management**, které udrží vaše prostředí přehledné.  

Než se pustíme dál, ujistěte se, že máte počítač s Windows a PowerShell 7 (nebo Windows PowerShell 5.1) a připojení k internetu. Nepotřebujete žádné další nástroje; vše běží přímo z vestavěného poskytovatele PackageManagement.

---

![Screenshot of an elevated PowerShell window with the Get-Package command](/images/verify-installation.png "Screenshot showing how to verify installation in an elevated PowerShell window")

## Krok 1: Spusťte PowerShell jako administrátor  

Spuštění PowerShellu s administrátorskými právy je první obranná linie proti problémům souvisejícím s oprávněními. Když **spustíte PowerShell jako administrátor**, cmdlet `Install-Package` může zapisovat do složky Program Files a zaregistrovat balíček v systémovém katalogu.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Tip:** Připněte zkratku “Windows PowerShell (Admin)” na hlavní panel. Jedním kliknutím jste připraveni.

### Proč je zvýšení oprávnění důležité  

Bez zvýšení oprávnění může `Install-Package` tiše přejít na uživatelsky omezené umístění, což může později zmást `Get-Package`, protože ve výchozím nastavení hledá v systémovém rozsahu. Zvýšení zaručuje, že se balíček objeví tam, kde jej většina skriptů očekává.

---

## Krok 2: Nainstalujte konkrétní verzi NuGet balíčku  

Často nechcete nejnovější vydání, ale známou stabilní verzi, proti které byl váš projekt testován. Vzor **install specific version** je jednoduchý s příznakem `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Rozbor příkazu  

| Parametr | Co dělá | Proč je potřeba |
|----------|---------|-----------------|
| `-Version 25.3` | Upevňuje přesné číslo buildu | Zaručuje reprodukovatelné sestavení |
| `-ProviderName NuGet` | Určuje PowerShellu, který poskytovatel se má použít | Zabraňuje nejasnostem, pokud je registrováno více poskytovatelů |
| `-Scope AllUsers` | Instaluje pro každý účet na počítači | Funguje s dotazy `Get-Package` na úrovni systému |
| `-Force` | Potlačuje výzvy (užitečné ve skriptech) | Udržuje automatizaci plynulou |

> **Pozor:** Pokud vynecháte `-Version`, PowerShell stáhne nejnovější balíček, což může zavést breaking changes.

---

## Krok 3: Ověřte instalaci  

Nyní nastává okamžik pravdy: **jak ověřit instalaci**. Nejpřímější způsob je požádat PowerShell o balíček, který jste právě nainstalovali.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Měli byste vidět výstup podobný tomuto:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Pokud příkaz nevrátí nic, zkuste dotaz v uživatelském rozsahu:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternativní metody ověření  

1. **Zkontrolujte složku modulu** – Balíčky jsou uloženy v `C:\Program Files\PackageManagement\Packages\`. Hledejte složku s názvem `Aspose.PDF.25.3`.  
2. **Použijte `Find-Package`** – Toto prohledá úložiště a může potvrdit, že verze je dostupná:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Ověřte pomocí .NET** – Načtěte sestavení v PowerShellu, aby bylo jisté, že DLL lze načíst:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Pokud některá z těchto kontrol uspěje, úspěšně jste **ověřili instalaci**.

---

## Časté úskalí a jak se jim vyhnout  

- **Chybějící poskytovatel NuGet** – Nejprve spusťte `Install-PackageProvider -Name NuGet -Force`.  
- **Bloky ExecutionPolicy** – Dočasně nastavte `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` pro tuto relaci.  
- **Problémy s proxy sítí** – Použijte parametry `-Proxy` a `-ProxyCredential`, pokud je vaše prostředí za firemní proxy.  
- **Konflikty verzí** – Když existuje více verzí, specifikujte `-RequiredVersion` v `Get-Package` pro rozlišení.

---

## Složení všeho dohromady – kompletní skript  

Níže je připravený skript, který zahrnuje všechny tři kroky, obsahuje zpracování chyb a vypíše přátelskou zprávu o úspěchu.

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

Spuštěním skriptu získáte jasnou řádku “✅ Successfully verified installation…”, která potvrzuje, že **jak ověřit instalaci** funguje od začátku do konce.

---

## Závěr  

Nyní víte, **jak ověřit instalaci** libovolného NuGet balíčku pomocí PowerShellu, od spuštění zvýšené relace po instalaci cílené verze a nakonec potvrzení přítomnosti balíčku. Ovládnutí těchto kroků vám dodá jistotu ve vašem workflow **PowerShell package management** a zabrání bolestem hlavy typu „vypadá to, že je nainstalováno, ale není“, které často trápí vývojáře Windows.

Co dál? Zkuste nahradit `Aspose.PDF` jinou knihovnou, experimentujte s `-Scope CurrentUser`, nebo vytvořte skript pro hromadnou instalaci několika balíčků na novém pracovním stanovišti. A pokud narazíte na podivnosti, pamatujte na výše uvedené tipy pro odstraňování problémů – zejména kontroly poskytovatele a ExecutionPolicy.

Šťastné skriptování a ať jsou vaše instalace vždy ověřitelné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}