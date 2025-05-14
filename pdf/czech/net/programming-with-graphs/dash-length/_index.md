---
"description": "Naučte se, jak přizpůsobit vzory čárově-čerchovaných čar v PDF pomocí Aspose.PDF pro .NET s naším podrobným návodem. Ideální pro přidání stylu do vašich dokumentů."
"linktitle": "Délka pomlčky"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Délka pomlčky"
"url": "/cs/net/programming-with-graphs/dash-length/"
"weight": 70
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Délka pomlčky

## Zavedení

Chcete do svých PDF dokumentů vnést trochu kreativity úpravou čar pomocí různých čárkovaných vzorů? S Aspose.PDF pro .NET můžete snadno upravovat styly čar tak, aby vyhovovaly potřebám vašeho dokumentu. V tomto tutoriálu se podíváme na to, jak upravit délku čárkovaných čar v PDF dokumentu pomocí Aspose.PDF pro .NET. Ať už chcete čárkovanou nebo tečkovanou čáru, tento průvodce vám poskytne nástroje a kroky potřebné k dosažení požadovaného výsledku.

## Předpoklady

Než se pustíte do tutoriálu, budete potřebovat několik věcí:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovaný soubor Aspose.PDF pro .NET. Pokud jej ještě nemáte nainstalovaný, můžete si jej stáhnout z [Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/).
2. Základní znalost C#: Tento tutoriál předpokládá, že máte základní znalosti programování v C#. Pokud s C# začínáte, možná si budete chtít nejprve osvěžit základy.
3. Visual Studio: I když můžete použít jakékoli vývojové prostředí (IDE), tato příručka předpokládá, že pro psaní a spouštění kódu C# používáte Visual Studio.
4. Účet Aspose: Další zdroje a podporu získáte, pokud máte účet u Aspose. Můžete se zaregistrovat [bezplatná zkušební verze](https://releases.aspose.com/) nebo si zakoupit licenci [zde](https://purchase.aspose.com/buy).

## Importovat balíčky

Abyste mohli začít pracovat s Aspose.PDF pro .NET, budete muset importovat příslušné jmenné prostory. Zde je návod, jak to udělat:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Tyto jmenné prostory zahrnují třídy a metody potřebné pro práci s PDF dokumenty, výkresy a čarami.

## Krok 1: Nastavení projektu

Než začnete s kódováním, vytvořte nový projekt C# ve Visual Studiu. Přidejte do projektu knihovnu Aspose.PDF pro .NET pomocí NuGetu nebo ručním odkazováním na DLL. 

## Krok 2: Inicializace dokumentu

Začněte vytvořením nového dokumentu PDF a přidáním stránky do něj. Toto je plátno, na kterém budete kreslit čáry.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Vytvoření instance dokumentu
Document doc = new Document();

// Přidat stránku do kolekce stránek objektu Document
Page page = doc.Pages.Add();
```

Zde vytváříme `Document` objekt a přidat nový `Page` k tomu. Tím se vytvoří základ pro stanovení vaší hranice.

## Krok 3: Vytvořte objekt kresby

Dále vytvořte `Graph` objekt, který představuje oblast, kde budete kreslit. Definujte jeho rozměry podle vašich požadavků.

```csharp
// Vytvořit objekt kresby s určitými rozměry
Aspose.Pdf.Drawing.Graph canvas = new Aspose.Pdf.Drawing.Graph(100.0, 400.0);

// Přidat objekt kresby do kolekce odstavců instance stránky
page.Paragraphs.Add(canvas);
```

Ten/Ta/To `Graph` Objekt funguje jako kontejner pro prvky výkresu. Zde je nastaven na šířku 100 jednotek a výšku 400 jednotek.

## Krok 4: Definujte čáru

Nyní je čas vytvořit `Line` objekt. Zadejte počáteční a koncový bod čáry a upravte její styl.

```csharp
// Vytvořit objekt Line
Aspose.Pdf.Drawing.Line line = new Aspose.Pdf.Drawing.Line(new float[] { 100, 100, 200, 100 });
```

Tato čára začíná na souřadnicích (100, 100) a končí na (200, 100). Tyto souřadnice můžete upravit podle svých specifických potřeb.

## Krok 5: Úprava stylu čáry

Nastavte barvu a čárkovaný vzor čáry. Zde můžete čáru zvýraznit.

```csharp
// Nastavení barvy pro objekt Čára
line.GraphInfo.Color = Aspose.Pdf.Color.Red;

// Zadejte pole pomlček pro objekt čáry
line.GraphInfo.DashArray = new int[] { 0, 1, 0 };

// Nastavení fáze pomlčky pro instanci čáry
line.GraphInfo.DashPhase = 1;
```

- `line.GraphInfo.Color`: Nastavuje barvu čáry. V tomto případě je červená.
- `line.GraphInfo.DashArray`: Definuje čárkovaný vzor. Zde, `{ 0, 1, 0 }` představuje přerušovaný vzor.
- `line.GraphInfo.DashPhase`: Upraví počáteční bod čárkovaného vzoru.

## Krok 6: Přidání čáry do výkresu

S upraveným stylem čáry ji přidejte do `Graph` objekt.

```csharp
// Přidat čáru do kolekce tvarů nakresleného objektu
canvas.Shapes.Add(line);
```

Tím se čára integruje do vašeho kreslicího plátna.

## Krok 7: Uložte dokument

Nakonec uložte dokument do zadané složky. Zde bude vytvořen soubor PDF.

```csharp
dataDir = dataDir + "DashLength_out.pdf";

// Uložit PDF dokument
doc.Save(dataDir);
Console.WriteLine("\nLength dashed successfully in black and white.\nFile saved at " + dataDir);
```

Tento řádek kódu uloží dokument PDF a zobrazí potvrzovací zprávu s uvedením místa uložení souboru.

## Závěr

Úprava stylů čar v dokumentech PDF může dodat vašim zprávám, prezentacím a dalším dokumentům profesionální nádech. Dodržováním tohoto tutoriálu jste se naučili, jak upravit délku čárkování pomocí Aspose.PDF pro .NET. Ať už vytváříte jednoduché čárkované čáry nebo složitější vzory, Aspose.PDF poskytuje flexibilitu, kterou potřebujete k tomu, aby vaše dokumenty vynikly. Experimentujte s různými vzory a barvami čárkování, abyste našli styl, který nejlépe vyhovuje vašim potřebám.

## Často kladené otázky

### Jak nainstaluji Aspose.PDF pro .NET?
Můžete si ho nainstalovat přes NuGet ve Visual Studiu nebo si ho stáhnout z [Webové stránky společnosti Aspose](https://releases.aspose.com/pdf/net/).

### Mohu používat Aspose.PDF pro .NET zdarma?
Ano, Aspose nabízí [bezplatná zkušební verze](https://releases.aspose.com/) abyste si mohli vyzkoušet jeho funkce před zakoupením licence.

### Jaké další úpravy mohu provést u řádků v PDF?
Můžete upravit tloušťku, barvu a čárkovací vzory čar. Viz [dokumentace](https://reference.aspose.com/pdf/net/) pro více informací.

### Jak mohu získat podporu, pokud narazím na problémy?
Podporu můžete získat prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

### Kde si mohu zakoupit licenci pro Aspose.PDF pro .NET?
Můžete si zakoupit licenci [zde](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}