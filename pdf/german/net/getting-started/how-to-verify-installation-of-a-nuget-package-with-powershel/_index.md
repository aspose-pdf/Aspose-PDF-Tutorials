---
category: general
date: 2026-03-03
description: Wie man die Installation eines NuGet-Pakets in PowerShell überprüft.
  Erfahren Sie, wie Sie PowerShell als Administrator ausführen, eine bestimmte Version
  installieren und Pakete effizient verwalten.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: de
og_description: Wie man die Installation eines NuGet‑Pakets in PowerShell überprüft.
  Diese Schritt‑für‑Schritt‑Anleitung zeigt, wie man PowerShell als Administrator
  ausführt, eine bestimmte Version installiert und bestätigt, dass das Paket vorhanden
  ist.
og_title: Wie man die Installation eines NuGet-Pakets mit PowerShell überprüft
tags:
- PowerShell
- NuGet
- Package Management
title: Wie man die Installation eines NuGet-Pakets mit PowerShell überprüft
url: /de/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man die Installation eines NuGet‑Pakets mit PowerShell überprüft

Wie man die Installation eines NuGet‑Pakets in PowerShell überprüft, ist eine gängige Aufgabe für Windows‑Admins. Wenn Sie sich jemals gefragt haben, ob das Paket wirklich auf Ihrem System gelandet ist, zeigt Ihnen dieser Leitfaden genau, wie Sie die Installation verifizieren – ohne Rätselraten.  

In den nächsten Minuten gehen wir Schritt für Schritt durch, wie Sie PowerShell als Administrator starten, eine bestimmte Version eines Pakets abrufen und schließlich bestätigen, dass das Paket auf Ihrem Rechner vorhanden ist. Außerdem erhalten Sie ein paar Tipps für das tägliche **PowerShell package management**, die Ihre Umgebung aufgeräumt halten.  

Bevor wir loslegen, stellen Sie sicher, dass Sie einen Windows‑Rechner mit PowerShell 7 (oder Windows PowerShell 5.1) und eine Internetverbindung haben. Keine zusätzlichen Tools werden benötigt; alles läuft über den integrierten PackageManagement‑Provider.

---

![Screenshot eines erhöhten PowerShell-Fensters mit dem Get-Package-Befehl](/images/verify-installation.png "Screenshot, der zeigt, wie man die Installation in einem erhöhten PowerShell-Fenster überprüft")

## Schritt 1: PowerShell als Administrator ausführen  

PowerShell mit administrativen Rechten zu starten, ist die erste Verteidigungslinie gegen berechtigungsbedingte Stolpersteine. Wenn Sie **PowerShell als Admin ausführen**, kann das Cmdlet `Install-Package` in den Program Files‑Ordner schreiben und das Paket im systemweiten Katalog registrieren.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Profi‑Tipp:** Pinnen Sie die Verknüpfung „Windows PowerShell (Admin)“ an Ihre Taskleiste. Ein Klick und Sie sind startklar.

### Warum Erhöhung wichtig ist  

Ohne Erhöhung kann `Install-Package` stillschweigend an einen benutzerbezogenen Ort zurückfallen, was später `Get-Package` verwirren kann, weil es standardmäßig im System‑Scope sucht. Durch Erhöhung wird garantiert, dass das Paket dort erscheint, wo die meisten Skripte es erwarten.

---

## Schritt 2: Eine bestimmte Version des NuGet‑Pakets installieren  

Oft möchte man nicht die neueste Version, sondern eine bewährte Version, gegen die das Projekt getestet wurde. Das Muster **install specific version** ist mit dem `-Version`‑Flag ganz einfach.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Aufschlüsselung des Befehls  

