---
category: general
date: 2026-03-03
description: Come verificare l'installazione di un pacchetto NuGet in PowerShell.
  Impara a eseguire PowerShell come amministratore, installare una versione specifica
  e gestire i pacchetti in modo efficiente.
draft: false
keywords:
- how to verify installation
- install specific version
- run powershell as admin
- install nuget package powershell
- powershell package management
language: it
og_description: Come verificare l'installazione di un pacchetto NuGet in PowerShell.
  Questa guida passo‑passo ti mostra come eseguire PowerShell come amministratore,
  installare una versione specifica e confermare che il pacchetto sia presente.
og_title: Come verificare l'installazione di un pacchetto NuGet con PowerShell
tags:
- PowerShell
- NuGet
- Package Management
title: Come verificare l'installazione di un pacchetto NuGet con PowerShell
url: /it/net/getting-started/how-to-verify-installation-of-a-nuget-package-with-powershel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come verificare l'installazione di un pacchetto NuGet con PowerShell

Verificare l'installazione di un pacchetto NuGet in PowerShell è un compito comune per gli amministratori Windows. Se ti sei mai chiesto se il pacchetto sia davvero stato installato sul tuo sistema, questa guida ti mostra esattamente come verificare l'installazione—senza supposizioni.  

Nei prossimi minuti vedremo come eseguire PowerShell come amministratore, scaricare una versione specifica di un pacchetto e, infine, confermare che il pacchetto esista sulla tua macchina. Acquisirai anche un paio di consigli per la **gestione dei pacchetti PowerShell** quotidiana che mantengono il tuo ambiente ordinato.  

Prima di iniziare, assicurati di avere una macchina Windows con PowerShell 7 (o Windows PowerShell 5.1) e una connessione internet. Non sono necessari strumenti aggiuntivi; tutto funziona direttamente dal provider integrato PackageManagement.

---

![Screenshot of an elevated PowerShell window with the Get-Package command](/images/verify-installation.png "Screenshot showing how to verify installation in an elevated PowerShell window")

## Passo 1: Esegui PowerShell come amministratore  

Eseguire PowerShell con diritti amministrativi è la prima linea di difesa contro problemi legati ai permessi. Quando **esegui PowerShell come amministratore**, il cmdlet `Install-Package` può scrivere nella cartella Program Files e registrare il pacchetto nel catalogo a livello di sistema.

```powershell
# Open an elevated session (manual step)
# Right‑click the PowerShell icon → Run as administrator
```

> **Suggerimento:** Aggiungi il collegamento “Windows PowerShell (Admin)” alla barra delle applicazioni. Un clic e sei pronto.

### Perché l'elevazione è importante  

Senza elevazione, `Install-Package` potrebbe tornare silenziosamente a una posizione a livello utente, il che può confondere `Get-Package` perché per impostazione predefinita cerca nello scope di sistema. L'elevazione garantisce che il pacchetto appaia dove la maggior parte degli script se lo aspetta.

---

## Passo 2: Installa una versione specifica del pacchetto NuGet  

Spesso non vuoi l'ultima versione ma una versione nota e stabile con cui il tuo progetto è stato testato. Il modello **install specific version** è semplice da usare con l'opzione `-Version`.

```powershell
# Install Aspose.PDF version 25.3 from the PowerShell Gallery
Install-Package Aspose.PDF -Version 25.3 -ProviderName NuGet -Scope AllUsers -Force
```

### Analisi del comando  

| Parametro | Cosa fa | Perché ti serve |
|-----------|--------------|-----------------|
| `-Version 25.3` | Fissa il numero di build esatto | Garantisce build riproducibili |
| `-ProviderName NuGet` | Indica a PowerShell quale provider utilizzare | Evita ambiguità se sono registrati più provider |
| `-Scope AllUsers` | Installa per tutti gli account sulla macchina | Funziona con le query di `Get-Package` a livello di sistema |
| `-Force` | Sopprime le richieste (utile negli script) | Mantiene l'automazione fluida |

> **Attenzione:** Se ometti `-Version`, PowerShell recupera il pacchetto più recente, il che potrebbe introdurre cambiamenti incompatibili.

---

## Passo 3: Verifica l'installazione  

Ora arriva il momento della verità: **come verificare l'installazione**. Il modo più diretto è chiedere a PowerShell il pacchetto appena installato.

```powershell
# Retrieve the package info
Get-Package -Name Aspose.PDF -ProviderName NuGet
```

Dovresti vedere un output simile a:

```
Name           Version   Source   Summary
----           -------   ------   -------
Aspose.PDF    25.3      NuGet    .NET PDF library from Aspose
```

Se il comando non restituisce nulla, prova la query a livello utente:

```powershell
Get-Package -Name Aspose.PDF -ProviderName NuGet -Scope CurrentUser
```

### Metodi alternativi di verifica  

1. **Controlla la cartella del modulo** – I pacchetti sono memorizzati in `C:\Program Files\PackageManagement\Packages\`. Cerca una cartella chiamata `Aspose.PDF.25.3`.  
2. **Usa `Find-Package`** – Questo ricerca nel repository e può confermare che la versione è disponibile:  

   ```powershell
   Find-Package -Name Aspose.PDF -ProviderName NuGet | Where-Object { $_.Version -eq '25.3' }
   ```

3. **Convalida con .NET** – Carica l'assembly in PowerShell per assicurarti che il DLL sia caricabile:  

   ```powershell
   Add-Type -Path "C:\Program Files\PackageManagement\Packages\Aspose.PDF.25.3\lib\netstandard2.0\Aspose.Pdf.dll"
   [Aspose.Pdf.License] | Get-Member
   ```

Se uno di questi controlli ha successo, hai **verificato correttamente l'installazione**.

---

## Problemi comuni e come evitarli  

- **Provider NuGet mancante** – Esegui prima `Install-PackageProvider -Name NuGet -Force`.  
- **Blocchi di ExecutionPolicy** – Imposta temporaneamente `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` per la sessione.  
- **Problemi di proxy di rete** – Usa i parametri `-Proxy` e `-ProxyCredential` se il tuo ambiente è dietro un proxy aziendale.  
- **Conflitti di versione** – Quando esistono più versioni, specifica `-RequiredVersion` in `Get-Package` per distinguere.

---

## Mettere tutto insieme – Uno script completo  

Di seguito trovi uno script pronto all'uso che racchiude i tre passaggi, include la gestione degli errori e stampa un messaggio di successo amichevole.

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

Eseguendo lo script otterrai una chiara riga “✅ Installazione verificata con successo…”, confermando che **come verificare l'installazione** funziona dall'inizio alla fine.

---

## Conclusione  

Ora sai **come verificare l'installazione** di qualsiasi pacchetto NuGet usando PowerShell, dall'avvio di una sessione elevata all'installazione di una versione mirata e infine alla conferma della presenza del pacchetto. Padroneggiare questi passaggi ti dà fiducia nel tuo flusso di lavoro di **gestione dei pacchetti PowerShell** e previene i mal di testa del tipo “sembra installato ma non lo è” che spesso affliggono gli sviluppatori Windows.

Cosa fare dopo? Prova a sostituire `Aspose.PDF` con un'altra libreria, sperimenta con `-Scope CurrentUser`, o scrivi uno script per l'installazione di massa di più pacchetti su una nuova workstation. E se incontri stranezze, ricorda i consigli di risoluzione dei problemi sopra—soprattutto i controlli sul provider e sulla execution‑policy.

Buona programmazione, e che le tue installazioni siano sempre verificabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}