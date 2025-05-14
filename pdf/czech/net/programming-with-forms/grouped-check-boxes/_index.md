---
"description": "Naučte se, jak v dokumentu PDF pomocí Aspose.PDF pro .NET vytvářet seskupená zaškrtávací políčka (přepínače)."
"linktitle": "Seskupená zaškrtávací políčka v dokumentu PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Seskupená zaškrtávací políčka v dokumentu PDF"
"url": "/cs/net/programming-with-forms/grouped-check-boxes/"
"weight": 170
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Seskupená zaškrtávací políčka v dokumentu PDF

## Zavedení

Vytváření interaktivních PDF souborů není tak složité, jak by se mohlo zdát, zvláště když máte k dispozici výkonné nástroje, jako je Aspose.PDF pro .NET. Jedním z interaktivních prvků, které můžete potřebovat přidat do svých PDF dokumentů, jsou seskupená zaškrtávací políčka, nebo konkrétněji přepínače, které uživatelům umožňují vybrat jednu možnost z dané sady. Tento tutoriál vás provede procesem přidávání seskupených zaškrtávacích políček (přepínačů) do PDF dokumentu pomocí Aspose.PDF pro .NET. Ať už jste začátečník nebo zkušený vývojář, shledáte tuto příručku poutavou, podrobnou a snadno srozumitelnou.

## Předpoklady

