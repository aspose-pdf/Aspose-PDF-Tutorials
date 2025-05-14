---
"description": "Scopri come firmare file PDF utilizzando una smart card con Aspose.PDF per .NET. Segui questa guida passo passo per firme digitali sicure."
"linktitle": "Firma con la smart card utilizzando la firma del file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Firma con la smart card utilizzando la firma del file PDF"
"url": "/it/net/programming-with-security-and-signatures/sign-with-smart-card-using-pdf-file-signature/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Firma con la smart card utilizzando la firma del file PDF

## Introduzione

Nell'era digitale, proteggere i documenti è più cruciale che mai. Che si tratti di un contratto, di un accordo o di qualsiasi informazione sensibile, garantire che il documento sia autentico e non sia stato manomesso è fondamentale. È arrivato il momento delle firme digitali! Oggi approfondiremo come firmare un file PDF utilizzando una smart card con Aspose.PDF per .NET. Questa potente libreria consente agli sviluppatori di manipolare e creare documenti PDF in modo efficiente, inclusa l'aggiunta di firme digitali sicure. Quindi, prendi la tua smart card e iniziamo!

## Prerequisiti

Prima di addentrarci nei dettagli della firma di un file PDF, assicuriamoci di avere tutto il necessario. Ecco una checklist per aiutarti a prepararti:

