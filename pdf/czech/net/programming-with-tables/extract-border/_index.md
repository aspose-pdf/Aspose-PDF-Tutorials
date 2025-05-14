---
"description": "Naučte se, jak extrahovat ohraničení ze souboru PDF a uložit je jako obrázek pomocí Aspose.PDF pro .NET. Podrobný návod s ukázkami kódu a tipy pro úspěch."
"linktitle": "Extrahovat okraj v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Extrahovat okraj v souboru PDF"
"url": "/cs/net/programming-with-tables/extract-border/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat okraj v souboru PDF

## Zavedení

Při práci s PDF soubory se může extrakce specifických prvků, jako jsou ohraničení nebo grafické cesty, zdát jako náročný úkol. S Aspose.PDF pro .NET však můžete snadno extrahovat ohraničení nebo tvary ze souboru PDF a uložit je jako obrázek. V tomto tutoriálu se ponoříme do procesu extrakce ohraničení z PDF a jeho uložení jako obrázku PNG. Připravte se převzít kontrolu nad grafickým obsahem vašeho PDF!

## Předpoklady

Než se pustíme do kódu, ujistěte se, že máte vše nastavené:

1. Aspose.PDF pro .NET: Pokud jste si ještě nenainstalovali knihovnu Aspose.PDF, můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/)Budete také muset použít licenci, a to buď prostřednictvím bezplatné zkušební verze, nebo zakoupené licence.
2. Nastavení IDE: Vytvořte projekt C# ve Visual Studiu nebo jakémkoli jiném IDE .NET. Ujistěte se, že jste přidali potřebné odkazy na knihovnu Aspose.PDF.
3. Vstupní PDF soubor: Připravte si PDF soubor, ze kterého budete extrahovat okraje. Tento tutoriál bude odkazovat na soubor s názvem `input.pdf`.

## Import požadovaných balíčků

Začněme importem požadovaných jmenných prostorů. Tyto balíčky poskytují nástroje potřebné k manipulaci s obsahem PDF.

```csharp
using System.IO;
using System;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;
using System.Collections;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
```

Nyní, když máme základy probrány, pojďme k podrobnému návodu, kde si rozebereme každou část kódu a podrobně ji vysvětlíme.


## Krok 1: Načtení dokumentu PDF

Prvním krokem je načtení PDF dokumentu, který obsahuje okraj, který chcete vyjmout. Představte si to jako otevření knihy před začátkem čtení – potřebujete přístup k obsahu!

