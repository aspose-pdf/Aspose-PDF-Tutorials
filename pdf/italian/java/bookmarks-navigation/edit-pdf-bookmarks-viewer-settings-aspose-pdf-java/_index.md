---
date: '2026-05-28'
description: Scopri come impostare la visualizzazione a pagina singola PDF, modificare
  le preferenze del visualizzatore, modificare i segnalibri e configurare le impostazioni
  PDF utilizzando Aspose.PDF per Java.
keywords:
- single page view pdf
- aspose pdf maven dependency
- change pdf viewer preference
- configure pdf viewer settings
- set pdf bookmark destination
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  headline: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  type: TechArticle
- description: Learn how to set single page view PDF, change viewer preferences, edit
    bookmarks, and configure PDF settings using Aspose.PDF for Java.
  name: Single Page View PDF in Java – Change Layout & Edit Bookmarks
  steps:
  - name: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
    text: '**Digital Books** – Ensure each chapter bookmark lands at the top of the
      page for a seamless reading experience.'
  - name: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
    text: '**Technical Manuals** – Precise navigation helps engineers find sections
      quickly, especially in large PDFs.'
  - name: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
    text: '**Product Catalogs** – Single‑page layout makes browsing catalogs on tablets
      more intuitive.'
  type: HowTo
- questions:
  - answer: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects
      the file format.
    question: What is the easiest way to load a PDF document in Java?
  - answer: Yes, you can set viewer preferences directly on the `Document` object
      via `pdfDocument.getViewerPreferences().setPageLayout(...)`.
    question: Can I change the page layout without using PdfContentEditor?
  - answer: Viewer layout only influences on‑screen display; it does not alter the
      printed output.
    question: Does changing the viewer layout affect printing?
  - answer: No explicit limit, but extremely large outline trees may impact performance;
      keep them organized.
    question: Are there limits on the number of bookmarks I can create?
  - answer: Re‑calculate destinations using the current page indices after any structural
      changes.
    question: How do I ensure bookmark destinations are accurate after adding or removing
      pages?
  type: FAQPage
title: Visualizzazione a pagina singola PDF in Java – Cambia layout e modifica segnalibri
url: /it/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Visualizzazione a pagina singola PDF in Java – Modifica layout e segnalibri

## Introduzione
Quando i lettori aprono un PDF di grandi dimensioni, il layout predefinito del visualizzatore può scorrere in modo continuo, rendendo difficile concentrarsi su una singola pagina. Configurando l'impostazione **single page view pdf**, si costringe il visualizzatore a mostrare una pagina alla volta, ideale per report, e‑book e cataloghi. In questo tutorial imparerai anche a modificare i segnalibri PDF esistenti, impostare le destinazioni dei segnalibri durante la creazione di un documento e regolare altre preferenze del visualizzatore usando Aspose.PDF per Java. Alla fine avrai il pieno controllo sulla navigazione, sull'accuratezza dei segnalibri e sul layout a schermo.

**Cosa imparerai**
- Come modificare i segnalibri PDF esistenti in modo che puntino all'inizio di una pagina.  
- Come impostare le destinazioni dei segnalibri durante la creazione di un PDF.  
- Come cambiare le preferenze del visualizzatore, ad esempio il layout a pagina singola.  
- Suggerimenti pratici per caricare un documento PDF in Java e ottimizzare le prestazioni.

