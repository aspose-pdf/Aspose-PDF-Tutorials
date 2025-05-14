---
"description": "Naučte se, jak nastavit výchozí písmo v souborech PDF pomocí Aspose.PDF pro .NET v tomto podrobném návodu. Ideální pro vývojáře, kteří chtějí vylepšit dokumenty PDF."
"linktitle": "Nastavení výchozího písma v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavení výchozího písma v souboru PDF"
"url": "/cs/net/programming-with-document/setdefaultfont/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení výchozího písma v souboru PDF

## Zavedení

Už se vám někdy stalo, že jste otevřeli dokument PDF a zjistili, že fonty chybí nebo se nezobrazují správně? Může to být frustrující, že? Nebojte se! V tomto tutoriálu se ponoříme do toho, jak nastavit výchozí písmo v souboru PDF pomocí Aspose.PDF pro .NET. Tato výkonná knihovna vám umožňuje snadno manipulovat s dokumenty PDF a nastavení výchozího písma je jen jednou z mnoha funkcí, které nabízí. Takže, vezměte si programátorskou čepici a pojďme na to!

## Předpoklady

Než se pustíme do kódu, je třeba mít připraveno několik věcí:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Je to nejlepší IDE pro vývoj v .NET.
2. Aspose.PDF pro .NET: Budete si muset stáhnout a nainstalovat knihovnu Aspose.PDF. Najdete ji [zde](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Trocha znalosti programování v C# vám hodně pomůže porozumět příkladům, které budeme probírat.

## Importovat balíčky

Chcete-li začít, budete muset importovat potřebné balíčky do svého projektu C#. Zde je návod, jak to udělat:

1. Otevřete svůj projekt ve Visual Studiu.
2. V Průzkumníku řešení klikněte pravým tlačítkem myši na svůj projekt a vyberte možnost „Spravovat balíčky NuGet“.
3. Hledat `Aspose.PDF` a nainstalujte nejnovější verzi.

Jakmile máte balíček nainstalovaný, můžete začít s kódováním!

## Krok 1: Nastavení projektu

### Vytvořit nový projekt

Nejdříve si vytvořme nový projekt v C# ve Visual Studiu:

- Otevřete Visual Studio a vyberte „Vytvořit nový projekt“.
- Vyberte „Konzolová aplikace (.NET Core)“ a klikněte na „Další“.
- Pojmenujte svůj projekt (např. `AsposePdfExample`) a klikněte na tlačítko „Vytvořit“.

### Přidat pomocí direktiv

Nyní přidejme potřebné direktivy using na začátek vašeho `Program.cs` soubor:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System.IO;
```

Tyto direktivy vám umožní přístup ke třídám a metodám Aspose.PDF.

## Krok 2: Načtěte dokument PDF

### Zadejte cestu k dokumentu

Dále budete muset zadat cestu k PDF dokumentu, se kterým chcete pracovat. Zde je návod, jak to udělat:

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Nahraďte svým skutečným adresářem
string documentName = Path.Combine(dataDir, "input.pdf");
```

Nezapomeňte vyměnit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kde se nachází váš PDF soubor.

### Načíst dokument

Nyní si načtěme existující PDF dokument:

```csharp
using (FileStream fs = new FileStream(documentName, FileMode.Open))
{
    Document document = new Document(fs);
}
```

Tento úryvek kódu otevře soubor PDF a vytvoří `Document` objekt, se kterým můžete manipulovat.

## Krok 3: Nastavení výchozího písma

### Možnosti uložení ve formátu PDF

A teď přichází ta vzrušující část! Budete muset vytvořit instanci `PdfSaveOptions` Chcete-li zadat výchozí písmo:

```csharp
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
```

### Zadejte výchozí název písma

Dále nastavíte výchozí název písma. V tomto příkladu použijeme „Arial“:

```csharp
pdfSaveOptions.DefaultFontName = "Arial";
```

Tento řádek říká Aspose.PDF, aby použil Arial jako výchozí písmo pro jakýkoli text, který nemá zadané písmo.

## Krok 4: Uložte dokument

Konečně je čas uložit upravený dokument PDF s novým výchozím písmem:

```csharp
document.Save(Path.Combine(dataDir, "output_out.pdf"), pdfSaveOptions);
```

Tento řádek uloží dokument jako `output_out.pdf` v zadaném adresáři.

## Závěr

A tady to máte! Úspěšně jste nastavili výchozí písmo v souboru PDF pomocí Aspose.PDF pro .NET. Tato jednoduchá, ale výkonná funkce vám pomůže zajistit, aby vaše dokumenty vypadaly přesně tak, jak chcete, i když v nich chybí písma. Takže až příště narazíte na PDF s problémy s písmy, budete přesně vědět, co dělat!

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům programově vytvářet, manipulovat a převádět PDF dokumenty.

### Mohu použít i jiná písma kromě Arialu?
Ano, jako výchozí písmo můžete zadat libovolné písmo nainstalované ve vašem systému.

### Je Aspose.PDF zdarma k použití?
Aspose.PDF nabízí bezplatnou zkušební verzi, ale pro plnou funkčnost si budete muset zakoupit licenci.

### Kde najdu další dokumentaci?
Najdete zde komplexní dokumentaci [zde](https://reference.aspose.com/pdf/net/).

### Jak získám podporu pro Aspose.PDF?
Podporu můžete získat prostřednictvím fóra Aspose [zde](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}