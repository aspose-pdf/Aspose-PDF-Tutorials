---
"description": "Scopri come estrarre i bordi da un file PDF e salvarli come immagine utilizzando Aspose.PDF per .NET. Guida passo passo con esempi di codice e suggerimenti per il successo."
"linktitle": "Estrai bordo nel file PDF"
"second_title": "Riferimento API Aspose.PDF per .NET"
"title": "Estrai bordo nel file PDF"
"url": "/it/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Estrai bordo nel file PDF

## Introduzione

Quando si lavora con i PDF, estrarre elementi specifici come bordi o tracciati grafici può sembrare un compito arduo. Ma con Aspose.PDF per .NET, è possibile estrarre facilmente bordi o forme da un file PDF e salvarli come immagine. In questo tutorial, approfondiremo il processo di estrazione di un bordo da un PDF e il suo salvataggio come immagine PNG. Preparati a prendere il controllo del contenuto grafico del tuo PDF!

## Prerequisiti

Prima di immergerci nel codice, assicurati di aver impostato tutto:

1. Aspose.PDF per .NET: se non hai ancora installato la libreria Aspose.PDF, puoi [scaricalo qui](https://releases.aspose.com/pdf/net/)Sarà inoltre necessario applicare la licenza, tramite la versione di prova gratuita o una licenza acquistata.
2. Configurazione IDE: configura un progetto C# in Visual Studio o in qualsiasi altro IDE .NET. Assicurati di aver aggiunto i riferimenti necessari alla libreria Aspose.PDF.
3. File PDF di input: tieni pronto un file PDF da cui estrarre i bordi. Questo tutorial farà riferimento a un file denominato `input.pdf`.

## Importazione dei pacchetti richiesti

Iniziamo importando gli spazi dei nomi necessari. Questi pacchetti forniscono gli strumenti necessari per manipolare il contenuto del PDF.

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

Ora che abbiamo capito le basi, passiamo alla guida dettagliata, in cui analizzeremo ogni parte del codice per spiegarla in dettaglio.


## Passaggio 1: caricamento del documento PDF

Il primo passo è caricare il documento PDF contenente il bordo che si desidera estrarre. Immagina di aprire un libro prima di iniziare a leggerlo: devi avere accesso al contenuto!

Inizieremo specificando la directory in cui è archiviato il file PDF e caricheremo il documento utilizzando `Aspose.Pdf.Document` classe.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Questo codice carica il `input.pdf` file dalla directory specificata. Assicurati che il percorso del file sia corretto, altrimenti potresti ricevere un errore di file non trovato.

## Fase 2: Impostazione della grafica e del bitmap

Prima di iniziare l'estrazione, dobbiamo creare un'area di disegno. Nel mondo .NET, questo significa impostare un oggetto Bitmap e un oggetto Graphics. Bitmap rappresenta l'immagine, mentre Graphics ci permetterà di disegnare forme, come i bordi, estratte dal PDF.

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

Ecco una ripartizione:
- Creiamo un'immagine bitmap delle dimensioni della prima pagina del PDF.
- GraphicsPath viene utilizzato per definire le forme (in questo caso, i bordi).
- La matrice definisce il modo in cui la grafica verrà trasformata; abbiamo bisogno di una matrice di inversione perché PDF e .NET hanno sistemi di coordinate diversi.

## Fase 3: Elaborazione del contenuto PDF


Il file PDF è una serie di comandi di disegno e dobbiamo elaborare ciascuno di questi comandi per identificare ed estrarre le informazioni sul bordo.

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // Elaborazione di comandi quali salvataggio/ripristino dello stato, disegno di linee, riempimento di forme, ecc.
}
```

Il codice esegue un ciclo su ogni operatore di disegno nel flusso di contenuti del PDF. Ogni operatore può rappresentare una linea, un rettangolo o un'altra istruzione grafica.

## Fase 4: Gestione degli operatori PDF

Ogni operatore nel file PDF controlla un'azione. Per estrarre il bordo, dobbiamo identificare comandi come "sposta a", "linea a" e "disegna rettangolo". I seguenti operatori gestiscono queste azioni:

- MoveTo: sposta il cursore su un punto di partenza.
- LineTo: traccia una linea dal punto corrente a un nuovo punto.
- Re: Disegna un rettangolo (potrebbe essere parte del bordo).

```csharp
Aspose.Pdf.Operators.MoveTo opMoveTo = op as Aspose.Pdf.Operators.MoveTo;
Aspose.Pdf.Operators.LineTo opLineTo = op as Aspose.Pdf.Operators.LineTo;
Aspose.Pdf.Operators.Re opRe = op as Aspose.Pdf.Operators.Re;