### Risposte rapide
- **Qual è il modo principale per abilitare la visualizzazione a pagina singola PDF?** Chiamare `PdfContentEditor.changeViewerPreference()` con `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Le destinazioni dei segnalibri possono essere modificate dopo la generazione del PDF?** Sì – carica il documento, recupera l'outline e assegna un nuovo `ExplicitDestination`.  
- **È necessaria una licenza per queste funzionalità?** Una prova gratuita è sufficiente per la valutazione; una licenza completa rimuove tutte le limitazioni.  
- **Quale dipendenza Maven è richiesta?** `com.aspose:aspose-pdf:25.3` (o successiva).  
- **È compatibile con Java 11 e versioni successive?** Assolutamente – Aspose.PDF supporta Java 8+.

## Cos'è “cambiare layout pagina PDF”?
Modificare il layout della pagina PDF controlla come le pagine vengono visualizzate in un visualizzatore—pagina singola, continua, visualizzazione a due pagine, ecc. Abilitare **single page view pdf** migliora la leggibilità dei documenti lunghi e garantisce che ogni pagina sia presentata in isolamento, particolarmente utile su dispositivi mobili e tablet.

## Perché modificare i segnalibri PDF e impostare le destinazioni dei segnalibri?
I segnalibri funzionano come un indice dinamico. Destinazioni precise consentono ai lettori di saltare direttamente alla sezione desiderata, eliminando lo scorrimento aggiuntivo e riducendo la frustrazione dell'utente. Questo porta a un'esperienza di navigazione più fluida e a una maggiore soddisfazione per manuali tecnici, cataloghi di prodotto e libri digitali.

## Prerequisiti
- **Librerie e dipendenze**: Aspose.PDF per Java v25.3 o successiva.  
- **Ambiente**: JDK 8 o più recente, strumento di build Maven o Gradle.  
- **Conoscenze**: Programmazione Java di base e familiarità con i concetti PDF.

## Configurazione di Aspose.PDF per Java
### Installazione Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Installazione Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Acquisizione della licenza**: Inizia con una prova gratuita o richiedi una licenza temporanea per l'accesso a tutte le funzionalità. Considera l'acquisto di una licenza permanente per l'uso in produzione.

### Inizializzazione di base
La classe `Document` è l'oggetto principale di Aspose.PDF che rappresenta un file PDF in memoria. Dopo aver creato un'istanza, tutte le operazioni di lettura/scrittura passano attraverso questo oggetto.  
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Guida all'implementazione
### Come cambiare il layout della pagina PDF in Java
**Panoramica**: Regola le preferenze del visualizzatore per mostrare le pagine nel modo desiderato.

#### Inizializzazione di PdfContentEditor
`PdfContentEditor` è una classe di utilità che consente di modificare le impostazioni del visualizzatore senza riscrivere l'intero documento.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Modifica delle preferenze del visualizzatore
Per abilitare **single page view pdf**, invoca `changeViewerPreference()` con il valore enum appropriato. Questa chiamata aggiorna il dizionario interno delle preferenze del visualizzatore del PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Salvataggio del documento aggiornato
Dopo aver modificato le preferenze, chiama `save()` per scrivere le modifiche su disco.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Come modificare i segnalibri PDF
**Risposta**: Per modificare i segnalibri esistenti, carica il PDF con `Document`, recupera la sua collezione di outline, individua l'`OutlineItem` desiderato e assegna un nuovo `ExplicitDestination` che punti alla pagina e alle coordinate corrette. Dopo aver aggiornato ogni segnalibro, salva il documento per rendere permanenti le modifiche. Questo garantisce che gli utenti vengano indirizzati esattamente alle sezioni previste senza scorrimenti aggiuntivi.

#### Accesso ai segnalibri
`OutlineItemCollection` rappresenta l'albero gerarchico dei segnalibri. Recuperalo dall'oggetto `Document` per lavorare con le singole voci.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Impostazione di una nuova destinazione
Un `ExplicitDestination` definisce la pagina esatta e la posizione a cui un segnalibro deve saltare. Assegnalo alla proprietà `Destination` dell'elemento outline.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Salvataggio delle modifiche
Rendi permanente l'albero dei segnalibri aggiornato chiamando `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Come impostare la destinazione del segnalibro durante la creazione di un PDF
**Risposta**: Quando generi un PDF, puoi creare segnalibri al volo istanziando oggetti `OutlineItem`, impostando i loro titoli e definendo un `ExplicitDestination` che punti a una pagina specifica e a una modalità di visualizzazione. Aggiungi ogni segnalibro alla collezione di outline del documento prima di salvare, così il file risultante conterrà un albero di navigazione pronto all'uso.

