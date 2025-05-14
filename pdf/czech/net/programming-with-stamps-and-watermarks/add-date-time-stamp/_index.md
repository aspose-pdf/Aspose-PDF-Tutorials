---
"description": "Naučte se, jak přidat datum a časové razítko do souborů PDF pomocí Aspose.PDF pro .NET v tomto podrobném návodu. Ideální pro zvýšení autenticity dokumentů."
"linktitle": "Přidat datum a časové razítko do souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat datum a časové razítko do souboru PDF"
"url": "/cs/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat datum a časové razítko do souboru PDF

## Zavedení

Pokud jde o správu dokumentů, zejména PDF, může přidání datového a časového razítka znamenat zásadní změnu. Ať už pracujete na právních dokumentech, projektových zprávách nebo fakturách, časové razítko nejen dodává autenticitu, ale také poskytuje jasný záznam o tom, kdy byl dokument vytvořen nebo upraven. V této příručce vás provedeme procesem přidání datového a časového razítka do souboru PDF pomocí knihovny Aspose.PDF pro .NET. 

Tento článek je navržen tak, aby byl srozumitelný a snadno srozumitelný, takže i když jste v programování nebo knihovně Aspose.PDF nováčkem, budete schopni tuto funkci s jistotou implementovat. Pojďme se do toho pustit!

## Předpoklady

Než začneme, je třeba splnit několik předpokladů:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Zde budete psát a spouštět svůj kód.
2. Aspose.PDF pro .NET: Je třeba stáhnout a nainstalovat knihovnu Aspose.PDF. Nejnovější verzi naleznete [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům, ale nebojte se, pokud s tím teprve začínáte; vše vám krok za krokem vysvětlíme.
4. Soubor PDF: Mějte připravený vzorový soubor PDF. V našem příkladu použijeme soubor s názvem `AddTextStamp.pdf`.

Jakmile splníte tyto předpoklady, můžete začít přidávat do souborů PDF razítka data a času!

## Importovat balíčky

Pro začátek je potřeba importovat potřebné jmenné prostory do vašeho projektu C#. Zde je návod, jak to udělat:

### Vytvořit nový projekt

1. Otevřete Visual Studio: Spusťte aplikaci Visual Studio.
2. Vytvoření nového projektu: Na úvodní obrazovce vyberte možnost „Vytvořit nový projekt“.
3. Výběr konzolové aplikace: V seznamu šablon projektů vyberte možnost „Konzolová aplikace (.NET Framework)“.
4. Pojmenujte svůj projekt: Pojmenujte svůj projekt, například `PDFDateTimeStamp`.

### Přidat odkaz na Aspose.PDF

1. Klikněte pravým tlačítkem myši na složku „Reference“: V Průzkumníku řešení klikněte pravým tlačítkem myši na složku „Reference“ ve vašem projektu.
2. Vyberte „Přidat referenci“: V kontextové nabídce vyberte možnost „Přidat referenci“.
3. Vyhledejte soubor Aspose.PDF: Přejděte do umístění, kam jste si stáhli soubor Aspose.PDF, a vyberte jej. Kliknutím na tlačítko „OK“ jej přidejte do svého projektu.

### Importovat požadované jmenné prostory

Na vrcholu tvého `Program.cs` soubor, je třeba importovat následující jmenné prostory:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Nyní, když máme vše nastavené, pojďme si rozebrat proces přidání data a časového razítka do souboru PDF do jasných a snadno zvládnutelných kroků.

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba zadat adresář, kde se nachází váš PDF soubor. To je klíčové, protože kód bude PDF hledat v tomto adresáři.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Nahraďte svou skutečnou cestou
```

Nezapomeňte vyměnit `YOUR DOCUMENT DIRECTORY` se skutečnou cestou k vašemu PDF souboru.

## Krok 2: Otevřete dokument PDF

Dále otevřete dokument PDF, do kterého chcete přidat časové razítko. 

```csharp
// Otevřít dokument
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Tento řádek kódu inicializuje `Document` třídu a načte váš PDF soubor do `pdfDocument` objekt.

## Krok 3: Vytvořte datum a časové razítko

Nyní je čas vygenerovat datum a časové razítko. Naformátujete ho tak, aby se zobrazovalo určitým způsobem. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Zde, `DateTime.Now` získá aktuální datum a čas a `ToString` naformátuje jej do požadovaného formátu.

## Krok 4: Vytvořte textové razítko

S připraveným řetězcem data a času můžete nyní vytvořit textové razítko, které bude přidáno do vašeho PDF.

```csharp
// Vytvořit textové razítko
TextStamp textStamp = new TextStamp(annotationText);
```

Tento řádek vytvoří novou instanci třídy `TextStamp` s použitím formátovaného řetězce data a času.

## Krok 5: Nastavení vlastností razítka

Vzhled a umístění razítka si můžete přizpůsobit. Zde je návod, jak nastavit jeho vlastnosti:

```csharp
// Nastavení vlastností razítka
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

V tomto kroku nastavíme okraje a zarovnáme razítko do pravého dolního rohu stránky PDF.

## Krok 6: Přidání razítka do PDF

Nyní je čas přidat textové razítko do dokumentu PDF. 

```csharp
// Přidání známky do sbírky známek
pdfDocument.Pages[1].AddStamp(textStamp);
```

Tento řádek přidá razítko na první stránku PDF. Číslo stránky můžete změnit, pokud chcete razítko umístit na jinou stránku.

## Krok 7: Vytvořte anotaci s volným textem (volitelné)

Pokud chcete k razítku přidat anotaci, můžete vytvořit `FreeTextAnnotation` následovně:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Tento volitelný krok vytvoří anotaci s volným textem, která může poskytnout další kontext nebo informace o razítku.

## Krok 8: Konfigurace ohraničení anotace

Pokud chcete upravit ohraničení anotace, můžete to udělat také:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Tento úryvek kódu nastaví šířku ohraničení na 0, čímž jej skryje, a přidá anotaci do PDF.

## Krok 9: Uložení dokumentu PDF

Nakonec je třeba upravený dokument PDF uložit. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Zadejte název výstupního souboru
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Tento řádek uloží PDF soubor s přidaným časovým razítkem do nového souboru. Výstup si můžete prohlédnout ve vámi zadaném adresáři.

## Závěr

Gratulujeme! Úspěšně jste přidali datum a časové razítko do PDF souboru pomocí Aspose.PDF pro .NET. Tato jednoduchá, ale efektivní funkce může vylepšit vaše dokumenty, učinit je profesionálnějšími a poskytnout jasný záznam o tom, kdy byly vytvořeny nebo upraveny. 

## Často kladené otázky

### Mohu si přizpůsobit formát data v časovém razítku?
Ano, můžete upravit `ToString` způsob změny formátu data podle vašich preferencí.

### Je Aspose.PDF zdarma k použití?
Aspose.PDF nabízí bezplatnou zkušební verzi, ale pro plné funkce je nutné zakoupit licenci. Můžete získat dočasnou licenci. [zde](https://purchase.aspose.com/temporary-license/).

### Mohu do PDF přidat více časových razítek?
Rozhodně! Můžete jich vytvořit více `TextStamp` instance a přidat je na různé stránky nebo pozice v PDF.

### Co když nemám Visual Studio?
Můžete použít libovolné C# IDE nebo textový editor, ale pro spuštění a ladění projektu se doporučuje Visual Studio.

### Kde najdu další příklady použití Aspose.PDF?
Další příklady a návody si můžete prohlédnout v [Dokumentace Aspose.PDF](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}