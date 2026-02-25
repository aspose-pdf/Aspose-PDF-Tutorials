---
date: '2025-12-19'
description: Scopri come modificare il layout delle pagine PDF, modificare i segnalibri
  PDF e personalizzare le impostazioni del visualizzatore con Aspose.PDF per Java.
  Padroneggia le preferenze di navigazione e layout per un'esperienza utente più fluida.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'Modifica il layout della pagina PDF in Java - modifica segnalibri e impostazioni'
url: /it/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Modifica layout pagina PDF in Java: Modifica segnalibri e impostazioni

## Introduzione
Navigare documenti PDF complessi può risultare macchinoso, soprattutto quando l'impostazione **change PDF page layout** non è configurata correttamente o i segnalibri puntano a posizioni errate. In questo tutorial imparerai a **cambiare il layout della pagina PDF**, **modificare i segnalibri PDF** e **configurare le impostazioni del visualizzatore PDF** utilizzando Aspose.PDF per Java. Alla fine avrai il pieno controllo sulla navigazione, le destinazioni dei segnalibri e su come il documento viene presentato ai lettori.

**Cosa imparerai**
- Come modificare i segnalibri PDF esistenti in modo che puntino all'inizio di una pagina.
- Come impostare le destinazioni dei segnalibri durante la creazione di un PDF.
- Come modificare le preferenze del visualizzatore, come il layout della pagina.
- Consigli pratici per caricare un documento PDF in Java e ottimizzare le prestazioni.

### Risposta rapida
- **Qual è la modalità principale per cambiare il layout della pagina PDF?** Usa `PdfContentEditor.changeViewerPreference()` con `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.
- **Posso modificare le destinazioni dei segnalibri dopo che un PDF è stato creato?** Sì – carica il documento, accedi all'outline e imposta un nuovo `ExplicitDestination`.
- **Ho bisogno di una licenza per queste funzionalità?** Una prova gratuita è sufficiente per la valutazione; una licenza completa rimuove tutte le limitazioni.
- **Quale dipendenza Maven è necessaria?** `com.aspose:aspose-pdf:25.3` (o successiva).
- **È compatibile con Java 11 e versioni successive?** Assolutamente – Aspose.PDF supporta Java 8+.

## Cos'è “cambiare layout di pagina PDF”?
Modificare il layout della pagina PDF controlla come le pagine vengono registrate in un visualizzatore—pagina singola, continua, visualizzazione a due pagine, ecc. Regolare questa impostazione migliora la leggibilità, soprattutto per report lunghi o cataloghi.

## Perché modificare i segnalibri PDF e impostare le destinazioni dei segnalibri?
I segnalibri funzionano come un indice. Destinazioni precise garantiscono che i lettori saltano direttamente alla sezione desiderata, riducendo la frustrazione e migliorando l'esperienza complessiva dell'utente.

## Prerequisiti
- **Librerie e dipendenze**: Aspose.PDF per Javav25.3o successiva.
- **Ambiente**: JDK8o più recente, strumento per costruire Maven o Gradle.
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

**Acquisizione licenza**: Inizia con una prova gratuita o richiedi una licenza temporanea per l'accesso a tutte le funzionalità. Considera l'acquisto di una licenza permanente per l'uso in produzione.

### Inizializzazione di base
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
**Panoramica**: regola le preferenze del visualizzatore per visualizzare le pagine come desideri.

#### Inizializzazione di PdfContentEditor
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Modifica delle preferenze del visualizzatore
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Salvataggio del documento aggiornato
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### Come modificare i segnalibri PDF
**Panoramica**: Regola i segnalibri esistenti in modo che puntino accuratamente all'inizio di una pagina specifica.

#### Accesso ai segnalibri
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Impostazione di una nuova destinazione
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Salvataggio delle modifiche
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### Come impostare la destinazione del segnalebro durante la creazione di un PDF
**Panoramica**: Crea segnalibri che conducono gli utenti direttamente alle posizioni desiderate in un PDF appena generato.

#### Creazione e configurazione di segnalibri
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definizione della destinazione del segnalibro
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Aggiunta e salvataggio del PDF
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Applicazioni pratiche
1. **Libri digitali** – Assicurati che il segnalibro di ogni capitolo arrivi in ​​cima alla pagina per un'esperienza di lettura fluida.
2. **Manuali tecnici** – Una navigazione precisa aiuta gli ingegneri a trovare rapidamente le sezioni, soprattutto in PDF di grandi dimensioni.
3. **Cataloghi di prodotto** – Il layout di una singola pagina rende la navigazione dei cataloghi sul tablet più intuitiva.

## Considerazioni sulle prestazioni
- **Ottimizzazione delle risorse**: Quando gestisci PDF di grandi dimensioni, usa `Document.optimizeResources()` per ridurre il consumo di memoria.
- **Gestione della memoria Java**: Chiudi esplicitamente gli stream e lascia che il garbage collector recuperi gli oggetti dopo l'elaborazione.

## Problemi e soluzioni comuni
- **Segnalibri non aggiornati**: Verifica di modificare l'indice delineato corretto (`get_Item(1)` si riferisce al primo segnalibro di livello superiore).
- **Preferenza visualizzata non applicata**: Assicurati di chiamare `editor.save()` dopo aver modificato la preferenza; altrimenti le modifiche rimarrebbero solo in memoria.
- **Eccezioni di licenza**: Una licenza di prova può aggiungere filigrane; ottieni una licenza completa per la produzione.

## Domande frequenti
**D: Qual è il modo più semplice per caricare un documento PDF in Java?**
R: Usa `new Document("percorso/del/file.pdf")`; Aspose.PDF rileva automaticamente il formato del file.

**D: Posso cambiare il layout della pagina senza usare PdfContentEditor?**
R: Sì, puoi impostare le preferenze del visualizzatore direttamente sull'oggetto `Document` tramite `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**D: La modifica del layout del display influisce sulla stampa?**
R: Il layout del visualizzatore influisce solo sulla visualizzazione a schermo; non modificare l'output stampato.

**D: Ci sono limiti al numero di segnalibri che posso creare?**
A: Nessun limite esplicito, ma alberi di contorno estremamente grandi possono influire sulle prestazioni; mantienili organizzati.

**D: Come garantisco che le destinazioni dei segnalibri siano accurate dopo aver aggiunto o rimosso le pagine?**
A: Ricalcola le destinazioni utilizzando gli indici di pagina correnti dopo qualsiasi modifica strutturale.

## Risorse
- **Documentazione**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Scarica**: [Ultime versioni per Java](https://releases.aspose.com/pdf/java/)
- **Acquista**: [Acquista licenza Aspose.PDF](https://purchase.aspose.com/buy)
- **Prova gratuita**: [Prova Aspose.PDF gratuitamente](https://releases.aspose.com/pdf/java/)
- **Licenza temporanea**: [Richiedi licenza temporanea](https://purchase.aspose.com/temporary-license)

---

**Ultimo aggiornamento:** 2025-12-19
**Testato con:** Aspose.PDF per Javav25.3
**Autore:** Chiedi  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}