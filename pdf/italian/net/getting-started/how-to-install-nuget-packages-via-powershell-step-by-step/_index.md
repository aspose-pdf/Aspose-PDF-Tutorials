---
category: general
date: 2026-02-20
description: Impara a installare i pacchetti NuGet usando PowerShell, esegui PowerShell
  come amministratore, elenca i pacchetti installati e verifica il pacchetto installato
  in pochi minuti.
draft: false
keywords:
- how to install nuget
- run powershell as admin
- list installed packages
- how to verify package
- verify installed package
language: it
og_description: come installare i pacchetti NuGet usando PowerShell, eseguire PowerShell
  come amministratore, elencare i pacchetti installati e verificare il pacchetto installato
  — guida completa.
og_title: come installare i pacchetti NuGet tramite PowerShell – guida rapida
tags:
- PowerShell
- NuGet
- Package Management
title: come installare i pacchetti NuGet tramite PowerShell – passo dopo passo
url: /it/net/getting-started/how-to-install-nuget-packages-via-powershell-step-by-step/
---


{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come installare pacchetti nuget tramite PowerShell – passo dopo passo

Ti sei mai chiesto **come installare nuget** senza aprire Visual Studio? Non sei l’unico. In molti pipeline CI o su macchine appena configurate, il percorso più veloce è aprire PowerShell—preferibilmente *run powershell as admin*—e lasciare che il package manager faccia il suo lavoro.

In questo tutorial percorreremo l’intero processo: aprire la console giusta, scaricare una versione specifica di una libreria e, infine, confermare che il pacchetto sia realmente stato installato sul tuo sistema. Alla fine sarai in grado di **list installed packages**, saprai **how to verify package** e avrai la certezza che il passaggio **verify installed package** sia riuscito ogni volta.

## Cosa imparerai

- Come avviare PowerShell con i privilegi corretti.  
- La sintassi esatta del comando `Install-Package` per NuGet.  
- Modi per **list installed packages** e confermare i numeri di versione.  
- Trappole comuni (mancanza di diritti admin, mismatch di versione) e come evitarle.  

Non è necessaria alcuna esperienza pregressa con NuGet, basta una macchina Windows funzionante e un po’ di curiosità.

---

## Come installare pacchetti NuGet usando PowerShell

> **Pro tip:** Se aggiungi spesso gli stessi pacchetti, considera di inserirli in un file script e di eseguirlo con `-File`. Ti farà risparmiare di digitare la stessa riga più e più volte.

### Step 1: Apri PowerShell con i permessi necessari

La prima cosa da fare è **run powershell as admin**. Senza privilegi elevati il cmdlet `Install-Package` potrebbe fallire silenziosamente o chiedere una conferma con cui non vuoi avere a che fare.

1. Fai clic sul pulsante Start.  
2. Digita **PowerShell**.  
3. Fai clic destro su *Windows PowerShell* e scegli **Run as administrator**.  

Vedrai una finestra UAC; fai clic su **Yes**. Ora hai una sessione privilegiata pronta per l’installazione dei pacchetti.

> *Perché admin?*  
> NuGet scrive i file nella cartella globale dei pacchetti (`C:\Program Files\PackageManagement\NuGet\Packages` per impostazione predefinita). Quella posizione è protetta, quindi solo un processo elevato **può scrivere lì**.

### Step 2: Installa il pacchetto NuGet desiderato e la versione

Con la console aperta, il comando principale è semplice:

```powershell
# Install the Aspose.PDF library, version 25.3
Install-Package Aspose.PDF -Version 25.3
```

- `Install-Package` è il wrapper PowerShell del client NuGet.  
- `-Version` fissa esattamente la build di cui hai bisogno, evitando aggiornamenti accidentali.  

Se ometti `-Version`, PowerShell scaricherà l’ultima release stabile—a volte va bene, a volte vuoi la versione esatta con cui hai testato.

#### Cosa succede dietro le quinte?

PowerShell contatta la sorgente di pacchetti configurata (per impostazione predefinita `https://www.nuget.org/api/v2`) e scarica il file `.nupkg`. Successivamente estrae i DLL nella cartella globale dei pacchetti e registra il pacchetto con il provider locale. L’intero processo di solito termina in pochi secondi, a meno che la rete non sia lenta.

### Step 3: Verifica che il pacchetto sia stato installato correttamente

Ora che il pacchetto è sul disco, probabilmente ti chiederai, **“How do I verify the package?”** La risposta è una semplice query:

```powershell
# List all installed NuGet packages
Get-Package -Name Aspose.PDF
```

Eseguendo questo ottieni qualcosa del tipo:

```
Name        Version   Source
----        -------   ------
Aspose.PDF  25.3      nuget.org
```

Quell’output conferma due cose:

1. Il pacchetto **Aspose.PDF** è presente.  
2. La sua versione corrisponde a quella richiesta, soddisfacendo il requisito **verify installed package**.

Se vuoi vedere *tutti* i pacchetti sulla macchina, rimuovi il filtro `-Name`:

```powershell
Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}
```

Questa vista **list installed packages** è utile per audit o quando devi pulire librerie obsolete.

### Step 4: Opzionale – gestione dei casi particolari

#### a) Pacchetto non trovato o mismatch di versione

Se PowerShell risponde con *“Package not found”* o *“Version not available”*, ricontrolla ortografia e numero di versione. NuGet non è sensibile al maiuscolo/minuscolo, ma uno spazio extra romperà il comando.

```powershell
# Search the NuGet feed for available versions
Find-Package Aspose.PDF -AllVersions
```

#### b) Esecuzione senza diritti admin

Se dimentichi di **run powershell as admin**, il cmdlet genererà un errore di permesso. La soluzione è semplicemente chiudere la finestra e riaprirla con privilegi elevati—non è necessario reinstallare nulla.

#### c) Uso di una sorgente personalizzata

In ambienti corporate potresti avere un feed NuGet interno:

```powershell
Install-Package MyCompany.Logging -Source https://nuget.mycompany.local/api/v2
```

Il passaggio di verifica rimane lo stesso; ricorda solo di includere `-Source` quando installi.

---

## Tabella di riferimento rapido

| Azione                              | Comando PowerShell                                          | Perché è importante |
|-------------------------------------|-------------------------------------------------------------|---------------------|
| Apri console elevata                | *Run PowerShell as Administrator*                           | Necessario per installazione globale |
| Installa una versione specifica     | `Install-Package <pkg> -Version <x.y.z>`                    | Garantisce build riproducibili |
| Elenca un singolo pacchetto         | `Get-Package -Name <pkg>`                                    | Conferma **how to verify package** |
| Elenca tutti i pacchetti NuGet      | `Get-Package | Where-Object {$_.ProviderName -eq 'NuGet'}`| Utile per **list installed packages** |
| Cerca versioni disponibili          | `Find-Package <pkg> -AllVersions`                           | Aiuta quando la versione è sconosciuta |

---

## Conclusione

Abbiamo coperto **how to install nuget** pacchetti usando PowerShell dall’inizio alla fine—aprendo la console **run powershell as admin**, scaricando una versione specifica e infine **list installed packages** per **verify installed package**. Con questi comandi nel tuo toolbox puoi automatizzare la gestione delle librerie su qualsiasi macchina Windows, sia che tu stia scriptando una pipeline CI sia che tu stia semplicemente risolvendo una DLL mancante sul tuo PC di sviluppo.

Prossimi passi? Prova ad aggiungere più pacchetti in un unico script, esplora il parametro `-Scope` per installare localmente a un progetto, o combina questi comandi con `Invoke-Expression` per creare un installer leggero per il tuo team. E se incontri un intoppo, ricorda il passaggio **how to verify package**—vedere la versione in `Get-Package` è spesso il modo più veloce per individuare un problema.

Buon PowerShelling! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}