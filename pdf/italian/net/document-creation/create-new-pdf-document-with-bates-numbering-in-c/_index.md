---
category: general
date: 2026-08-04
description: Crea un nuovo documento PDF in C# e aggiungi rapidamente la numerazione
  Bates al PDF usando Aspose.Pdf – impara ad aggiungere una pagina vuota al PDF e
  numeri di pagina personalizzati.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: it
lastmod: 2026-08-04
og_description: Crea un nuovo documento PDF in C# e aggiungi automaticamente la numerazione
  Bates al PDF per la gestione dei casi legali – esempio di codice completo incluso.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Crea un nuovo documento PDF con numerazione Bates in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Crea un nuovo documento PDF con numerazione Bates in C#
url: /it/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un nuovo documento PDF con numerazione Bates in C#

Se hai bisogno di **creare un nuovo documento PDF** in C#, questa guida ti mostra come **aggiungere la numerazione Bates a un PDF** usando Aspose.Pdf. Imparerai a **aggiungere una pagina vuota al PDF**, configurare **l'aggiunta di numeri di pagina personalizzati**, e salvare il file finale.

Il tutorial copre ogni passaggio, dall'installazione della libreria alla generazione di un PDF che rispetta gli standard dei fascicoli legali. Alla fine potrai generare un PDF, inserire una pagina vuota, applicare i numeri Bates e personalizzare il formato di numerazione—tutto con un unico programma eseguibile.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* SDK .NET 6.0 o successivo installato  
* Visual Studio 2022 (o qualsiasi IDE C#)  
* Una licenza attiva di Aspose.Pdf per .NET o una chiave di valutazione gratuita  

Non è necessario alcun pacchetto NuGet aggiuntivo; il tutorial installa tutto automaticamente.

## Passo 1: Installa Aspose.Pdf tramite NuGet

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.Pdf
```

Il comando aggiunge l'ultima versione stabile di Aspose.Pdf al tuo progetto, fornendo le classi `Document`, `BatesNumbering` e altre classi per la manipolazione dei PDF che utilizzerai.

## Passo 2: Crea un nuovo documento PDF – configurazione iniziale

Creare il file PDF è la base per ogni operazione successiva. La classe `Document` rappresenta l'intero contenitore PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Perché è importante*: L'istanziazione di `Document` alloca le strutture interne necessarie per pagine, font e grafica. L'uso di `using var` garantisce che il file venga correttamente rilasciato dopo il salvataggio.

## Passo 3: Aggiungi una pagina vuota al PDF

Un PDF deve contenere almeno una pagina prima di poter inserire contenuti. L'aggiunta di una pagina vuota ti fornisce una tela pulita per i numeri Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

Il metodo `Pages.Add()` aggiunge una nuova pagina vuota alla fine della collezione di pagine del documento. Puoi ripetere questa chiamata per aggiungere altre pagine se in seguito devi **aggiungere numeri di pagina personalizzati** su più pagine.

## Passo 4: Configura la numerazione Bates – come aggiungere Bates

La numerazione Bates è un identificatore sequenziale comunemente usato nei documenti legali. La configuri tramite la classe `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Perché è importante*: `StartNumber` definisce il primo numero, `Prefix` aggiunge un'etichetta leggibile e `Increment` controlla la dimensione del passo. Puoi anche regolare `HorizontalAlignment`, `VerticalAlignment`, `FontSize` e `Margins` per controllare l'aspetto del numero su ogni pagina.

## Passo 5: Applica la numerazione Bates al PDF nella pagina

Ora che le opzioni di numerazione sono pronte, applicale alla pagina (o all'intero documento).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Chiamare `Apply` inserisce il numero formattato nel piè di pagina della pagina per impostazione predefinita. Se hai bisogno del numero altrove, imposta `bates.Position` prima di chiamare `Apply`.

## Passo 6: Salva il PDF con i numeri Bates applicati

Infine, scrivi il documento in memoria su disco.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

Il file salvato ora contiene una singola pagina con il numero Bates **CaseA-1000** visualizzato in fondo. Apri il PDF in qualsiasi visualizzatore per verificare la numerazione.

## Output previsto

Quando apri `BatesNumbered.pdf`, dovresti vedere:

* Una pagina vuota (o più se hai aggiunto pagine aggiuntive)  
* Il testo **CaseA-1000** posizionato in fondo alla pagina (posizione predefinita)  

Se aggiungi più pagine e riutilizzi la stessa istanza di `BatesNumbering`, i numeri verranno incrementati automaticamente (CaseA-1001, CaseA-1002, …).

## Consiglio esperto: Aggiungere numeri di pagina personalizzati oltre ai numeri Bates

A volte hai bisogno sia dei numeri Bates sia dei numeri di pagina tradizionali. Puoi combinarli aggiungendo un `TextFragment` dopo aver applicato la numerazione Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Questo frammento dimostra come **aggiungere numeri di pagina personalizzati** mantenendo l'etichetta Bates.

## Caso limite: Applicare la numerazione Bates a più pagine

Se il tuo documento contiene diverse pagine, puoi applicare la stessa istanza di `BatesNumbering` a ciascuna pagina in un ciclo:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

Il ciclo garantisce che ogni pagina riceva un numero sequenziale basato su `StartNumber` e `Increment` che hai definito.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| I numeri appaiono fuori centro | L'allineamento predefinito potrebbe non corrispondere al tuo layout | Imposta esplicitamente `bates.HorizontalAlignment` e `bates.VerticalAlignment` |
| I numeri si sovrappongono al contenuto esistente | Nessun margine è definito | Regola `bates.Margin` o utilizza `bates.Position` per spostare il numero |
| Eccezione di licenza a runtime | La versione di valutazione limita l'output | Applica una licenza valida di Aspose.Pdf prima di creare il documento (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Esempio completo funzionante

Di seguito trovi un programma autonomo che puoi copiare, incollare ed eseguire.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come aggiungere e personalizzare i numeri di pagina nei PDF usando Aspose.PDF per .NET | Guida alla manipolazione dei documenti](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Aggiungere numeri di pagina ai PDF usando FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Creare documento PDF con Aspose.PDF – Aggiungere pagina, forma e salvare](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}