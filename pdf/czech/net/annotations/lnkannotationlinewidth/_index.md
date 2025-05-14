---
"description": "Naučte se, jak nastavit šířku čáry inkoustových anotací v PDF pomocí Aspose.PDF pro .NET. Tento podrobný tutoriál vás provede jednotlivými kroky a zajistí vám vysoce kvalitní výstup."
"linktitle": "Šířka čáry anotace lnk"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Šířka čáry anotace lnk"
"url": "/cs/net/annotations/lnkannotationlinewidth/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Šířka čáry anotace lnk

## Zavedení

Při práci s dokumenty PDF může být přidávání anotací účinným způsobem, jak zvýraznit informace nebo přidat do souborů interaktivní prvky. Jednou z takových anotací je Inkoustová anotace, která umožňuje kreslit čáry volného tvaru do PDF. Co když ale potřebujete přizpůsobit vzhled těchto čar, zejména jejich šířku? V tomto tutoriálu vás provedeme procesem nastavení šířky čáry inkoustové anotace pomocí Aspose.PDF pro .NET.

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše nastavené pro hladký průběh tohoto tutoriálu:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF pro .NET. Můžete si ji stáhnout z [stránka ke stažení](https://releases.aspose.com/pdf/net/) nebo jej nainstalujte pomocí Správce balíčků NuGet ve Visual Studiu.
2. Vývojové prostředí: Tento tutoriál předpokládá, že pracujete ve vývojovém prostředí .NET, jako je Visual Studio.
3. Základní znalost C#: Základní znalost C# vám pomůže s postupem v kódování.
4. Dokument PDF: Pro tento tutoriál použijte buď existující dokument PDF, nebo vytvořte nový.

## Import nezbytných jmenných prostorů

Než začnete s kódováním, nezapomeňte do projektu importovat potřebné jmenné prostory:

```csharp
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System;
using System.Collections;
using System.Collections.Generic;
```

Tyto jmenné prostory poskytují třídy a metody potřebné pro manipulaci s PDF dokumenty, práci s anotacemi a zpracování grafických prvků.

Nyní, když máme připravené všechny potřebné kroky, si rozdělme proces nastavení šířky čáry inkoustové anotace na jasné a zvládnutelné kroky.

## Krok 1: Inicializace dokumentu PDF

Nejprve musíme vytvořit nebo otevřít dokument PDF. V tomto tutoriálu si ukážeme, jak vytvořit nový dokument PDF od nuly.

```csharp
// Inicializace dokumentu PDF
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Zadejte adresář dokumentů
Document doc = new Document();
doc.Pages.Add(); // Přidání prázdné stránky do dokumentu
```

Zde inicializujeme nový `Document` objekt, který představuje náš PDF soubor. Do tohoto dokumentu pak přidáme prázdnou stránku, se kterou budeme pracovat.

## Krok 2: Vytvořte anotaci rukopisem

Dále vytvoříme samotnou anotaci perem. To zahrnuje definování bodů, které tvoří tahy perem.

```csharp
// Vytvořte anotaci rukopisem
IList<Point[]> inkList = new List<Point[]>();
LineInfo lineInfo = new LineInfo();
lineInfo.VerticeCoordinate = new float[] { 55, 55, 70, 70, 70, 90, 150, 60 };
lineInfo.Visibility = true;
lineInfo.LineColor = Color.Red;
lineInfo.LineWidth = 2;
```

V tomto kroku definujeme `LineInfo` objekt, který obsahuje souřadnice tahů perem, jejich viditelnost, barvu a počáteční šířku čáry. `VerticeCoordinate` Pole obsahuje souřadnice X a Y každého bodu v tahu.

## Krok 3: Převod souřadnic na body

Nyní musíme tyto souřadnice převést na body, které může použít anotace rukopisem.

```csharp
// Převod souřadnic na body
int length = lineInfo.VerticeCoordinate.Length / 2;
Aspose.Pdf.Point[] gesture = new Aspose.Pdf.Point[length];
for (int i = 0; i < length; i++)
{
    gesture[i] = new Aspose.Pdf.Point(lineInfo.VerticeCoordinate[2 * i], lineInfo.VerticeCoordinate[2 * i + 1]);
}

inkList.Add(gesture);
```

Tato smyčka zpracovává pole souřadnic a převádí každou dvojici souřadnic na `Point` objekt, který je poté přidán do našeho `inkList`.

## Krok 4: Přidání anotace rukopisem na stránku PDF

S připravenými body můžeme nyní vytvořit anotaci rukopisu a přidat ji na stránku PDF.

```csharp
// Přidání anotace rukopisem na stránku PDF
InkAnnotation a1 = new InkAnnotation(doc.Pages[1], new Aspose.Pdf.Rectangle(100, 100, 300, 300), inkList);
a1.Subject = "Test";
a1.Title = "Title";
a1.Color = Aspose.Pdf.Color.FromRgb(Color.Green);
```

tomto kroku inicializujeme `InkAnnotation` objekt, specifikující stránku, ohraničující obdélník a seznam bodů. Také nastavíme předmět, název a barvu anotace.

## Krok 5: Přizpůsobení okraje anotace

Pro další úpravu vzhledu naší anotace upravíme vlastnosti jejího ohraničení.

```csharp
// Přizpůsobení okraje anotace
Border border = new Border(a1);
border.Width = 3;
border.Effect = BorderEffect.Cloudy;
border.Dash = new Dash(1, 1);
border.Style = BorderStyle.Solid;
doc.Pages[1].Annotations.Add(a1);
```

Zde vytváříme `Border` objekt pro naši anotaci, nastavení jeho šířky, efektu, čárkovaného vzoru a stylu. Tento krok zajistí, že anotace na stránce PDF vizuálně vynikne.

## Krok 6: Uložení dokumentu PDF

Nakonec, po provedení všech potřebných změn, je čas dokument uložit.

```csharp
// Uložit dokument PDF
dataDir = dataDir + "lnkAnnotationLineWidth_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nInk annotation line width setup successfully.\nFile saved at " + dataDir);
```

Tento kód uloží upravený PDF dokument s anotací rukopisu do zadaného adresáře. `Console.WriteLine` Příkaz potvrzuje úspěšné spuštění kódu.

## Závěr

Gratulujeme! Úspěšně jste vytvořili a upravili rukopisnou anotaci v dokumentu PDF pomocí Aspose.PDF pro .NET. Tento tutoriál pokryl celý proces, od inicializace dokumentu až po uložení finálního souboru. S těmito znalostmi můžete dále prozkoumat rozsáhlé možnosti Aspose.PDF pro .NET a aplikovat podobné techniky na jiné typy anotací nebo manipulací s PDF.

## Často kladené otázky

### Mohu použít různé barvy pro různé části anotace s rukopisem?  
Ano, můžete jich vytvořit více `InkAnnotation` objekty s různými barvami a přidat je na stejné nebo různé stránky PDF.

### Jak mohu dynamicky změnit šířku čáry?  
Můžete upravit `LineWidth` majetek `LineInfo` objektu před převodem souřadnic na body.

### Je možné, aby byla anotace s inkoustem průhledná?  
Ano, můžete upravit `Opacity` majetek `InkAnnotation` objekt, aby byl průhledný.

### Mohu na stejnou stránku přidat více rukopisných poznámek?  
Rozhodně! Na jednu stránku můžete přidat libovolný počet poznámek s rukopisem opakováním tohoto postupu.

### Jak odstraním inkoustovou poznámku z PDF?  
Anotaci můžete odstranit pomocí `doc.Pages[1].Annotations.Delete(a1)` metoda, kde `a1` je váš objekt anotace.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}