1. Aspose.PDF per .NET: assicurati di aver installato la libreria Aspose.PDF. Puoi scaricarla da [sito](https://releases.aspose.com/pdf/net/).
2. Visual Studio: un ambiente di sviluppo in cui puoi scrivere ed eseguire il codice .NET.
3. Smart Card: è necessaria una smart card con installato un certificato digitale valido.
4. Nozioni di base di C#: la familiarità con la programmazione C# sarà utile poiché scriveremo frammenti di codice in questo linguaggio.
5. Documento PDF: un file PDF di esempio (come `blank.pdf`) per testare il nostro processo di firma.

Una volta soddisfatti questi prerequisiti, sei pronto per immergerti nel codice!

## Importa pacchetti

Per prima cosa, importiamo i pacchetti necessari. Dovrai aggiungere riferimenti alla libreria Aspose.PDF nel tuo progetto. Ecco come fare:

1. Aprire Visual Studio.
2. Crea un nuovo progetto o aprine uno esistente.
3. Fai clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e seleziona `Manage NuGet Packages`.
4. Cercare `Aspose.PDF` e installare la versione più recente.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ora che abbiamo importato i pacchetti necessari, analizziamo il codice passo dopo passo.

## Passaggio 1: imposta il documento

Il primo passo del nostro processo è impostare il documento PDF che vogliamo firmare. Ecco come fare:

```csharp
string dataDir = "YOUR DOCUMENTS DIRECTORY";
Document doc = new Document(dataDir + "blank.pdf");
```
In questo frammento definiamo il percorso verso la nostra directory dei documenti e creiamo un'istanza di `Document` classe utilizzando un file PDF di esempio denominato `blank.pdf`Assicurati di sostituire `"YOUR DOCUMENTS DIRECTORY"` con il percorso effettivo in cui si trova il PDF.

## Passaggio 2: inizializzare PdfFileSignature

Successivamente, inizializzeremo il `PdfFileSignature` classe, responsabile della gestione del processo di firma.

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature())
{
    pdfSign.BindPdf(doc);
```
Qui creiamo un'istanza di `PdfFileSignature` e associarlo al nostro documento PDF. Questo prepara il documento per la firma.

## Passaggio 3: accedere al certificato della smart card

Ora arriva la parte cruciale: accedere al certificato digitale memorizzato sulla tua smart card. Ecco come possiamo farlo:

### Aprire l'archivio certificati

```csharp
System.Security.Cryptography.X509Certificates.X509Store store = new System.Security.Cryptography.X509Certificates.X509Store(System.Security.Cryptography.X509Certificates.StoreLocation.CurrentUser);
store.Open(System.Security.Cryptography.X509Certificates.OpenFlags.ReadOnly);
```
Apriamo l'archivio certificati presente nel profilo dell'utente corrente. Questo ci consente di accedere ai certificati installati sul tuo computer, inclusi quelli sulla tua smart card.

### Seleziona il certificato

```csharp
System.Security.Cryptography.X509Certificates.X509Certificate2Collection sel =
    System.Security.Cryptography.X509Certificates.X509Certificate2UI.SelectFromCollection(
        store.Certificates, null, null, System.Security.Cryptography.X509Certificates.X509SelectionFlag.SingleSelection);
```
Questo codice richiede all'utente di selezionare un certificato dalla raccolta. L'interfaccia utente visualizzerà tutti i certificati disponibili, consentendo di scegliere quello associato alla propria smart card.

## Passaggio 4: creare la firma esterna

Dopo aver selezionato il certificato, il passo successivo è creare una firma esterna utilizzando il certificato selezionato.

```csharp
Aspose.Pdf.Forms.ExternalSignature externalSignature = new Aspose.Pdf.Forms.ExternalSignature(sel[0]);
```
Qui creiamo un'istanza di `ExternalSignature` Utilizzando il certificato selezionato. Questo oggetto verrà utilizzato per firmare il documento PDF.

## Passaggio 5: imposta l'aspetto della firma

Ora impostiamo l'aspetto della nostra firma. Qui puoi personalizzare l'aspetto della tua firma sul documento.

```csharp
pdfSign.SignatureAppearance = dataDir + "demo.png";
```
In questo frammento, specifichiamo l'aspetto della firma fornendo il percorso di un file immagine (come un logo o un'immagine di firma). Assicurati di sostituire `"demo.png"` con l'immagine effettiva che vuoi utilizzare.

## Passaggio 6: firmare il PDF

Dopo aver impostato tutto, è il momento di firmare il documento PDF!

```csharp
pdfSign.Sign(1, "Reason", "Contact", "Location", true, new System.Drawing.Rectangle(100, 100, 200, 200), externalSignature);
pdfSign.Save(dataDir + "externalSignature2.pdf");
```
In questo passaggio chiamiamo il `Sign` metodo sul nostro `pdfSign` oggetto. Ecco cosa significa ogni parametro:
- `1`: Numero di pagina in cui apparirà la firma.
- `"Reason"`: Il motivo della firma del documento.
- `"Contact"`: Informazioni di contatto del firmatario.
- `"Location"`: La posizione del firmatario.
- `true`: Indica se creare una firma visibile.
- `new System.Drawing.Rectangle(100, 100, 200, 200)`: Posizione e dimensione della firma sul PDF.
- `externalSignature`: L'oggetto firma che abbiamo creato in precedenza.

Infine, salviamo il documento firmato come `externalSignature2.pdf`.

## Passaggio 7: verifica la firma

Dopo aver firmato il documento, è fondamentale verificare che la firma sia valida. Ecco come fare:

### Inizializza il processo di verifica

```csharp
using (Facades.PdfFileSignature pdfSign = new Facades.PdfFileSignature(new Document(dataDir + "externalSignature2.pdf")))
{
    IList<string> sigNames = pdfSign.GetSignNames();
```
Creiamo una nuova istanza di `PdfFileSignature` per il documento firmato. Recuperiamo quindi i nomi di tutte le firme presenti nel documento.

### Controllare la validità della firma

```csharp
for (int index = 0; index <= sigNames.Count - 1; index++)
{
    if (!pdfSign.VerifySigned(sigNames[index]) || !pdfSign.VerifySignature(sigNames[index]))
    {
        throw new ApplicationException("Not verified");
    }
}
```
Esaminiamo ogni nome di firma e ne verifichiamo la validità. Se una firma non supera la verifica, viene generata un'eccezione che indica che la firma non è valida.

## Conclusione

Ed ecco fatto! Hai firmato con successo un documento PDF utilizzando una smart card con Aspose.PDF per .NET. Questo processo non solo protegge il documento, ma aggiunge anche un livello di autenticità cruciale nel mondo digitale odierno. Che si tratti di contratti, documenti legali o informazioni sensibili, sapere come implementare le firme digitali è una competenza preziosa. 

## Domande frequenti

### Che cos'è Aspose.PDF per .NET?
Aspose.PDF per .NET è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire documenti PDF all'interno delle applicazioni .NET.

### Ho bisogno di una smart card per firmare i PDF?
Sebbene la smart card non sia obbligatoria, è altamente consigliata per le firme digitali sicure, in quanto fornisce un ulteriore livello di sicurezza.

### Posso usare qualsiasi file PDF per firmare?
Sì, puoi usare qualsiasi file PDF, ma assicurati che non sia protetto da password. In tal caso, dovrai prima sbloccarlo.

### Cosa succede se non ho un certificato digitale?
È possibile ottenere un certificato digitale da un'autorità di certificazione (CA) attendibile oppure utilizzare un certificato autofirmato a scopo di test.

### È disponibile una versione di prova di Aspose.PDF?
Sì, puoi scaricare una versione di prova gratuita da [Sito web di Aspose](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}