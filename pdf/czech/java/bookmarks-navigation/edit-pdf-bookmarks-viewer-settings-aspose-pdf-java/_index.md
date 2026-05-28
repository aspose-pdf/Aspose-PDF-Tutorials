---
date: '2026-05-28'
description: Naučte se, jak nastavit single page view PDF, změnit viewer preferences,
  edit bookmarks a configure PDF settings pomocí Aspose.PDF for Java.
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
title: Single Page View PDF v Javě – Change Layout & Edit Bookmarks
url: /cs/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/products-backtop-button >}}
# Jednostránkové zobrazení PDF v Javě – Změna rozvržení a úprava záložek

## Úvod
Když čtenáři otevřou velký PDF, výchozí rozvržení prohlížeče může skrolovat nepřetržitě, což ztěžuje soustředění se na jedinou stránku. Nastavením **single page view pdf** vynutíte, aby prohlížeč zobrazoval jednu stránku najednou, což je ideální pro zprávy, e‑knihy a katalogy. V tomto tutoriálu se také naučíte, jak upravit existující záložky PDF, nastavit cíle záložek při vytváření dokumentu a doladit další preference prohlížeče pomocí Aspose.PDF pro Java. Na konci budete mít plnou kontrolu nad navigací, přesností záložek a rozvržením na obrazovce.

**Co se naučíte**
- Jak upravit existující záložky PDF tak, aby ukazovaly na začátek stránky.  
- Jak nastavit cíle záložek při vytváření PDF.  
- Jak změnit preference prohlížeče, například jednostránkové rozvržení.  
- Praktické tipy pro načítání PDF dokumentu v Javě a optimalizaci výkonu.

