---
category: general
date: 2026-02-20
description: Erfahren Sie, wie Sie NuGet‑Pakete mit PowerShell installieren, PowerShell
  als Administrator ausführen, installierte Pakete auflisten und das installierte
  Paket in wenigen Minuten überprüfen.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: de
og_description: Wie man NuGet-Pakete mit PowerShell installiert, PowerShell als Administrator
  ausführt, installierte Pakete auflistet und das installierte Paket überprüft – vollständige
  Anleitung.
og_title: Wie man NuGet‑Pakete über PowerShell installiert – Schnellleitfaden
tags:
- PowerShell
- NuGet
- Package Management
title: Wie man NuGet-Pakete über PowerShell installiert – Schritt für Schritt
url: /de/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---


{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man NuGet-Pakete über PowerShell installiert – Schritt für Schritt

Haben Sie sich jemals gefragt, **wie man NuGet** Pakete installiert, ohne Visual Studio zu öffnen? Sie sind nicht allein. In vielen CI-Pipelines oder auf frischen Maschinen ist der schnellste Weg, in PowerShell zu wechseln – vorzugsweise *run powershell as admin* – und den Paketmanager seine Arbeit machen zu lassen.

In diesem Tutorial gehen wir den gesamten Prozess durch: das Öffnen der richtigen Konsole, das Herunterladen einer bestimmten Version einer Bibliothek und schließlich das Bestätigen, dass das Paket wirklich auf Ihrem System gelandet ist. Am Ende können Sie **installierte Pakete auflisten**, wissen **wie man das Paket überprüft** und sind zuversichtlich, dass der Schritt **verify installed package** jedes Mal erfolgreich war.

## Was Sie lernen werden

- Wie man PowerShell mit den richtigen Berechtigungen startet.  
- Die genaue `Install-Package` Befehls‑Syntax für NuGet.  
- Möglichkeiten, **installierte Pakete auflisten** und Versionsnummern zu bestätigen.  
- Häufige Fallstricke (fehlende Administratorrechte, Versionskonflikte) und wie man sie vermeidet.  

Vorkenntnisse mit NuGet sind nicht erforderlich, nur ein funktionierender Windows‑Computer und ein wenig Neugier.

---

## Wie man NuGet-Pakete mit PowerShell installiert

> **Pro-Tipp:** Wenn Sie häufig dieselben Pakete hinzufügen, sollten Sie sie in eine Skriptdatei aufnehmen und mit `-File` ausführen. Das spart Ihnen das wiederholte Eingeben derselben Zeile.

### Schritt 1: PowerShell mit den erforderlichen Berechtigungen öffnen

Das allererste, was Sie tun müssen, ist **run powershell as admin**. Ohne erhöhte Rechte kann das `Install-Package` Cmdlet stillschweigend fehlschlagen oder nach einer Bestätigung fragen, die Sie nicht erhalten möchten.

1. Klicken Sie auf die Start-Schaltfläche.  
2. Geben Sie **PowerShell** ein.  
3. Rechts‑klicken Sie auf *Windows PowerShell* und wählen Sie **Run as administrator**.  

Sie sehen eine UAC‑Aufforderung; klicken Sie auf **Yes**. Jetzt haben Sie eine privilegierte Sitzung, bereit für die Paketinstallation.

> *Warum Administrator?*  
> NuGet schreibt Dateien in den globalen Paketordner (`C:\Program Files\PackageManagement\NuGet\Packages` standardmäßig). Dieser Ort ist geschützt, sodass nur ein erhöhter Prozess dort schreiben kann.

### Schritt 2: Das gewünschte NuGet-Paket und die Version installieren

With the console open, the core command is straightforward:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` ist die PowerShell‑Umhüllung um den NuGet‑Client.  
- `-Version` legt die genaue Build fest, die Sie benötigen, und verhindert versehentliche Upgrades.  

Wenn Sie `-Version` weglassen, holt PowerShell die neueste stabile Version – manchmal ist das in Ordnung, manchmal benötigen Sie die genaue Version, die Sie getestet haben.

#### Was passiert im Hintergrund?

PowerShell kontaktiert die konfigurierte Paketquelle (standardmäßig `https://www.nuget.org/api/v2`) und lädt die `.nupkg`‑Datei herunter. Anschließend extrahiert es die DLLs in den globalen Paketordner und registriert das Paket beim lokalen Paket‑Provider. Der gesamte Vorgang dauert in der Regel nur wenige Sekunden, es sei denn, Sie haben ein langsames Netzwerk.

### Schritt 3: Überprüfen, ob das Paket erfolgreich installiert wurde

Jetzt, wo das Paket auf der Festplatte ist, werden Sie sich wahrscheinlich fragen, **„Wie überprüfe ich das Paket?“** Die Antwort liegt in einer einfachen Abfrage:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Die Ausführung liefert etwa Folgendes:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Diese Ausgabe bestätigt zwei Dinge:

1. Das Paket **Aspose.PDF** ist vorhanden.  
2. Seine Version entspricht der von Ihnen angeforderten, was die Anforderung **verify installed package** erfüllt.

Wenn Sie *jedes* Paket auf dem Rechner sehen möchten, entfernen Sie den `-Name`‑Filter:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Diese Ansicht zum **installierte Pakete auflisten** ist praktisch für Audits oder wenn Sie alte Bibliotheken bereinigen müssen.

### Schritt 4: Optional – Umgang mit Randfällen

#### a) Paket nicht gefunden oder Versionskonflikt

Wenn PowerShell mit *„Package not found“* oder *„Version not available“* antwortet, überprüfen Sie Rechtschreibung und Versionsnummer erneut. NuGet ist nicht case‑sensitive, aber ein überflüssiges Leerzeichen bricht den Befehl.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Ausführung ohne Administratorrechte

Falls Sie vergessen, **run powershell as admin** auszuführen, wirft das Cmdlet einen Berechtigungsfehler. Die Lösung besteht einfach darin, das Fenster zu schließen und mit erhöhten Rechten erneut zu öffnen – eine Neuinstallation ist nicht nötig.

#### c) Verwendung einer benutzerdefinierten Quelle

In Unternehmensumgebungen kann es einen internen NuGet‑Feed geben:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Der Verifizierungsschritt bleibt gleich; denken Sie nur daran, beim Installieren `-Source` anzugeben.

---

## Schnellreferenztabelle

| Aktion                              | PowerShell‑Befehl                                          | Warum es wichtig ist |
|-------------------------------------|------------------------------------------------------------|----------------------|
| Erhöhte Konsole öffnen               | *Run PowerShell as Administrator*                          | Erforderlich für globale Installation |
| Bestimmte Version installieren       | `Install-Package <pkg> -Version <x.y.z>`                   | Garantiert reproduzierbare Builds |
| Ein einzelnes Paket auflisten        | `Get-Package -Name <pkg>`                                   | Bestätigt **wie man das Paket überprüft** |
| Alle NuGet-Pakete auflisten          | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Nützlich für **installierte Pakete auflisten** |
| Verfügbare Versionen suchen          | `Find-Package <pkg> -AllVersions`                          | Hilft, wenn die Version unbekannt ist |

## Fazit

Wir haben **wie man NuGet** Pakete mit PowerShell von Anfang bis Ende behandelt – die Konsole **run powershell as admin** öffnen, eine bestimmte Version herunterladen und schließlich **installierte Pakete auflisten**, um **verify installed package** zu **verifizieren**. Mit diesen Befehlen in Ihrem Werkzeugkasten können Sie die Bibliotheksverwaltung auf jedem Windows‑Computer automatisieren, egal ob Sie eine CI‑Pipeline skripten oder einfach eine fehlende DLL auf Ihrer Entwicklungsmaschine reparieren.

Nächste Schritte? Versuchen Sie, mehrere Pakete in ein einzelnes Skript zu integrieren, erkunden Sie den Parameter `-Scope`, um lokal für ein Projekt zu installieren, oder kombinieren Sie diese Befehle mit `Invoke-Expression`, um einen leichten Installer für Ihr Team zu erstellen. Und wenn Sie auf ein Problem stoßen, denken Sie an den Schritt **wie man das Paket überprüft** – das Anzeigen der Version in `Get-Package` ist oft der schnellste Weg, ein Problem zu erkennen.

Viel Spaß beim PowerShellen! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}