if (opMoveTo != null)
{
    lastPoint = new System.Drawing.PointF((float)opMoveTo.X, (float)opMoveTo.Y);
}
else if (opLineTo != null)
{
    System.Drawing.PointF linePoint = new System.Drawing.PointF((float)opLineTo.X, (float)opLineTo.Y);
    graphicsPath.AddLine(lastPoint, linePoint);
    lastPoint = linePoint;
}
else if (opRe != null)
{
    System.Drawing.RectangleF re = new System.Drawing.RectangleF((float)opRe.X, (float)opRe.Y, (float)opRe.Width, (float)opRe.Height);
    graphicsPath.AddRectangle(re);
}
```

In questa fase:
- Catturiamo i punti per ogni linea o forma disegnata.
- Per i rettangoli (`opRe`), li aggiungiamo direttamente al `graphicsPath`, che useremo più avanti per disegnare il bordo.

## Fase 5: Disegno del bordo

Una volta identificate le linee e i rettangoli che formano il bordo, dobbiamo disegnarli effettivamente sull'oggetto Bitmap. È qui che entra in gioco l'oggetto Graphics.

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- Creiamo un oggetto Graphics basato sulla bitmap.
- SmoothingMode.HighQuality garantisce un'immagine piacevolmente omogenea.
- Infine, utilizziamo DrawPath per disegnare il bordo.

## Passaggio 6: salvataggio del bordo estratto

Ora che abbiamo estratto il bordo, è il momento di salvarlo come file immagine. Questo salverà il bordo in formato PNG.

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- La bitmap viene salvata come immagine PNG.
- Ora puoi aprire questa immagine per visualizzare il bordo estratto.

## Conclusione

Estrarre i bordi da un file PDF utilizzando Aspose.PDF per .NET potrebbe sembrare complicato all'inizio, ma una volta capito, diventa semplice. Comprendendo gli operatori di disegno in un PDF e utilizzando le potenti librerie .NET, è possibile manipolare ed estrarre contenuti grafici in modo efficiente. Questa guida fornisce solide basi per iniziare a manipolare i PDF!

## Domande frequenti

### Come faccio a gestire più pagine in un PDF?  
È possibile scorrere ogni pagina del documento iterando `doc.Pages` invece di codificare in modo rigido `doc.Pages[1]`.

### Posso estrarre altri elementi, come il testo, utilizzando lo stesso approccio?  
Sì, Aspose.PDF fornisce API avanzate per estrarre testo, immagini e altri contenuti dai file PDF.

### Come posso richiedere una licenza per evitare limitazioni?  
Puoi [applicare una licenza](https://purchase.aspose.com/temporary-license/) caricandolo tramite il `License` classe fornita da Aspose.

### Cosa succede se il mio PDF non ha bordi?  
Se il PDF non contiene bordi visibili, il processo di estrazione della grafica potrebbe non produrre alcun risultato. Assicurati che il contenuto del PDF includa bordi disegnabili.

### Posso salvare l'output in formati diversi da PNG?  
Sì, basta cambiare il `ImageFormat.Png` in un altro formato supportato come `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}