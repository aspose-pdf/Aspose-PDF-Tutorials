---
"description": "Scopri come firmare digitalmente un PDF con marca temporale utilizzando Aspose.PDF per .NET. Questa guida dettagliata illustra i prerequisiti, la configurazione del certificato, la marca temporale e altro ancora."
"linktitle": "Firma digitale con marca temporale nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Firma digitale con marca temporale nel file PDF"
"url": "/it/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Firma digitale con marca temporale nel file PDF

## Introduzione

Hai mai avuto bisogno di firmare digitalmente un PDF e includere una marca temporale per una maggiore sicurezza? Che tu stia lavorando a documenti legali, contratti o qualsiasi cosa che richieda un'autenticazione sicura, una firma digitale con marca temporale aggiunge un ulteriore livello di credibilità. In questo tutorial, ti spiegheremo come utilizzare Aspose.PDF per .NET per aggiungere una firma digitale e una marca temporale ai tuoi documenti PDF. Non preoccuparti, ti guideremo passo dopo passo!

## Prerequisiti

Prima di immergerci nel codice, ci sono alcune cose che dovrai configurare per seguire il tutorial. Ecco una rapida checklist dei prerequisiti per iniziare:

- Libreria Aspose.PDF per .NET: è necessario che la libreria Aspose.PDF per .NET sia installata nel progetto. È possibile [scarica l'ultima versione qui](https://releases.aspose.com/pdf/net/) oppure aggiungilo al tuo progetto tramite NuGet.
- Un documento PDF: avrai bisogno di un file PDF di esempio con cui lavorare. Assicurati di avere un file nella directory del tuo progetto che desideri firmare.
- Certificato digitale (file PFX): assicurati di avere un certificato digitale (un `.pfx` file) per firmare digitalmente il documento.
- URL di marcatura temporale: si tratta di un servizio di marcatura temporale online che verrà utilizzato per allegare una marca temporale alla firma digitale. 
- Conoscenza di base di C#: non è necessario essere un esperto, ma conoscere le basi di C# ti aiuterà a comprendere e personalizzare il codice.

Una volta spuntate tutte queste caselle, sei pronto per iniziare a programmare!

## Importa pacchetti

Per iniziare, dovrai importare i seguenti namespace nel tuo progetto C#. Questo ti garantirà l'accesso alle classi e alle funzioni Aspose.PDF pertinenti.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Passaggio 1: caricare il documento PDF

La prima cosa che dobbiamo fare è caricare il documento PDF che vogliamo firmare. Ecco come fare:

```csharp
// Definisci il percorso verso la directory dei tuoi documenti
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Carica il documento PDF
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Questo passaggio è piuttosto semplice. Stiamo semplicemente definendo il percorso del documento che vogliamo firmare. `Document` La classe di Aspose.PDF gestisce il caricamento del file.

## Passaggio 2: impostare la firma digitale

Successivamente, creeremo la firma digitale utilizzando la classe PKCS7 e caricheremo il file PFX. Questo file PFX contiene il certificato e la chiave privata, necessari per firmare il documento.

```csharp
// Percorso al file .pfx
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Inizializza l'oggetto firma
PdfFileSignature signature = new PdfFileSignature(document);

// Carica il file PFX con una password
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

A questo punto, stai dicendo ad Aspose di utilizzare il tuo certificato digitale per firmare il documento. `PKCS7` L'oggetto gestisce tutto il lavoro crittografico per te, così non devi preoccuparti dei dettagli minuziosi.

## Passaggio 3: aggiungere le impostazioni di timestamp

Uno degli elementi chiave di una firma digitale affidabile è la marca temporale. Questa garantisce che la firma del documento possa essere verificata anche dopo la scadenza del certificato. Impostiamo la marca temporale utilizzando un'autorità di marcatura temporale online.

```csharp
// Definisci le impostazioni del timestamp
TimestampSettings timestampSettings = new TimestampSettings("https://il_tuo_URL_data_data", "utente:password");

// Aggiungere impostazioni di timestamp all'oggetto PKCS7
pkcs.TimestampSettings = timestampSettings;
```

Qui, stai specificando l'URL del servizio di marcatura temporale, che fornirà automaticamente data e ora alla tua firma. Questa operazione può essere eseguita con o senza autenticazione.

## Passaggio 4: definire la posizione e l'aspetto della firma

Ora definiamo dove apparirà la firma nel PDF e le sue dimensioni. È possibile personalizzare la posizione del riquadro della firma sulla pagina, così come le sue dimensioni.

```csharp
// Definire l'aspetto e la posizione della firma (pagina 1, con rettangolo specificato)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Qui definiamo un rettangolo che posiziona la firma alle coordinate (100, 100) sulla prima pagina del PDF, con una larghezza di 200 e un'altezza di 100. Puoi modificare questi valori per adattarli al tuo progetto.

## Passaggio 5: firmare il documento PDF

Una volta configurato tutto, è il momento di applicare la firma digitale al PDF. Questo passaggio combina certificato, marca temporale e posizionamento in un unico semplice comando.

```csharp
// Firmare il documento sulla prima pagina
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Ecco cosa sta succedendo:
- 1: Indica che la firma deve essere applicata alla prima pagina.
- "Motivo della firma": qui puoi specificare il motivo per cui stai firmando il documento.
- "Contatto": inserisci le informazioni di contatto del firmatario.
- "Posizione": specificare la posizione del firmatario.
- true: questo valore booleano indica se la firma è visibile nel documento.
- rect: il rettangolo definito in precedenza specifica la dimensione e la posizione della firma.
- pkcs: l'oggetto PKCS7 contiene le impostazioni del certificato digitale e della marca temporale.

## Passaggio 6: salva il PDF firmato

Una volta firmato il documento, non resta che salvarlo. Puoi scegliere un nuovo nome per il file, in modo da conservare sia la versione originale che quella firmata.

```csharp
// Salva il documento PDF firmato
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Il PDF appena firmato e timbrato verrà salvato nella directory specificata!

## Conclusione

Ed ecco fatto! Hai firmato digitalmente un PDF con marca temporale utilizzando Aspose.PDF per .NET. Questo processo garantisce l'autenticità e l'integrità dei tuoi documenti, offrendo tranquillità sia a te che al destinatario. Le firme digitali stanno diventando sempre più essenziali nel mondo digitale odierno, quindi padroneggiare questo processo è sicuramente un'abilità che vale la pena acquisire.

## Domande frequenti

### Posso utilizzare un formato di file diverso per il certificato?  
Sì, ma il tutorial si concentra sull'utilizzo di un file PFX, che è il formato più comune per i certificati digitali.

### Ho bisogno di una connessione Internet per applicare la marca temporale?  
Sì, poiché la marca temporale viene recuperata da un'autorità di marcatura temporale online, avrai bisogno di un accesso a Internet.

### Posso firmare più pagine di un PDF?  
Assolutamente! Puoi modificare il `signature.Sign()` Metodo per selezionare più pagine o per scorrere tutte le pagine.

### Cosa succede se la password del file PFX è errata?  
Se la password è errata riceverai un'eccezione, quindi assicurati di averla inserita correttamente.

### Posso rendere invisibile la firma?  
Sì, puoi passare `false` al `Sign` parametro visibility del metodo per rendere invisibile la firma.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}