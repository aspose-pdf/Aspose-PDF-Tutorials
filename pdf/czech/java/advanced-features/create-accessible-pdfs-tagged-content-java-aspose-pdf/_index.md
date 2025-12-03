---
date: '2025-12-01'
description: Naučte se, jak vytvářet přístupné PDF soubory, generovat PDF tabulky
  a označovat PDF pro čtečky obrazovky pomocí Aspise.PDF pro Javu.
keywords:
- accessible PDFs with Java
- Aspose.PDF for Java
- tagged PDF creation
language: cs
title: Vytvořte přístupný PDF s tagovaným obsahem v Javě pomocí Aspose.PDF
url: /java/advanced-features/create-accessible-pdfs-tagged-content-java-aspose-pdf/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Vytvořte přístupný PDF s označeným obsahem v Javě pomocí Aspose.PDF

Vytváření **přístupných PDF** dokumentů je nezbytné pro zajištění, aby všichni uživatelé, včetně těch, kteří spoléhají na asistenční technologie, mohli číst a interagovat s vaším obsahem. V tomto tutoriálu se naučíte, jak **vytvořit přístupné PDF** soubory s označeným obsahem, generovat PDF tabulky a nastavit jazyk dokumentu, aby čtečky obrazovky mohly správně interpretovat strukturu.

## Rychlé odpovědi
- **Jakou knihovnu mám použít?** Aspose.PDF for Java.  
- **Jak dlouho trvá implementace?** Přibližně 15‑20 minut pro základní označený PDF.  
- **Potřebuji licenci?** Bezplatná zkušební verze funguje pro vývoj; pro produkci je vyžadována trvalá licence.  
- **Mohu generovat tabulky?** Ano – API vám umožní vytvářet a stylovat PDF tabulky s označenou strukturou.  
- **Jak zajistit, aby byl PDF čitelný čtečkami obrazovky?** Označte obsah, nastavte jazyk a poskytněte alternativní text pro strukturované prvky.

## Co je „vytvořit přístupný pdf“?
**Přístupný PDF** obsahuje logickou strukturu (značky), která popisuje nadpisy, tabulky, odstavce a další prvky. Tato struktura umožňuje čtečkám obrazovky a dalším asistenčním nástrojům prezentovat dokument smysluplným způsobem uživatelům se zrakovým nebo kognitivním postižením.

## Proč označovat PDF?
Označování PDF (proces **jak označit pdf**) vám poskytuje:
- **Vylepšenou navigaci** pro čtečky obrazovky a uživatele klávesnice.  
- **Soulad** s normami WCAG 2.1 a PDF/UA.  
- **Lepší prohledatelnost** díky sémantickému indexování textu.  

## Předpoklady
Před zahájením se ujistěte, že máte:
- Nainstalovaný Java Development Kit (JDK).  
- IDE, např. IntelliJ IDEA nebo Eclipse.  
- Základní znalosti Javy a povědomí o konceptech PDF.  