### Rychlé odpovědi
- **Jaký je hlavní způsob, jak povolit jednostránkové zobrazení PDF?** Call `PdfContentEditor.changeViewerPreference()` with `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Lze cíle záložek upravit po vygenerování PDF?** Yes – load the document, retrieve the outline, and assign a new `ExplicitDestination`.  
- **Potřebuji licenci pro tyto funkce?** A free trial works for evaluation; a full license removes all limitations.  
- **Jaká Maven závislost je vyžadována?** `com.aspose:aspose-pdf:25.3` (or later).  
- **Je to kompatibilní s Java 11 a vyšší?** Absolutely – Aspose.PDF supports Java 8+.

## Co je „change PDF page layout“?
Změna rozvržení stránky PDF řídí, jak jsou stránky zobrazovány v prohlížeči – jednostránkové, kontinuální, dvoustránkové zobrazení atd. Povolení **single page view pdf** zlepšuje čitelnost dlouhých dokumentů a zajišťuje, že každá stránka je zobrazena samostatně, což je zvláště užitečné na mobilních zařízeních a tabletech.

## Proč upravovat záložky PDF a nastavovat cíle záložek?
Záložky fungují jako dynamický obsah. Přesné cíle umožňují čtenářům přejít přímo na požadovanou sekci, čímž se eliminuje nadbytečné skrolování a snižuje frustrace uživatelů. To vede k plynulejší navigaci a vyšší spokojenosti u technických příruček, produktových katalogů a digitálních knih.

## Požadavky
- **Knihovny a závislosti**: Aspose.PDF pro Java v25.3 nebo novější.  
- **Prostředí**: JDK 8 nebo novější, Maven nebo Gradle nástroj pro sestavení.  
- **Znalosti**: Základní programování v Javě a povědomí o konceptech PDF.

## Nastavení Aspose.PDF pro Java
### Instalace pomocí Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Instalace pomocí Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Získání licence**: Začněte s bezplatnou zkušební verzí nebo požádejte o dočasnou licenci pro plný přístup ke všem funkcím. Zvažte zakoupení trvalé licence pro produkční použití.

### Základní inicializace
Třída `Document` je jádrový objekt Aspose.PDF, který představuje PDF soubor v paměti. Po vytvoření instance všechny operace čtení/zápisu probíhají přes tento objekt.  
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

## Průvodce implementací
### Jak změnit rozvržení stránky PDF v Javě
**Přehled**: Upravte preference prohlížeče tak, aby stránky byly zobrazeny podle vašich požadavků.

#### Inicializace PdfContentEditor
`PdfContentEditor` je pomocná třída, která vám umožňuje upravit nastavení prohlížeče bez nutnosti přepisovat celý dokument.  
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Změna preferencí prohlížeče
Aby se povolilo **single page view pdf**, zavolejte `changeViewerPreference()` s odpovídající hodnotou enumu. Tento volání aktualizuje interní slovník preferencí prohlížeče PDF.  
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Uložení aktualizovaného dokumentu
Po úpravě preferencí zavolejte `save()`, aby se změny zapsaly zpět na disk.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

## Jak upravit záložky PDF
**Odpověď**: Aby bylo možné upravit existující záložky, načtěte PDF pomocí `Document`, získejte jeho kolekci osnovy, najděte požadovaný `OutlineItem` a přiřaďte mu novou `ExplicitDestination`, která ukazuje na správnou stránku a souřadnice. Po aktualizaci každé záložky dokument uložte, aby se změny zachovaly. Tím zajistíte, že uživatelé budou přesně nasměrováni na požadované sekce bez nadbytečného skrolování.

#### Přístup k záložkám
`OutlineItemCollection` představuje hierarchický strom záložek. Získejte jej z objektu `Document`, abyste mohli pracovat s jednotlivými položkami.  
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Nastavení nového cíle
`ExplicitDestination` definuje přesnou stránku a umístění, kam má záložka přejít. Přiřaďte ji k vlastnosti `Destination` položky osnovy.  
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Uložení změn
Uložte aktualizovaný strom záložek voláním `document.save()`.  
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

## Jak nastavit cíl záložky při vytváření PDF
**Odpověď**: Při generování PDF můžete vytvářet záložky za běhu vytvořením objektů `OutlineItem`, nastavením jejich názvů a definováním `ExplicitDestination`, která cílí na konkrétní stránku a režim zobrazení. Přidejte každou záložku do kolekce osnovy dokumentu před uložením, aby výsledný soubor obsahoval připravený navigační strom.

#### Vytvoření a konfigurace záložky
`OutlineItem` představuje jedinou položku záložky v osnově PDF. Při tvorbě PDF od nuly vytvořte novou instanci `OutlineItem` a přidejte ji do kolekce osnovy dokumentu.  
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Definování cíle záložky
Použijte `ExplicitDestination.createFitH(page, top)`, aby se pohled umístil na horní část cílové stránky.  
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Přidání a uložení PDF
Nakonec přidejte záložku do osnovy a dokument uložte.  
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Praktické aplikace
1. **Digitální knihy** – Zajistěte, aby každá záložka kapitoly končila na vrcholu stránky pro plynulé čtení.  
2. **Technické příručky** – Přesná navigace pomáhá inženýrům rychle najít sekce, zejména ve velkých PDF.  
3. **Produktové katalogy** – Jednostránkové rozvržení usnadňuje prohlížení katalogů na tabletech.

## Úvahy o výkonu
- **Optimalizace zdrojů**: Aspose.PDF dokáže zpracovávat PDF až do 2 GB, aniž by načítal celý soubor do paměti, díky své streamovací architektuře. Použijte `Document.optimizeResources()`, abyste dále snížili paměťovou zátěž.  
- **Správa paměti v Javě**: Výslovně zavírejte streamy a nechte garbage collector uvolnit objekty po zpracování, aby nedocházelo k únikům paměti.

## Časté problémy a řešení
- **Záložky se neaktualizují**: Ověřte, že upravujete správný index osnovy (`get_Item(1)` odkazuje na první záložku nejvyšší úrovně).  
- **Preference prohlížeče se neaplikují**: Ujistěte se, že po změně preferencí zavoláte `editor.save()`; jinak změny zůstanou jen v paměti.  
- **Licence výjimky**: Zkušební licence může přidávat vodoznaky; pro produkci získejte plnou licenci.

## Často kladené otázky
**Q: Jaký je nejjednodušší způsob, jak načíst PDF dokument v Javě?**  
A: Use `new Document("path/to/file.pdf")`; Aspose.PDF automatically detects the file format.

**Q: Mohu změnit rozvržení stránky bez použití PdfContentEditor?**  
A: Yes, you can set viewer preferences directly on the `Document` object via `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q: Ovlivňuje změna rozvržení prohlížeče tisk?**  
A: Viewer layout only influences on‑screen display; it does not alter the printed output.

**Q: Existují limity na počet záložek, které mohu vytvořit?**  
A: No explicit limit, but extremely large outline trees may impact performance; keep them organized.

**Q: Jak zajistit, aby cíle záložek byly přesné po přidání nebo odebrání stránek?**  
A: Re‑calculate destinations using the current page indices after any structural changes.

## Zdroje
- **Documentation**: [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Download**: [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Purchase**: [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Free Trial**: [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Temporary License**: [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Last Updated:** 2026-05-28  
**Tested With:** Aspose.PDF for Java v25.3  
**Author:** Aspose

## Související tutoriály

- [How to Change PDF Viewer Preferences Using Aspose.PDF for Java: A Comprehensive Guide](/pdf/java/printing-rendering/modify-pdf-viewer-preferences-aspose-pdf-java/)
- [How to Create PDF Bookmarks and Manage Navigation Using Aspose.PDF for Java](/pdf/java/bookmarks-navigation/create-manage-pdf-bookmarks-aspose-java/)
- [PDF Bookmarks and Navigation Tutorials for Aspose.PDF Java](/pdf/java/bookmarks-navigation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}