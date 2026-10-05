---
category: general
date: 2026-03-03
description: Jak zweryfikować instalację pakietu NuGet w PowerShell. Dowiedz się,
  jak uruchomić PowerShell jako administrator, zainstalować konkretną wersję i efektywnie
  zarządzać pakietami.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: pl
og_description: Jak zweryfikować instalację pakietu NuGet w PowerShell. Ten przewodnik
  krok po kroku pokazuje, jak uruchomić PowerShell jako administrator, zainstalować
  określoną wersję i potwierdzić, że pakiet jest obecny.
og_title: Jak sprawdzić instalację pakietu NuGet za pomocą PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Jak sprawdzić instalację pakietu NuGet za pomocą PowerShell
url: /pl/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zweryfikować instalację pakietu NuGet za pomocą PowerShell

Jak zweryfikować instalację pakietu NuGet w PowerShell to powszechne zadanie dla administratorów Windows. Jeśli kiedykolwiek zastanawiałeś się, czy pakiet naprawdę trafił na Twój system, ten przewodnik pokaże Ci dokładnie, jak zweryfikować instalację — bez domysłów.  

W ciągu kilku minut przejdziemy przez uruchamianie PowerShell jako administrator, pobieranie konkretnej wersji pakietu i ostateczne potwierdzenie, że pakiet istnieje na Twojej maszynie. Poznasz także kilka wskazówek dotyczących codziennego **PowerShell package management**, które pomogą utrzymać środowisko w porządku.  

Zanim zaczniemy, upewnij się, że masz komputer z systemem Windows z PowerShell 7 (lub Windows PowerShell 5.1) oraz połączenie z internetem. Nie potrzebujesz dodatkowych narzędzi; wszystko działa bezpośrednio z wbudowanego dostawcy PackageManagement.

---

![Zrzut ekranu podniesionego okna PowerShell z poleceniem Get-Package](/images/verify-installation.png "Zrzut ekranu pokazujący, jak zweryfikować instalację w podniesionym oknie PowerShell")

## Krok 1: Uruchom PowerShell jako administrator  

Uruchamianie PowerShell z uprawnieniami administratora to pierwsza linia obrony przed problemami związanymi z uprawnieniami. Gdy **uruchomisz PowerShell jako admin**, polecenie `Install-Package` może zapisywać do folderu Program Files i rejestrować pakiet w katalogu systemowym.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Wskazówka:** Przypnij skrót „Windows PowerShell (Admin)” do paska zadań. Jeden klik i jesteś gotowy.

### Dlaczego podniesienie uprawnień ma znaczenie  

Bez podniesienia uprawnień `Install-Package` może cicho przejść do lokalizacji scoped dla użytkownika, co później może wprowadzić zamieszanie w `Get-Package`, ponieważ domyślnie przeszukuje zakres systemowy. Podniesienie uprawnień gwarantuje, że pakiet pojawi się tam, gdzie większość skryptów się tego spodziewa.

---

## Krok 2: Zainstaluj konkretną wersję pakietu NuGet  

Często nie chcesz najnowszej wersji, lecz sprawdzoną wersję, z którą Twój projekt był testowany. Wzorzec **install specific version** jest prosty przy użyciu flagi `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Rozbicie polecenia  

| Parametr | Co robi | Dlaczego jest potrzebny |
|----------|---------|------------------------|
| `-Version 25.3` | Ustawia dokładny numer kompilacji | Gwarantuje odtwarzalne kompilacje |
| `-ProviderName NuGet` | Informuje PowerShell, którego dostawcę użyć | Unika niejednoznaczności, gdy zarejestrowano wiele dostawców |
| `-Scope AllUsers` | Instaluje dla każdego konta na maszynie | Działa z zapytaniami systemowymi `Get-Package` |
| `-Force` | Tłumi monity (przydatne w skryptach) | Utrzymuje płynność automatyzacji |

> **Uwaga:** Jeśli pominiesz `-Version`, PowerShell pobierze najnowszy pakiet, co może wprowadzić zmiany łamiące kompatybilność.

---

## Krok 3: Zweryfikuj instalację  

Teraz najważniejszy moment: **jak zweryfikować instalację**. Najbardziej bezpośredni sposób to poprosić PowerShell o pakiet, który właśnie zainstalowałeś.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Powinieneś zobaczyć wyjście podobne do:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Jeśli polecenie nie zwróci nic, spróbuj zapytania scoped dla użytkownika:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternatywne metody weryfikacji  

1. **Sprawdź folder modułu** – Pakiety są przechowywane w `C:\Program Files\PackageManagement\Packages\`. Poszukaj folderu o nazwie `Aspose.PDF.25.3`.  
2. **Użyj `Find-Package`** – To przeszukuje repozytorium i może potwierdzić dostępność wersji:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Zweryfikuj za pomocą .NET** – Załaduj zestaw w PowerShell, aby upewnić się, że DLL można załadować:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Jeśli którykolwiek z tych testów się powiedzie, pomyślnie **zweryfikowałeś instalację**.

---

## Częste pułapki i jak ich unikać  

- **Brak dostawcy NuGet** – Najpierw uruchom `Install-PackageProvider -Name NuGet -Force`.  
- **Blokady ExecutionPolicy** – Tymczasowo ustaw `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` dla sesji.  
- **Problemy z proxy sieciowym** – Użyj parametrów `-Proxy` i `-ProxyCredential`, jeśli twoje środowisko znajduje się za korporacyjnym proxy.  
- **Konflikty wersji** – Gdy istnieje wiele wersji, określ `-RequiredVersion` w `Get-Package`, aby rozróżnić.

---

## Łączenie wszystkiego – kompletny skrypt  

Poniżej znajduje się gotowy do uruchomienia skrypt, który kapsułkuje trzy kroki, zawiera obsługę błędów i wypisuje przyjazny komunikat o sukcesie.

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

Uruchomienie skryptu daje wyraźny wiersz „✅ Successfully verified installation…”, potwierdzający, że **how to verify installation** działa od początku do końca.

---

## Zakończenie  

Teraz wiesz, **jak zweryfikować instalację** dowolnego pakietu NuGet przy użyciu PowerShell, od uruchomienia podniesionej sesji, przez instalację wybranej wersji, aż po potwierdzenie obecności pakietu. Opanowanie tych kroków daje pewność w Twoim **PowerShell package management** i zapobiega bólom głowy typu „wygląda na zainstalowany, ale nie jest”, które często dręczą programistów Windows.

Co dalej? Spróbuj zamienić `Aspose.PDF` na inną bibliotekę, poeksperymentuj z `-Scope CurrentUser` lub napisz skrypt instalujący hurtowo wiele pakietów na nowym stanowisku roboczym. A jeśli napotkasz problemy, pamiętaj o wskazówkach rozwiązywania problemów powyżej — szczególnie o sprawdzeniu dostawcy i ustawień ExecutionPolicy.

Miłego skryptowania i niech Twoje instalacje zawsze będą weryfikowalne!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}