### Požadované knihovny a závislosti
Přidejte Aspose.PDF for Java do svého projektu pomocí Maven nebo Gradle.

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Získání licence
Aspose.PDF for Java nabízí bezplatnou zkušební verzi. Dočasnou licenci můžete získat [zde](https://purchase.aspose.com/temporary-license/). Pro produkční použití zakupte plnou licenci.

## Nastavení Aspose.PDF pro Java
Pokud nepoužíváte Maven/Gradle, stáhněte JAR ze [stránky vydání Aspose](https://releases.aspose.com/pdf/java/) a přidejte jej do cesty sestavení vašeho projektu.

Zde je jednoduchý úryvek, který ověří vaše nastavení vytvořením prázdného PDF:

```java
import com.aspose.pdf.Document;

public class PdfCreator {
    public static void main(String[] args) {
        // Initialize Aspose.PDF
        Document doc = new Document();
        
        // Save the empty document to check setup
        doc.save("output/EmptyDocument.pdf");
        
        System.out.println("Setup complete and document created successfully.");
    }
}
```

## Průvodce implementací

### Vytvoření nového PDF s označeným obsahem
**Přehled** – Označený obsah poskytuje logickou hierarchii, která zlepšuje přístupnost. Níže uvedené kroky vás provedou vytvořením PDF, povolením označování a naplněním stylované tabulky.

#### Krok 1: Inicializace dokumentu a povolení označování
Nejprve vytvořte instanci `Document` a získejte rozhraní `ITaggedContent`. Také **nastavíme jazyk PDF** (krok **set pdf language**), aby čtečky obrazovky věděly, v jakém jazyce je dokument.

```java
import com.aspose.pdf.*;

public class TaggedPdfCreator {
    public static void main(String[] args) {
        String outputDir = "YOUR_OUTPUT_DIRECTORY";

        // Create a new PDF document
        Document document = new Document();

        // Obtain tagged content
        ITaggedContent taggedContent = document.getTaggedContent();
        
        // Set the title and language for accessibility purposes
        taggedContent.setTitle("Example table row style");
        taggedContent.setLanguage("en-US");

        // Proceed to add structured elements
    }
}
```

#### Krok 2: Přidání strukturálních prvků (Jak generovat PDF tabulku)
Dále definujte kořenový prvek a vytvořte strukturu tabulky s hlavičkou, tělem a patou. Toto demonstruje funkci **generate pdf table**, přičemž obsah zůstává plně označený.

```java
import com.aspose.pdf.tagged.logicalstructure.elements.bls.*;

// Get root structure element
StructureElement rootElement = taggedContent.getRootElement();

// Create a new table structure element
TableElement tableElement = taggedContent.createTableElement();
rootElement.appendChild(tableElement);

// Add header, body, and footer to the table
TableTHeadElement tableTHeadElement = tableElement.createTHead();
TableTBodyElement tableTBodyElement = tableElement.createTBody();
TableTFootElement tableTFootElement = tableElement.createTFoot();
```

#### Krok 3: Naplnění prvků tabulky (Styling rows for screen reader PDF)
Nyní přidáme řádky, naformátujeme je a poskytneme alternativní text. Alternativní text zajišťuje, že tabulka je srozumitelná pro uživatele **screen reader PDF**.

```java
int rowCount = 7;
int colCount = 3;

// Add a header row with column titles
TableTRElement headTrElement = tableTHeadElement.createTR();
headTrElement.setAlternativeText("Head Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTHElement thElement = headTrElement.createTH();
    thElement.setText(String.format("Head %s", colIndex));
}

// Add rows to the table body with styled cells
for (int rowIndex = 0; rowIndex < rowCount; rowIndex++) {
    TableTRElement trElement = tableTBodyElement.createTR();
    trElement.setAlternativeText(String.format("Row %s", rowIndex));

    // Set row styles
    trElement.setBackgroundColor(Color.getLightSeaGreen());
    trElement.setBorder(new BorderInfo(BorderSide.All, 0.75F, Color.getDarkGray()));
    trElement.setDefaultCellBorder(new BorderInfo(BorderSide.All, 0.50F, Color.getBlue()));
    trElement.setMinRowHeight(100.0);
    trElement.setFixedRowHeight(120.0);

    // Set default text state for cells in this row
    TextState cellTextState = new TextState();
    cellTextState.setForegroundColor(Color.getRed());
    trElement.setDefaultCellTextState(cellTextState);

    // Add cells to the row
    for (int colIndex = 0; colIndex < colCount; colIndex++) {
        TableTDElement tdElement = trElement.createTD();
        tdElement.setText(String.format("Cell [{0}, {1}]", rowIndex, colIndex));
    }
}

// Add a footer row to the table
TableTRElement footTrElement = tableTFootElement.createTR();
footTrElement.setAlternativeText("Foot Row");
for (int colIndex = 0; colIndex < colCount; colIndex++) {
    TableTDElement tdElement = footTrElement.createTD();
    tdElement.setText(String.format("Foot %s", colIndex));
}
```

### Uložení PDF dokumentu
Nakonec dokument uložte. Uložený soubor zachová všechny značky, nastavení jazyka a strukturu tabulky, čímž bude plně připravený **create accessible pdf** k distribuci.

```java
// Save the tagged PDF document
document.save(outputDir + "/StyleTableRow.pdf");
System.out.println("Document saved successfully.");
```

## Praktické aplikace
Vytváření přístupných PDF je klíčové v mnoha reálných scénářích:

1. **Vzdělávací materiály** – Poskytněte inkluzivní učebnice a materiály pro všechny studenty.  
2. **Vládní publikace** – Splňte právní požadavky na přístupnost veřejných dokumentů.  
3. **Firemní zprávy** – Zajistěte, aby akcionáři a zaměstnanci mohli přistupovat k finančním výkazům pomocí čteček obrazovky.  

## Úvahy o výkonu
Při práci s velkými PDF:
- Sledujte využití paměti; uvolňujte zdroje okamžitě.  
- Minimalizujte počet dynamických prvků, které přidáváte.  
- Dodržujte osvědčené postupy Javy pro garbage collection a opětovné použití objektů.  

## Časté problémy a řešení
| Problém | Řešení |
|-------|----------|
| Značky se neobjevují v PDF čtečce | Ověřte, že je získáno `taggedContent` a že jsou před přidáním prvků zavolány `setTitle`/`setLanguage`. |
| Buňky tabulky postrádají alternativní text | Použijte `setAlternativeText` na každém `TableTRElement` a na řádcích hlavičky/paty. |
| Velké soubory způsobují OutOfMemoryError | Zpracovávejte dokument po částech nebo zvyšte velikost haldy JVM (`-Xmx`). |

## Často kladené otázky

**Q: Jak mohu ověřit, že je mé PDF skutečně přístupné?**  
A: Použijte nástroje jako Adobe Acrobat’s Accessibility Checker nebo otevřete soubor pomocí čtečky obrazovky (NVDA, JAWS) a potvrďte správnou navigaci.

**Q: Podporuje Aspose.PDF i jiné jazyky kromě angličtiny?**  
A: Ano. Nastavte kód jazyka pomocí `taggedContent.setLanguage("fr-FR")` pro francouzštinu, `es-ES` pro španělštinu atd.

**Q: Mohu do označeného PDF přidat obrázky s alt textem?**  
A: Rozhodně. Použijte třídu `Image` a nastavte její vlastnost `AlternativeText`, aby popisovala vizuální obsah.

**Q: Existuje limit na počet řádků, které mohu v PDF tabulce generovat?**  
A: Neexistuje pevný limit, ale velmi velké tabulky mohou zvýšit spotřebu paměti; zvažte stránkování nebo rozdělení dokumentu.

**Q: Bude vygenerovaný PDF fungovat se všemi čtečkami obrazovky?**  
A: Pokud jsou značky, jazyk a alternativní text správně nastaveny, PDF splňuje standard PDF/UA a mělo by být čitelné většinou hlavních čteček obrazovky.

## Závěr
Nyní máte kompletní, krok‑za‑krokem průvodce **vytvořením přístupných PDF** dokumentů s označeným obsahem, generováním stylovaných tabulek a zajištěním kompatibility s čtečkami obrazovky. Využitím Aspose.PDF pro Java můžete vložit přístupnost přímo do vašeho pipeline pro generování PDF a poskytovat inkluzivní obsah všem uživatelům.

### Další kroky
- Prozkoumejte další funkce označování, jako jsou nadpisy, seznamy a odkazy.  
- Integrovat tento workflow do vašich existujících Java služeb nebo dávkových úloh.  
- Sdílejte své zkušenosti a ptejte se na [Aspose PDF fóru](https://forum.aspose.com/c/pdf/10).

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.PDF for Java 25.3  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
