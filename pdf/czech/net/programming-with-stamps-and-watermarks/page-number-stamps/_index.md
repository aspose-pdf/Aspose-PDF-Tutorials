---
"description": "Naučte se, jak přidat razítka s čísly stránek do PDF souborů pomocí Aspose.PDF pro .NET, a to v našem snadno srozumitelném návodu s ukázkovým kódem."
"linktitle": "Razítka s čísly stránek v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Razítka s čísly stránek v souboru PDF"
"url": "/cs/net/programming-with-stamps-and-watermarks/page-number-stamps/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Razítka s čísly stránek v souboru PDF

## Zavedení

Už jste někdy zápasili s PDF dokumentem a přáli jste si, aby měl čísla stránek pro snazší navigaci? Ať už jste student, který sdílí poznámky, profesionál prezentující zprávy, nebo někdo, kdo spravuje vícestránkové dokumenty, přidání čísel stránek může skutečně zlepšit přehlednost vašich PDF souborů. Naštěstí s výkonnou knihovnou Aspose.PDF pro .NET můžete do svých PDF dokumentů snadno přidávat razítka s čísly stránek. V této příručce vás krok za krokem provedeme celým procesem a zajistíme, abyste měli všechny potřebné znalosti. Pojďme se do toho pustit!

## Předpoklady

Než začneme s přidáváním razítek s číslováním stránek do dokumentů PDF, ujistěte se, že máte splněny následující předpoklady:

