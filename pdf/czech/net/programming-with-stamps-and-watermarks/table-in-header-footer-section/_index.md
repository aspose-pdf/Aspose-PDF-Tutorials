---
"description": "Naučte se, jak přidat tabulku do záhlaví/zápatí dokumentu PDF pomocí Aspose.PDF pro .NET."
"linktitle": "Tabulka v sekci záhlaví a zápatí"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Tabulka v sekci záhlaví a zápatí"
"url": "/cs/net/programming-with-stamps-and-watermarks/table-in-header-footer-section/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tabulka v sekci záhlaví a zápatí

## Zavedení

Už jste se někdy přistihli, že zíráte na obyčejný PDF dokument a přáli si, aby měl tenhle extra šmrnc? Máte štěstí! Aspose.PDF pro .NET vám umožňuje vytvářet a manipulovat s PDF soubory jako profesionál. Dnes se ponoříme do praktické funkce, která vám umožní přidat tabulku do záhlaví PDF dokumentu. Nejenže se naučíte, jak na to, ale já vás krok za krokem provedu celým procesem, aby byl co nejplynulejší. 🎉

## Předpoklady

Než se pustíme do samotného kódování, ujistěte se, že máte vše, co potřebujete k zahájení. Zde je to, co budete potřebovat:

1. Visual Studio: Ujistěte se, že máte v počítači nainstalované Visual Studio. Pokud ho nemáte, můžete si ho stáhnout z [Stránky společnosti Microsoft](https://visualstudio.microsoft.com/).
2. Knihovna Aspose.PDF: Musíte mít knihovnu Aspose.PDF pro .NET. K jejímu získání můžete použít následující odkaz. [Aspose.PDF pro balíček .NET](https://releases.aspose.com/pdf/net/).
3. Základní znalost C#: Měli byste mít alespoň základní znalosti C#. Nebojte se, pokud se stále učíte; budu se snažit vše co nejjednodušší!

## Importovat balíčky

Dobře, čas si vyhrnout rukávy a pustit se do programování! Nejdříve si ale musíme nastavit naše prostředí importem potřebných balíčků. Zde je návod, jak to udělat:

###  Otevřete svůj projekt
Otevřete projekt Visual Studia, ve kterém budete pracovat na vytváření PDF souboru. 

###  Přidat odkaz na Aspose.PDF
1. Správce balíčků NuGet: V Průzkumníku řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost „Spravovat balíčky NuGet“.
2. Vyhledejte Aspose.PDF: Do vyhledávacího řádku zadejte „Aspose.PDF“ a nainstalujte balíček.

Na konci tohoto kroku byste měli mít vše nastavené a připravené k zahájení kódování!

A teď se pojďme pustit do kódování! Postupujte podle těchto kroků a vytvořte tabulku v záhlaví PDF souboru:

## Krok 1: Nastavení cesty k adresáři dokumentů

Než začneme vytvářet PDF, musíme si určit, kam bude náš dokument uložen. Postupujte takto:

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Změňte toto na váš skutečný adresář
```

Nahradit `YOUR DOCUMENT DIRECTORY` s cestou, kam chcete PDF uložit. Může to být kdekoli ve vašem systému – jen se ujistěte, že je to přístupné!

## Krok 2: Vytvoření instance dokumentu

Dále vytvoříme nový PDF dokument.

```csharp
// Vytvoření instance Document voláním prázdného konstruktoru
Aspose.Pdf.Document pdfDocument = new Aspose.Pdf.Document();
```

Zde vytvoříme prázdný PDF dokument, do kterého přidáme všechny naše potřebné informace.

## Krok 3: Vytvořte novou stránku

Přidejme do našeho dokumentu novou stránku. 

```csharp
// Vytvořte stránku v dokumentu PDF
Aspose.Pdf.Page page = pdfDocument.Pages.Add();
```

Představte si tuto stránku jako prázdné plátno, na kterém budeme malovat naše mistrovské dílo!

## Krok 4: Vytvořte záhlaví

Nyní si vytvoříme záhlaví pro náš PDF soubor.

```csharp
// Vytvořte záhlaví souboru PDF
Aspose.Pdf.HeaderFooter header = new Aspose.Pdf.HeaderFooter();
```

Tato hlavička bude obsahovat naši tabulku. 

## Krok 5: Přiřaďte záhlaví stránce

Dále se chceme ujistit, že se naše záhlaví zobrazuje na stránce.

```csharp
// Nastavení záhlaví lichých znaků pro soubor PDF
page.Header = header;
```

## Krok 6: Nastavení horního okraje

Abychom zajistili, že naše hlavička má v horní části nějaký prostor pro dýchání, upravme okraj.

```csharp
// Nastavení horního okraje pro záhlaví
header.Margin.Top = 20;
```

Nastavení okraje je jako dát textu osobní prostor – nikdo nemá rád stísněné prostory!

## Krok 7: Vytvořte tabulku

Nyní je čas vytvořit tabulku, která se zobrazí v naší hlavičce.

```csharp
// Vytvoření instance objektu tabulky
Aspose.Pdf.Table tab1 = new Aspose.Pdf.Table();
```

## Krok 8: Přidání tabulky do záhlaví

Nově vytvořenou tabulku přidáme do kolekce odstavců v záhlaví.

```csharp
// Přidejte tabulku do kolekce odstavců požadované sekce
header.Paragraphs.Add(tab1);
```

## Krok 9: Nastavení ohraničení buněk

Dáme naší tabulce určitou strukturu definováním výchozího ohraničení buňky.

```csharp
// Nastavení výchozího ohraničení buňky pomocí objektu BorderInfo
tab1.DefaultCellBorder = new Aspose.Pdf.BorderInfo(Aspose.Pdf.BorderSide.All, 0.1F);
```

## Krok 10: Definování šířky sloupců

Můžete určit, jak široký by měl být každý sloupec tabulky.

```csharp
// Nastavit šířky sloupců tabulky
tab1.ColumnWidths = "60 300";
```

Hodnoty představují šířku každého sloupce v bodech. Neváhejte je upravit podle svých potřeb!

## Krok 11: Vytvoření řádků a přidání buněk

Je čas přidat nějaké řádky a buňky! 

```csharp
// Vytvořte řádky v tabulce a poté buňky v řádcích
Aspose.Pdf.Row row1 = tab1.Rows.Add();
row1.Cells.Add("Table in Header Section");
row1.BackgroundColor = Color.Gray;
```

Tím se vytvoří první řádek s buňkou obsahující text a nastaví se barva pozadí na šedou.

## Krok 12: Nastavení rozpětí řádků a stylu textu

Chcete, aby váš řádek zabíral více sloupců? Zde je postup:

```csharp
// Nastavte hodnotu rozpětí řádku pro první řádek na 2
tab1.Rows[0].Cells[0].ColSpan = 2;
tab1.Rows[0].Cells[0].DefaultCellTextState.ForegroundColor = Color.Cyan;
tab1.Rows[0].Cells[0].DefaultCellTextState.Font = FontRepository.FindFont("Helvetica");
```

Tento krok nejen nastaví rozpětí řádků, ale také změní barvu textu a písmo.

## Krok 13: Přidání druhého řádku

Přidejme do tabulky další řádek, ano?

```csharp
// Vytvořte v tabulce další řádek
Aspose.Pdf.Row row2 = tab1.Rows.Add();

// Nastavení barvy pozadí pro řádek 2
row2.BackgroundColor = Color.White;
```

## Krok 14: Přidání obrázku do druhého řádku

Teď tam přidáme logo, aby náš stůl vypadal elegantně!

```csharp
// Přidejte buňku, která obsahuje obrázek
Aspose.Pdf.Image img = new Aspose.Pdf.Image();
img.File = dataDir + "aspose-logo.jpg"; // Nezapomeňte umístit obrázek do adresáře
```

Nezapomeňte vyměnit `"aspose-logo.jpg"` se skutečným názvem vašeho obrázku!

## Krok 15: Úprava šířky obrázku

Nastavte šířku obrázku tak, aby v buňce vypadal přesně.

```csharp
// Nastavte šířku obrázku na 60
img.FixWidth = 60;

// Přidat obrázek do buňky tabulky
Aspose.Pdf.Cell cell2 = row2.Cells.Add();
cell2.Paragraphs.Add(img);
```

## Krok 16: Přidání textu do druhé buňky

Je čas přidat krátký text vedle našeho loga!

```csharp
row2.Cells.Add("Logo is looking fine !");
row2.Cells[1].DefaultCellTextState.Font = FontRepository.FindFont("Helvetica");
```

## Krok 17: Zarovnání textu svisle a vodorovně

Ujistěte se, že vše vypadá úhledně. Zarovnejte text!

```csharp
// Nastavit svislé zarovnání textu na střed
row2.Cells[1].VerticalAlignment = Aspose.Pdf.VerticalAlignment.Center;
row2.Cells[1].Alignment = Aspose.Pdf.HorizontalAlignment.Center;
```

## Krok 18: Uložení dokumentu PDF

V neposlední řadě si pojďme zachránit náš výtvor!

```csharp
// Uložit soubor PDF
pdfDocument.Save(dataDir + "TableInHeaderFooterSection_out.pdf");
```

voilà! Vytvořili jste úžasný PDF soubor s tabulkou v záhlaví!

## Závěr

A tady to máte! Úspěšně jste přidali tabulku do záhlaví vašeho PDF dokumentu pomocí Aspose.PDF pro .NET. Je úžasné, jak jen pár řádků kódu dokáže proměnit jednoduchý PDF v profesionálně vypadající dokument. Ať už připravujete zprávy, faktury nebo prezentace, přidání špetky kreativity může mít zásadní význam. 

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je výkonná knihovna, která umožňuje vývojářům programově vytvářet a manipulovat s PDF dokumenty.

### Potřebuji licenci k používání Aspose.PDF?
I když můžete knihovnu používat zdarma během zkušební doby, pro delší používání je vyžadována licence. Můžete získat [dočasná licence](https://purchase.aspose.com/temporary-license/) pro hodnocení.

### Kde najdu dokumentaci?
Komplexní dokumentaci a příklady naleznete na [Stránka s dokumentací Aspose.PDF](https://reference.aspose.com/pdf/net/).

### Jak mohu kontaktovat podporu s technickými problémy?
O podporu se můžete obrátit prostřednictvím [Fórum Aspose](https://forum.aspose.com/c/pdf/10).

### Mohu vytvářet tabulky v jiných částech PDF?
Rozhodně! Tabulky můžete vytvářet i v zápatích a sekcích těla; stačí postupovat podle podobných kroků.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}