Začneme tím, že zadáme adresář, kde je uložen váš PDF soubor, a načteme dokument pomocí `Aspose.Pdf.Document` třída.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Document doc = new Document(dataDir + "input.pdf");
```

Tento kód načte `input.pdf` soubor ze zadaného adresáře. Ujistěte se, že cesta k souboru je správná, jinak se může zobrazit chyba „soubor nebyl nalezen“.

## Krok 2: Nastavení grafiky a bitmapy

Než začneme s extrakcí, musíme si vytvořit plátno, na které budeme kreslit. Ve světě .NET to znamená nastavení objektů Bitmap a Graphics. Bitmap představuje obrázek a objekt Graphics nám umožní kreslit tvary, například ohraničení, extrahované z PDF.

```csharp
System.Drawing.Bitmap bitmap = new System.Drawing.Bitmap((int)doc.Pages[1].PageInfo.Width, (int)doc.Pages[1].PageInfo.Height);
System.Drawing.Drawing2D.GraphicsPath graphicsPath = new System.Drawing.Drawing2D.GraphicsPath();
System.Drawing.Drawing2D.Matrix lastCTM = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, 0);
System.Drawing.Drawing2D.Matrix inversionMatrix = new System.Drawing.Drawing2D.Matrix(1, 0, 0, -1, 0, (float)doc.Pages[1].PageInfo.Height);
System.Drawing.PointF lastPoint = new System.Drawing.PointF(0, 0);
System.Drawing.Color fillColor = System.Drawing.Color.FromArgb(0, 0, 0);
System.Drawing.Color strokeColor = System.Drawing.Color.FromArgb(0, 0, 0);
```

Zde je rozpis:
- Vytvoříme bitmapový obrázek o velikosti první stránky PDF.
- GraphicsPath se používá k definování tvarů (v tomto případě ohraničení).
- Matice definuje, jak bude grafika transformována; potřebujeme inverzní matici, protože PDF a .NET mají odlišné souřadnicové systémy.

## Krok 3: Zpracování obsahu PDF


Soubor PDF je řadou kreslicích příkazů a my musíme zpracovat každý z těchto příkazů, abychom identifikovali a extrahovali informace o ohraničení.

```csharp
foreach (Operator op in doc.Pages[1].Contents)
{
    // Zpracování příkazů, jako je ukládání/obnovení stavu, kreslení čar, vyplňování tvarů atd.
}
```

Kód prochází každým operátorem kreslení v proudu obsahu PDF. Každý operátor může představovat čáru, obdélník nebo jinou grafickou instrukci.

## Krok 4: Zpracování operátorů PDF

Každý operátor v souboru PDF řídí akci. Pro vyjmutí ohraničení musíme identifikovat příkazy jako „přesunout na“, „čára na“ a „nakreslit obdélník“. Tyto akce zvládají následující operátory:

- Přesunout na: Přesune kurzor na počáteční bod.
- ČáraK: Nakreslí čáru z aktuálního bodu do nového bodu.
- Re: Nakreslí obdélník (může být součástí ohraničení).

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

V tomto kroku:
- Body zachytíme pro každou nakreslenou čáru nebo tvar.
- Pro obdélníky (`opRe`), přidáme je přímo do `graphicsPath`, který později použijeme k nakreslení ohraničení.

## Krok 5: Nakreslení okraje

Jakmile identifikujeme čáry a obdélníky, které tvoří ohraničení, musíme je nakreslit na objekt Bitmap. Zde přichází na řadu objekt Graphics.

```csharp
using (System.Drawing.Graphics gr = System.Drawing.Graphics.FromImage(bitmap))
{
    gr.SmoothingMode = SmoothingMode.HighQuality;
    gr.DrawPath(new System.Drawing.Pen(strokeColor), graphicsPath);
}
```

- Na základě bitmapy vytvoříme objekt Graphics.
- SmoothingMode.HighQuality zajišťuje pěkný hladký obraz.
- Nakonec použijeme DrawPath k nakreslení ohraničení.

## Krok 6: Uložení extrahovaného okraje

Nyní, když jsme vyjmuli okraj, je čas jej uložit jako obrazový soubor. Tím se okraj uloží jako PNG.

```csharp
dataDir = dataDir + "ExtractBorder_out.png";
bitmap.Save(dataDir, ImageFormat.Png);
```

- Bitmapa se uloží jako obrázek PNG.
- Nyní můžete tento obrázek otevřít a zobrazit si extrahovaný okraj.

## Závěr

Extrakce okrajů ze souboru PDF pomocí Aspose.PDF pro .NET se může zpočátku zdát složitá, ale jakmile si ji rozeberete, stane se snadnou. Pochopením operátorů kreslení v PDF a využitím výkonných knihoven .NET můžete efektivně manipulovat s grafickým obsahem a extrahovat ho. Tato příručka vám poskytne robustní základ pro začátek manipulace s PDF!

## Často kladené otázky

### Jak zpracuji více stránek v PDF?  
Každou stránku v dokumentu můžete procházet iterací. `doc.Pages` místo pevného kódování `doc.Pages[1]`.

### Mohu stejným způsobem extrahovat další prvky, například text?  
Ano, Aspose.PDF poskytuje bohatá API pro extrakci textu, obrázků a dalšího obsahu ze souborů PDF.

### Jak si mohu požádat o licenci, abych se vyhnul omezením?  
Můžeš [požádat o licenci](https://purchase.aspose.com/temporary-license/) načtením přes `License` kurz poskytovaný společností Aspose.

### Co když můj PDF soubor nemá okraje?  
Pokud váš PDF neobsahuje žádné viditelné okraje, proces extrakce grafiky nemusí přinést žádný výsledek. Ujistěte se, že obsah PDF obsahuje kreslitelné okraje.

### Mohu uložit výstup v jiném formátu než PNG?  
Ano, stačí změnit `ImageFormat.Png` do jiného podporovaného formátu, jako například `ImageFormat.Jpeg`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}