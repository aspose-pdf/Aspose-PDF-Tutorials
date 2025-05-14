---
"description": "Naučte se, jak nastavit popisky přepínačů v PDF pomocí Aspose.PDF pro .NET. Tato podrobná příručka vás provede načítáním, úpravou a ukládáním formulářů PDF."
"linktitle": "Nastavit popisek přepínače"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Nastavit popisek přepínače"
"url": "/cs/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Nastavit popisek přepínače

## Zavedení

Pokud se pouštíte do manipulace s PDF soubory pomocí Aspose.PDF pro .NET, čeká vás lahůdka! Dnes se zaměříme na praktickou funkci: nastavení popisků přepínačů ve vašich PDF formulářích. Přepínače jsou nezbytné pro uživatelské formuláře, kde potřebujete vybrat z nabídky možností. Představte si je jako otázky s výběrem odpovědí, kde je povolena pouze jedna odpověď. Tento tutoriál vás provede procesem aktualizace popisků přepínačů ve formuláři PDF, aby vaše dokumenty byly interaktivní a uživatelsky přívětivé. 

## Předpoklady

Než se ponoříte do kódu, je třeba se ujistit, že máte několik věcí:

1. Aspose.PDF pro .NET: Ujistěte se, že máte nainstalovanou knihovnu Aspose.PDF. Tato knihovna vám pomůže programově manipulovat se soubory PDF.
2. Vývojové prostředí: Měli byste mít nastavené vývojové prostředí .NET, například Visual Studio.
3. Ukázkový formulář PDF: Pro tento tutoriál budete potřebovat ukázkový formulář PDF s přepínači. Můžete použít libovolný existující formulář PDF nebo vytvořit nový s přepínači.
4. Základní znalost jazyka C#: Tato příručka předpokládá, že máte základní znalosti programovacích konceptů v jazyce C# a .NET.

Pokud jste si ještě nenainstalovali Aspose.PDF pro .NET nebo potřebujete dočasnou licenci, můžete [stáhněte si to zde](https://releases.aspose.com/pdf/net/) nebo [získat dočasnou licenci](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Chcete-li začít, musíte do svého projektu C# importovat potřebné balíčky. Zde je návod, jak zahrnout knihovnu Aspose.PDF:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Ujistěte se, že máte tyto balíčky přidány do projektu pomocí NuGetu nebo preferovanou metodou.

## Krok 1: Načtěte formulář PDF

Nejprve je třeba načíst PDF formulář, který obsahuje přepínače. `Aspose.Pdf.Facades.Form` Pro tento účel se používá třída . Zde je návod, jak to udělat:

```csharp
// Definujte cestu k adresáři s dokumenty
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Načíst zdrojový PDF formulář
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

V tomto úryvku kódu:
- `dataDir` určuje cestu, kde se nachází váš PDF soubor.
- `Form` Třída se používá k interakci s poli formuláře v PDF.
- `Document` třída poskytuje přístup ke stránkám PDF dokumentu.

## Krok 2: Iterujte přes pole přepínačů

Dále budete muset iterovat mezi poli ve formuláři, abyste identifikovali a upravili pole přepínačů:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

V této smyčce:
- `FieldNames` poskytuje seznam všech názvů polí v PDF.
- `GetButtonOptionValues(item)` načte dostupné možnosti pro každé přepínač.

## Krok 3: Úprava možností přepínače

Jakmile identifikujete pole přepínačů, můžete upravit jejich možnosti. K tomu je třeba přetypovat pole na `RadioButtonField` a aktualizujte jeho možnosti:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Zde:
- Zkontrolujeme, zda název pole obsahuje „radio1“, abychom identifikovali konkrétní pole přepínače, které chceme upravit.
- `RadioButtonField` se přetypuje z polí formuláře pro provedení specifických úprav.

## Krok 4: Nastavení popisku pro přepínač

Chcete-li nastavit nebo aktualizovat popisek přepínače, budete muset vytvořit `TextFragment` používat `TextBuilder` umístit na požadované místo:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Vytvořit objekt TextParagraph
        TextParagraph par = new TextParagraph();
        // Nastavení pozice odstavce
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Zadejte režim zalamování slov
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Přidat nový TextFragment do odstavce
        par.AppendLine(updatedFragment);
        // Přidání textového odstavce pomocí TextBuilderu
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

V této části:
- `TextFragment` slouží k definování textu a jeho vzhledu.
- `TextParagraph` pomáhá s umístěním a formátováním textu.
- `TextBuilder` přidá text na zadanou stránku PDF.

## Krok 5: Uložte aktualizovaný PDF

Nakonec uložte aktualizovaný PDF soubor do nového souboru:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Tím se zajistí, že:
- Změny se použijí v PDF.
- Původní přepínač je odebrán dle zadání.

## Závěr

Úprava popisků přepínačů ve formuláři PDF pomocí Aspose.PDF pro .NET může výrazně zlepšit interaktivitu a použitelnost vašich dokumentů. Pomocí kroků popsaných v tomto tutoriálu můžete snadno načíst PDF, aktualizovat možnosti přepínačů a uložit změny. Tento přístup je užitečný pro správu formulářů a zajišťuje, že vaše PDF soubory přesně splňují potřeby vašich uživatelů. Ponořte se do Aspose.PDF a prozkoumejte jeho možnosti pro další manipulace s PDF!

## Často kladené otázky

### Mohu aktualizovat více polí přepínačů najednou?
Ano, můžete iterovat všemi poli přepínačů a podle potřeby provádět změny.

### Potřebuji licenci k používání Aspose.PDF?
Můžete začít s bezplatnou zkušební verzí, ale pro delší používání je vyžadována licence. [Získejte licenci zde](https://purchase.aspose.com/buy).

### Jak mohu otestovat změny před uložením PDF?
PDF si můžete prohlédnout ve svém vývojovém prostředí nebo použít prohlížeč PDF ke kontrole úprav.

### Je Aspose.PDF kompatibilní se všemi verzemi .NET?
Aspose.PDF podporuje různé verze .NET. Ujistěte se, že jste si ověřili kompatibilitu s vaší konkrétní verzí .NET.

### Mohu podobným způsobem manipulovat s dalšími poli formuláře?
Ano, podobné techniky lze použít i na jiné typy formulářových polí v dokumentech PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}