Než se ponoříme do podrobného návodu, pojďme si probrat některé základní předpoklady:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF. Pokud ne, můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/).
2. IDE: Měli byste mít nastavené vývojové prostředí, například Visual Studio.
3. .NET Framework: Projekt by měl cílit na verzi .NET Framework kompatibilní s Aspose.PDF.
4. Základní znalost C#: Pro plynulé sledování je nutná znalost C# a manipulace s PDF.
5. Licence: Aspose.PDF vyžaduje licenci pro plnou funkčnost. Můžete [získat dočasnou licenci](https://purchase.aspose.com/temporary-license/) v případě potřeby.

## Importovat balíčky

Než začnete, ujistěte se, že jste do projektu importovali potřebné jmenné prostory:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Tyto balíčky vám poskytnou přístup ke všem třídám a metodám potřebným pro manipulaci s dokumenty PDF, včetně vytváření přepínačů a definování jejich vlastností.

V této části si rozebereme proces vytváření seskupených zaškrtávacích políček (přepínačů) do jasných a snadno sledovatelných kroků.

## Krok 1: Vytvořte nový dokument PDF

Prvním krokem je vytvoření instance `Document` objekt, který bude reprezentovat váš PDF soubor. Poté do dokumentu přidejte prázdnou stránku, na kterou umístíte seskupená zaškrtávací políčka.

```csharp
// Vytvoření instance objektu Document
Document pdfDocument = new Document();

// Přidání stránky do souboru PDF
Page page = pdfDocument.Pages.Add();
```

Tím se vytvoří základ pro přidávání jakýchkoli prvků, jako jsou například přepínače, do PDF.

## Krok 2: Inicializace pole přepínače

Dále musíme vytvořit `RadioButtonField` objekt, který bude obsahovat seskupená zaškrtávací políčka (přepínače). Toto pole se přidá na konkrétní stránku, kde se zaškrtávací políčka zobrazí.

```csharp
// Vytvořte instanci objektu RadioButtonField a přiřaďte ji k první stránce
RadioButtonField radio = new RadioButtonField(pdfDocument.Pages[1]);
```

Představte si to jako kontejner, který seskupí jednotlivé možnosti přepínačů.

## Krok 3: Přidání možností přepínače

Nyní přidejme do pole jednotlivé možnosti přepínačů. V tomto příkladu přidáme dva přepínače a určíme jejich pozice pomocí `Rectangle` objekt.

```csharp
// Přidat první přepínač a určit jeho polohu pomocí obdélníku
RadioButtonOptionField opt1 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(0, 0, 20, 20));
RadioButtonOptionField opt2 = new RadioButtonOptionField(page, new Aspose.Pdf.Rectangle(100, 0, 120, 20));

// Nastavení názvů možností pro identifikaci
opt1.OptionName = "Option1";
opt2.OptionName = "Option2";
```

Zde, `Rectangle` Objekt definuje souřadnice a velikost každého přepínače na stránce.

## Krok 4: Přizpůsobení stylu přepínačů

Vzhled přepínačů si můžete přizpůsobit nastavením jejich `Style` vlastnost. Můžete například chtít zaškrtávací políčka ve tvaru čtverce nebo kříže.

```csharp
// Nastavení stylu přepínačů
opt1.Style = BoxStyle.Square;
opt2.Style = BoxStyle.Cross;
```

To vám umožňuje ovládat vzhled a dojem z zaškrtávacích políček, díky čemuž jsou uživatelsky přívětivější a vizuálně atraktivnější.

## Krok 5: Konfigurace vlastností ohraničení

Okraje hrají zásadní roli pro snadnou identifikaci zaškrtávacích políček. Zde přidáme plné okraje kolem každé možnosti přepínače a definujeme jejich šířku a barvu.

```csharp
// Konfigurace ohraničení prvního přepínače
opt1.Border = new Border(opt1);
opt1.Border.Style = BorderStyle.Solid;
opt1.Border.Width = 1;
opt1.Characteristics.Border = Color.Black;

// Konfigurace ohraničení druhého přepínače
opt2.Border = new Border(opt2);
opt2.Border.Style = BorderStyle.Solid;
opt2.Border.Width = 1;
opt2.Characteristics.Border = Color.Black;
```

Tento krok zajišťuje, že každý přepínač má dobře definovaný okraj, což zlepšuje čitelnost dokumentu.

## Krok 6: Přidání možností přepínačů do formuláře

Nyní přidáme přepínače do formuláře dokumentu. Toto je poslední krok v seskupení zaškrtávacích políček do jednoho pole.

```csharp
// Přidat pole přepínače do objektu formuláře v dokumentu
pdfDocument.Form.Add(radio);
```

Objekt formuláře funguje jako kontejner pro všechny interaktivní prvky, včetně našich seskupených zaškrtávacích políček.

## Krok 7: Uložení dokumentu PDF

Nakonec, jakmile je vše nastaveno, můžete dokument PDF uložit na požadované místo.

```csharp
// Definujte cestu k výstupnímu souboru
string dataDir = "YOUR DOCUMENT DIRECTORY" + "GroupedCheckBoxes_out.pdf";

// Uložit dokument PDF
pdfDocument.Save(dataDir);

// Potvrzení úspěšného vytvoření
Console.WriteLine("Grouped checkboxes added successfully. File saved at " + dataDir);
```

A to je vše! Úspěšně jste vytvořili PDF se seskupenými zaškrtávacími políčky pomocí Aspose.PDF pro .NET.

## Závěr

Přidávání interaktivních prvků, jako jsou seskupená zaškrtávací políčka, do dokumentů PDF se může zpočátku zdát složité, ale s Aspose.PDF pro .NET se to stane hračkou. Dodržováním tohoto podrobného návodu jste se naučili, jak nastavit základní dokument PDF, přidat seskupená přepínače, přizpůsobit jejich vzhled a uložit konečný výsledek. Ať už vytváříte formuláře, průzkumy nebo jakýkoli jiný typ interaktivního PDF, tento návod vám poskytne solidní základ pro začátek.

## Často kladené otázky

### Mohu do skupiny přidat více než dva přepínače?
Rozhodně! Jednoduše vytvořte další instanci `RadioButtonOptionField` objekty a přidat je do `RadioButtonField` jak je znázorněno v tutoriálu.

### Jak mohu v jednom dokumentu zpracovat více skupin zaškrtávacích políček?
Chcete-li vytvořit více skupin, vytvořte samostatné instance `RadioButtonField` objekty pro každou skupinu.

### Existuje omezení počtu zaškrtávacích políček, která mohu přidat?
Ne, Aspose.PDF pro .NET nestanovuje žádná omezení počtu zaškrtávacích políček, která můžete do PDF přidat.

### Mohu změnit vzhled zaškrtávacích políček po jejich přidání?
Ano, po přidání zaškrtávacích políček můžete upravit vlastnosti, jako je styl ohraničení, šířka a barva.

### Je možné použít obrázky jako přepínače?
Ano, Aspose.PDF umožňuje používat vlastní obrázky jako přepínače nastavením `Appearance` vlastnost každé možnosti přepínače.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}