| Parameter | Was es tut | Warum Sie es benötigen |
|-----------|------------|------------------------|
| `-Version 25.3` | Legt die genaue Build‑Nummer fest | Garantiert reproduzierbare Builds |
| `-ProviderName NuGet` | Teilt PowerShell mit, welchen Provider es verwenden soll | Vermeidet Mehrdeutigkeiten, falls mehrere Provider registriert sind |
| `-Scope AllUsers` | Installiert für jedes Konto auf dem Rechner | Funktioniert mit `Get-Package` systemweiten Abfragen |
| `-Force` | Unterdrückt Eingabeaufforderungen (nützlich in Skripten) | Hält die Automatisierung reibungslos |

> **Achtung:** Wenn Sie `-Version` weglassen, holt PowerShell das neueste Paket, was zu Breaking Changes führen kann.

---

## Schritt 3: Installation überprüfen  

Jetzt kommt der entscheidende Moment: **wie man die Installation überprüft**. Der direkteste Weg ist, PowerShell nach dem gerade installierten Paket zu fragen.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Sie sollten eine Ausgabe ähnlich der folgenden sehen:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Falls der Befehl nichts zurückgibt, versuchen Sie die benutzerbezogene Abfrage:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Alternative Verifizierungsmethoden  

1. **Modulordner prüfen** – Pakete werden unter `C:\Program Files\PackageManagement\Packages\` gespeichert. Suchen Sie nach einem Ordner mit dem Namen `Aspose.PDF.25.3`.  
2. **`Find-Package` verwenden** – Dies durchsucht das Repository und kann bestätigen, dass die Version verfügbar ist:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Mit .NET validieren** – Laden Sie die Assembly in PowerShell, um sicherzustellen, dass die DLL geladen werden kann:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Wenn einer dieser Checks erfolgreich ist, haben Sie die **Installation erfolgreich verifiziert**.

---

## Häufige Fallstricke und wie man sie vermeidet  

- **Fehlender NuGet‑Provider** – Führen Sie zuerst `Install-PackageProvider -Name NuGet -Force` aus.  
- **ExecutionPolicy‑Blockaden** – Setzen Sie temporär `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` für die Sitzung.  
- **Netzwerk‑Proxy‑Probleme** – Verwenden Sie die Parameter `-Proxy` und `-ProxyCredential`, falls Ihre Umgebung hinter einem Unternehmens‑Proxy liegt.  
- **Versionskonflikte** – Wenn mehrere Versionen existieren, geben Sie `-RequiredVersion` in `Get-Package` an, um sie zu unterscheiden.

---

## Alles zusammenführen – Ein komplettes Skript  

Unten finden Sie ein sofort ausführbares Skript, das die drei Schritte zusammenfasst, Fehlerbehandlung enthält und eine freundliche Erfolgsmeldung ausgibt.

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

Die Ausführung des Skripts liefert eine klare Zeile „✅ Successfully verified installation…“, die bestätigt, dass **how to verify installation** von Anfang bis Ende funktioniert.

---

## Fazit  

Sie wissen jetzt, **wie man die Installation** eines beliebigen NuGet‑Pakets mit PowerShell überprüft, vom Starten einer erhöhten Sitzung über die Installation einer gezielten Version bis hin zur Bestätigung der Paketpräsenz. Das Beherrschen dieser Schritte gibt Ihnen Vertrauen in Ihren **PowerShell package management**‑Workflow und verhindert die „es sieht installiert aus, ist es aber nicht“‑Kopfschmerzen, die Windows‑Entwickler häufig plagen.

Was kommt als Nächstes? Versuchen Sie, `Aspose.PDF` durch eine andere Bibliothek zu ersetzen, experimentieren Sie mit `-Scope CurrentUser` oder skripten Sie eine Masseninstallation mehrerer Pakete für einen neuen Arbeitsplatz. Und wenn Sie auf Eigenheiten stoßen, denken Sie an die oben genannten Fehlersuche‑Tipps – insbesondere die Provider‑ und Execution‑Policy‑Prüfungen.

Viel Spaß beim Skripten, und möge Ihre Installation stets verifizierbar sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}