1. Visual Studio: Ujistěte se, že máte v systému nainstalované Visual Studio. Zde budete psát a spouštět svůj kód.
2. .NET Framework: Znalost programování v C# a frameworku .NET je nezbytná, protože Aspose.PDF je určen pro .NET aplikace.
3. Knihovna Aspose.PDF: Knihovnu Aspose.PDF si můžete stáhnout z [PDF verze Aspose](https://releases.aspose.com/pdf/net/). 
4. Základní znalost PDF souborů: I když nemusíte být odborníkem, základní znalost fungování PDF souborů vám pomůže lépe porozumět tutoriálu.

Jakmile budete mít tyto předpoklady nastavené, budete připraveni začít s razítkováním čísel stránek!

## Importovat balíčky

Než se pustíte do kódování, musíte se ujistit, že máte do projektu importovány potřebné balíčky Aspose.PDF. To je klíčové pro bezproblémové využití funkcí knihovny. Zde je návod, jak to udělat:

### Vytvořit nový projekt

1. Otevřete Visual Studio.
2. Klikněte na `File` > `New` > `Project`.
3. Vyberte šablonu vhodnou pro C# (např. Konzolová aplikace), pojmenujte ji a klikněte `Create`.

### Přidat odkaz na Aspose.PDF

1. Klikněte pravým tlačítkem myši na název projektu v Průzkumníku řešení.
2. Klikněte na `Manage NuGet Packages`.
3. Hledat `Aspose.PDF` a nainstalujte nejnovější verzi.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

knihovnou připravenou k nastartování se pojďme pustit do kódování!

Nyní, když je naše prostředí nastavené, je čas přidat do PDF souboru razítka s čísly stránek. Pro lepší pochopení si tento proces rozdělíme do jasných kroků.

## Krok 1: Zadejte adresář dokumentů

Nejprve je třeba zadat adresář, kde se nachází váš PDF soubor. Toto je výchozí bod vašeho projektu.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Aktualizovat tuto cestu
```

Vysvětlení: Nahradit `"YOUR DOCUMENT DIRECTORY"` s cestou vedoucí k adresáři obsahujícímu váš PDF soubor. To je důležité, protože to vašemu kódu říká, kde má najít soubor, se kterým chcete manipulovat.

## Krok 2: Otevřete dokument

Dále otevřeme existující dokument PDF, do kterého chceme přidat razítka s čísly stránek.

```csharp
Document pdfDocument = new Document(dataDir + "PageNumberStamp.pdf");
```

Vysvětlení: Zde používáme `Document` třída poskytovaná Aspose.PDF pro otevření našeho konkrétního PDF souboru. Ujistěte se, že název souboru odpovídá skutečnému souboru, který máte ve svém adresáři.

## Krok 3: Vytvořte razítko s číslem stránky

teď přichází ta zábavná část! Pojďme si vytvořit razítko s číslem stránky, které přidáme do našeho PDF.

```csharp
PageNumberStamp pageNumberStamp = new PageNumberStamp();
```

Vysvětlení: `PageNumberStamp` Třída nám umožní vytvořit razítko, které zobrazí aktuální číslo stránky vzhledem k celkovému počtu stránek v dokumentu.

## Krok 4: Konfigurace razítka

Nyní budete muset nakonfigurovat nastavení razítka. Zde navrhujete, jak bude razítko vypadat a chovat se.

```csharp
pageNumberStamp.Background = false;
pageNumberStamp.Format = "Page # of " + pdfDocument.Pages.Count;
pageNumberStamp.BottomMargin = 10;
pageNumberStamp.HorizontalAlignment = HorizontalAlignment.Center;
pageNumberStamp.StartingNumber = 1;
```

Vysvětlení:
- `Background = false`: To znamená, že se razítko zobrazí v popředí.
- `Format`Zde nastavujete formát pro zobrazení „Stránka X z Y“, kde dynamicky načítáte celkový počet stránek v dokumentu.
- `BottomMargin`: Upraví vzdálenost od spodního okraje stránky.
- `HorizontalAlignment`: Vycentruje razítko vodorovně.
- `StartingNumber`: Nastavuje počáteční číslo stránky, obvykle od 1.

## Krok 5: Nastavení vlastností textu

Dále si můžete přizpůsobit vzhled textu v razítku.

```csharp
pageNumberStamp.TextState.Font = FontRepository.FindFont("Arial");
pageNumberStamp.TextState.FontSize = 14.0F;
pageNumberStamp.TextState.FontStyle = FontStyles.Bold;
pageNumberStamp.TextState.FontStyle = FontStyles.Italic;
pageNumberStamp.TextState.ForegroundColor = Color.Aqua;
```

Vysvětlení: Tyto atributy konfigurují typ písma, velikost písma, styl (tučné i kurzíva) a barvu textu v razítku, aby byl vizuálně přitažlivý.

## Krok 6: Přidání razítka na konkrétní stránku

Jakmile máte razítko nakonfigurované, je čas ho přidat na konkrétní stránku v dokumentu.

```csharp
pdfDocument.Pages[1].AddStamp(pageNumberStamp);
```

Vysvětlení: Tento řádek přidá razítko na první stránku PDF. Můžete upravit `Pages[1]` indexovat další stránky dle potřeby.

## Krok 7: Uložení výstupního dokumentu

Nakonec upravený dokument PDF uložte, aby změny byly trvalé.

```csharp
dataDir = dataDir + "PageNumberStamp_out.pdf";
pdfDocument.Save(dataDir);
Console.WriteLine("\nPage number stamp added successfully.\nFile saved at " + dataDir);
```

Vysvětlení: Definujete cestu k výstupnímu souboru a ukládáte dokument. Konzola vás upozorní, že razítko bylo úspěšně přidáno a kam je soubor uložen.

## Závěr

Přidávání razítek s čísly stránek do PDF souborů pomocí Aspose.PDF pro .NET je nejen jednoduché, ale také vysoce přizpůsobitelné. Postupně jsme vás krok za krokem provedl procesem vytváření razítka s čísly stránek, abyste měli jasné pokyny. Nyní máte znalosti, které vám pomohou vylepšit vaše PDF dokumenty, učinit je uživatelsky přívětivějšími a profesionálnějšími. 

## Často kladené otázky

### Mohu si přizpůsobit vzhled čísel stránek?  
Ano! Písmo, velikost, barvu a formátování čísel stránek můžete změnit, jak je znázorněno v průvodci.

### Je Aspose.PDF zdarma k použití?  
Aspose.PDF nabízí bezplatnou zkušební verzi, ale pro rozsáhlé použití budete potřebovat licenci. Podívejte se na [koupit stránku](https://purchase.aspose.com/buy) pro více informací.

### Co když narazím na problémy při implementaci?  
Můžete navštívit [Fórum podpory Aspose](https://forum.aspose.com/c/pdf/10) pomoc.

### Jak mohu automaticky generovat čísla stránek pro více stránek?  
Kód průvodce automaticky vypočítá celkový počet stránek, což usnadňuje přizpůsobení pro více stránek.

### Mohu použít Aspose.PDF v jiných programovacích jazycích?  
Ačkoli se tato příručka zaměřuje na .NET, Aspose nabízí knihovny pro Javu, Python a další.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}