#### Creazione e configurazione del segnalibro
`OutlineItem` rappresenta una singola voce di segnalibro nell'outline PDF. Quando costruisci un PDF da zero, istanzia un nuovo `OutlineItem` e aggiungilo alla collezione di outline del documento.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definizione della destinazione del segnalibro
Usa `ExplicitDestination.createFitH(page, top)` per posizionare la visualizzazione in cima alla pagina di destinazione.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Aggiunta e salvataggio del PDF
Infine, aggiungi il segnalibro all'outline e salva il documento.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Applicazioni pratiche
1. **Libri digitali** – Assicurati che ogni segnalibro di capitolo arrivi in cima alla pagina per un'esperienza di lettura fluida.  
2. **Manuali tecnici** – Una navigazione precisa aiuta gli ingegneri a trovare rapidamente le sezioni, soprattutto in PDF di grandi dimensioni.  
3. **Cataloghi di prodotto** – Il layout a pagina singola rende la consultazione dei cataloghi su tablet più intuitiva.

## Considerazioni sulle prestazioni
- **Ottimizzazione delle risorse**: Aspose.PDF può elaborare PDF fino a 2 GB senza caricare l'intero file in memoria, grazie alla sua architettura di streaming. Usa `Document.optimizeResources()` per ridurre ulteriormente l'impronta di memoria.  
- **Gestione della memoria in Java**: Chiudi esplicitamente gli stream e consenti al garbage collector di recuperare gli oggetti dopo l'elaborazione per evitare perdite di memoria.

## Problemi comuni e soluzioni
- **Segnalibri non aggiornati**: Verifica di modificare l'indice outline corretto (`get_Item(1)` si riferisce al primo segnalibro di livello superiore).  
- **Preferenza del visualizzatore non applicata**: Assicurati di chiamare `editor.save()` dopo aver modificato le preferenze; altrimenti le modifiche rimangono solo in memoria.  
- **Eccezioni di licenza**: Una licenza di prova può aggiungere filigrane; ottieni una licenza completa per la produzione.

## Domande frequenti
**D: Qual è il modo più semplice per caricare un documento PDF in Java?**  
R: Usa `new Document("path/to/file.pdf")`; Aspose.PDF rileva automaticamente il formato del file.

**D: Posso cambiare il layout della pagina senza usare PdfContentEditor?**  
R: Sì, puoi impostare le preferenze del visualizzatore direttamente sull'oggetto `Document` tramite `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**D: La modifica del layout del visualizzatore influisce sulla stampa?**  
R: Il layout del visualizzatore influisce solo sulla visualizzazione a schermo; non altera l'output stampato.

**D: Ci sono limiti al numero di segnalibri che posso creare?**  
R: Nessun limite esplicito, ma alberi di outline estremamente grandi possono influire sulle prestazioni; mantienili organizzati.

**D: Come garantire che le destinazioni dei segnalibri siano accurate dopo aver aggiunto o rimosso pagine?**  
R: Ricalcola le destinazioni usando gli indici di pagina correnti dopo qualsiasi modifica strutturale.

## Risorse
- **Documentazione**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Acquisto**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Prova gratuita**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Licenza temporanea**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Ultimo aggiornamento:** 2026-05-28  
**Testato con:** Aspose.PDF per Java v25.3  
**Autore:** Aspose

## Tutorial correlati

- [How to Change PDF Viewer Preferences Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [How to Create PDF Bookmarks and Manage Navigation Using Aspose.PDF for Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [PDF Bookmarks and Navigation Tutorials for Aspose.PDF Java](/pdf/java/bookmarks-navigation/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}