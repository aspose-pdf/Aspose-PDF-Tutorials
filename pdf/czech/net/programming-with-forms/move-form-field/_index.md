---
"description": "Naučte se v tomto návodu, jak přesouvat pole formuláře v dokumentech PDF pomocí Aspose.PDF pro .NET. Postupujte podle tohoto podrobného návodu a snadno upravte umístění textových polí."
"linktitle": "Přesunout pole formuláře"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přesunout pole formuláře"
"url": "/cs/net/programming-with-forms/move-form-field/"
"weight": 200
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přesunout pole formuláře

## Zavedení

Úprava polí formuláře v dokumentech PDF se může zpočátku zdát složitá, ale s Aspose.PDF pro .NET je to hračka! Ať už pracujete na přesouvání textových polí, doladění rozvržení nebo úpravě interaktivních prvků, Aspose.PDF nabízí výkonné řešení pro vaše projekty .NET. V tomto tutoriálu vás provedeme kroky k přesunutí pole formuláře v dokumentu PDF pomocí Aspose.PDF pro .NET.

## Předpoklady

Než začneme, zde je několik věcí, které budete potřebovat:

1. Aspose.PDF pro .NET nainstalovaný ve vašem vývojovém prostředí.
2. Soubor PDF, který obsahuje pole formuláře (v tomto případě textové pole), které má být upraveno.
3. Základní znalost programování v C#.
4. Visual Studio nebo jakékoli jiné vývojové prostředí pro C#.

### Instalace Aspose.PDF pro .NET

Nejnovější verzi souboru Aspose.PDF pro .NET si můžete stáhnout z [Stránka ke stažení Aspose](https://releases.aspose.com/pdf/net/)Po stažení jej můžete nainstalovat pomocí NuGetu ve Visual Studiu spuštěním následujícího příkazu:

```bash
Install-Package Aspose.PDF
```

Budete také muset získat [dočasná licence](https://purchase.aspose.com/temporary-license/) nebo si zakoupit licenci od [Obchod Aspose](https://purchase.aspose.com/buy).

## Importovat balíčky

Než budete moci použít Aspose.PDF, budete muset importovat požadované jmenné prostory do kódu C#:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
```

Tyto balíčky vám poskytnou přístup k základním funkcím pro manipulaci s PDF dokumenty a specifickým funkcím formulářů, které potřebujete.

Nyní, když máte vše připraveno, pojďme si projít proces přesunutí pole formuláře v dokumentu PDF pomocí Aspose.PDF pro .NET.

## Krok 1: Nastavení projektu a načtení dokumentu PDF

První věc, kterou musíte udělat, je nastavit projekt a načíst soubor PDF, který obsahuje pole formuláře, které chcete upravit. Zde je návod, jak to udělat:

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Otevřít dokument
Document pdfDocument = new Document(dataDir + "MoveFormField.pdf");
```

Tento kód inicializuje dokument jeho načtením ze zadaného adresáře. Nezapomeňte nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k souboru, kde je váš PDF uložen. Tento PDF by měl obsahovat alespoň jedno pole formuláře, se kterým můžete pracovat.

## Krok 2: Přístup k poli formuláře, které chcete přesunout

Jakmile je PDF načten, dalším krokem je přístup k poli formuláře, které chcete přesunout. V tomto případě přesouváme textové pole formuláře, ale tuto metodu lze použít i pro jiné typy polí formuláře.

```csharp
// Získání pole formuláře podle jeho názvu (v tomto případě „textbox1“)
TextBoxField textBoxField = pdfDocument.Form["textbox1"] as TextBoxField;
```

Zde přistupujeme k poli formuláře s názvem `"textbox1"`Ujistěte se, že znáte název pole formuláře, které chcete upravovat, nebo v případě potřeby můžete k zobrazení seznamu nebo vyhledávání polí formuláře použít jiné techniky.

## Krok 3: Upravte umístění pole

A teď přichází ta vzrušující část: přesun pole formuláře! Toho dosáhneme úpravou jeho obdélníkových hranic, které definují polohu a velikost pole formuláře na stránce.

```csharp
// Změnit umístění pole formuláře (nové souřadnice)
textBoxField.Rect = new Aspose.Pdf.Rectangle(300, 400, 600, 500);
```

Ve výše uvedeném řádku kódu nastavujeme polohu textového pole definováním souřadnic jeho obdélníku. Čísla představují levý dolní a pravý horní roh obdélníku (`300, 400, 600, 500`). Tyto hodnoty můžete přizpůsobit podle toho, kde se má pole na stránce zobrazovat.

## Krok 4: Uložení upraveného dokumentu

Po přesunutí pole formuláře je posledním krokem uložení upraveného PDF souboru. Můžete jej uložit pod novým názvem, abyste zabránili přepsání původního dokumentu.

```csharp
// Uložit aktualizovaný dokument PDF
dataDir = dataDir + "MoveFormField_out.pdf";
pdfDocument.Save(dataDir);
Console.WriteLine("\nForm field moved successfully to a new location.\nFile saved at " + dataDir);
```

Dokument bude uložen do stejného adresáře s aktualizovaným názvem (`MoveFormField_out.pdf`). Po uložení můžete soubor otevřít a ověřit, zda bylo pole formuláře přesunuto na požadované místo.

## Závěr

Přesouvání polí formuláře v PDF pomocí Aspose.PDF pro .NET je jednoduché, jakmile pochopíte základy práce s... `Rectangle` objekt a pole formuláře. Pomocí výše uvedeného kódu můžete snadno upravit polohu libovolného pole formuláře, což vám pomůže přizpůsobit rozvržení PDF a interakce s uživateli.

## Často kladené otázky

### Mohu touto metodou přesouvat i jiné typy polí formuláře?
Ano, libovolné pole formuláře, včetně zaškrtávacích políček, přepínačů a podpisů, můžete přesunout stejnou metodou přístupem k danému typu pole.

### Jak mohu načíst názvy všech polí formuláře v PDF?
Pole formuláře můžete iterovat pomocí `pdfDocument.Form.Fields` vypsat všechna pole formuláře a jejich názvy.

### Co když chci změnit velikost pole formuláře, místo abych ho přesunul?
Umístění i velikost můžete upravit úpravou `Rectangle` šířku a výšku objektu při nastavování nových souřadnic.

### Potřebuji licenci k používání Aspose.PDF pro .NET?
Ano, Aspose.PDF vyžaduje licenci pro produkční použití, ale můžete si ji pořídit [dočasná licence](https://purchase.aspose.com/temporary-license/) pro účely hodnocení.

### Mohu přesunout více polí formuláře najednou?
Ano, přístupem ke každému poli formuláře a jeho úpravou `Rect` vlastnost, můžete přesouvat více polí současně.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}