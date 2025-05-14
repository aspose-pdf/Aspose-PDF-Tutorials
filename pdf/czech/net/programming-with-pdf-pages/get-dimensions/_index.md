---
"description": "V tomto tutoriálu si vysvětlíme, jak získat rozměry stránek PDF a provádět s nimi manipulace pomocí Aspose.PDF pro .NET. Jsou zde uvedeny podrobné kroky, které vás celým procesem provedou."
"linktitle": "Získejte rozměry stránky PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Získejte rozměry stránky PDF"
"url": "/cs/net/programming-with-pdf-pages/get-dimensions/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Získejte rozměry stránky PDF

## Zavedení

Potřebovali jste někdy upravit rozměry stránky PDF dokumentu? Možná jste chtěli změnit velikost stránky nebo ji otočit podle svých potřeb? Pokud ano, jste na správném místě! V tomto tutoriálu vás provedeme načítáním a úpravou rozměrů stránky PDF pomocí Aspose.PDF pro .NET. Ať už jste začátečník nebo zkušený vývojář, tento návod bude jednoduchý a snadno se vám bude řídit.

Aspose.PDF pro .NET je výkonná knihovna, která vám umožňuje bez námahy vytvářet, manipulovat a transformovat soubory PDF. Je to jako mít švýcarský armádní nůž na PDF – můžete upravit každý detail tak, aby přesně vyhovoval vašim požadavkům. Pojďme se tedy rovnou do toho pustit a naučit se, jak pomocí tohoto skvělého nástroje načítat a aktualizovat rozměry stránek PDF!

## Předpoklady

Než začnete, budete potřebovat několik věcí, abyste tento tutoriál hladce zvládli:

1. Aspose.PDF pro .NET: Můžete [stáhněte si nejnovější verzi zde](https://releases.aspose.com/pdf/net/)Pokud nemáte licenci, nebojte se! Můžete o ni požádat [bezplatná zkušební verze](https://releases.aspose.com/)nebo se rozhodnout pro [dočasná licence](https://purchase.aspose.com/temporary-license/).
2. Visual Studio: Vývojové prostředí, které použijete k psaní a spouštění kódu.
3. Základní znalost C#: I když se budeme snažit vše zjednodušit, určitá znalost C# celý proces usnadní.
4. PDF soubor pro práci: Vezměte si libovolný vzorový PDF soubor nebo si vytvořte nový pro testování.

## Importovat balíčky

Pro práci s Aspose.PDF pro .NET je potřeba importovat několik základních jmenných prostorů. To připraví půdu pro interakci s dokumenty PDF. Zde je návod, jak to udělat:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
```

Tyto importy zajišťují, že máte přístup k základním třídám potřebným pro manipulaci s PDF soubory, zejména pro správu stránek a načítání jejich rozměrů.

Nyní, když máme vše připravené, rozdělme si proces na snadno sledovatelné kroky.

## Krok 1: Definování cesty k souboru a načtení dokumentu

Prvním krokem je zadat cestu k vašemu PDF dokumentu a načíst ho pomocí Aspose.PDF. To vám umožní interagovat se stránkami v PDF souboru.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Otevřít dokument
Document pdfDocument = new Document(dataDir + "UpdateDimensions.pdf");
```

V tomto kroku v podstatě otevíráte soubor PDF, se kterým chcete pracovat. Pokud jste někdy otevřeli knihu na konkrétní stránce, je to docela podobné – ale místo toho otevíráte dokument PDF pro přístup k jeho stránkám.

## Krok 2: Přidejte prázdnou stránku, pokud žádné stránky neexistují

Co když váš dokument nemá žádné stránky? Nebojte se! Můžeme do dokumentu přidat prázdnou stránku a pracovat s ní. Zde je návod, jak zkontrolovat, zda stránka existuje, a v případě potřeby přidat novou:

```csharp
// Přidá do PDF dokumentu prázdnou stránku
Page page = pdfDocument.Pages.Count > 0 ? pdfDocument.Pages[1] : pdfDocument.Pages.Add();
```

Tento řádek kódu kontroluje, zda v dokumentu již existuje stránka. Pokud ano, vybere první stránku (`Pages[1]`). Jinak vytvoří prázdnou stránku a přidá ji do PDF.

Představte si to jako otevření prázdného sešitu a psaní na první stránku, pokud tam nic není – snadné, že?

## Krok 3: Získejte informace o výšce a šířce stránky

Nyní, když máme stránku, se kterou můžeme pracovat, pojďme zjistit její rozměry. Použijeme `GetPageRect()` metoda pro získání výšky a šířky.

```csharp
// Získání informací o výšce a šířce stránky
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Zde, `GetPageRect(true)` vrací obdélník, který zahrnuje výšku a šířku stránky. Je to jako změřit kus papíru pravítkem. Výstup se zobrazí v konzoli a uvede aktuální rozměry stránky.

## Krok 4: Otočení stránky o 90 stupňů

Chcete otočit stránku? Žádný problém! Pomocí jednoduché vlastnosti můžete stránku otočit o 90 stupňů.

```csharp
// Otočit stránku o 90 stupňů
page.Rotate = Rotation.on90;
```

Tento krok otočí stránku o 90 stupňů ve směru hodinových ručiček. Představte si, že otáčíte vytištěný list na stole – nyní je v režimu na šířku!

## Krok 5: Znovu zkontrolujte rozměry stránky po otočení

Po otočení stránky je vhodné znovu zkontrolovat rozměry. Proč? Protože otočení může ovlivnit interpretaci výšky a šířky.

```csharp
// Získání informací o výšce a šířce stránky
Console.WriteLine(page.GetPageRect(true).Width.ToString() + ":" + page.GetPageRect(true).Height.ToString());
```

Rozměry stránky se nyní aktualizují na základě nové orientace. Je to jako otáčení fotografie v telefonu – najednou se šířka změní na výšku a naopak.


## Závěr

Gratulujeme! Úspěšně jste se naučili, jak načíst a upravit rozměry stránky PDF pomocí Aspose.PDF pro .NET. Nyní byste měli být schopni načíst PDF, zkontrolovat jeho rozměry a v případě potřeby stránku dokonce otočit.

Manipulace s PDF soubory nemusí být složitá. S Aspose.PDF je to tak jednoduché, jako provést několik kroků a používat intuitivní metody. Takže až budete příště potřebovat zvládnout rozměry stránek PDF, budete přesně vědět, co dělat!

## Často kladené otázky

### Mohu stránku otočit o jiné úhly než o 90 stupňů?
Ano, Aspose.PDF umožňuje otáčet stránky o 0, 90, 180 nebo 270 stupňů pomocí `Rotation` vlastnictví.

### Co se stane, když můj PDF soubor nemá žádné stránky?
Pokud váš PDF soubor neobsahuje žádné stránky, můžete přidat prázdnou stránku pomocí `Pages.Add()` metodu, jak je znázorněno v tomto tutoriálu.

### Mohu manipulovat s více stránkami najednou?
Ano, můžete procházet více stránkami a na všechny z nich aplikovat transformace, jako je změna velikosti nebo otočení.

### Ovlivňují rozměry stránky obsah uvnitř PDF?
Rozměry stránky mění pouze velikost plátna, nikoli obsah. Změna velikosti však může změnit způsob, jakým se obsah na stránce zobrazuje.

### Kde najdu více informací o souboru Aspose.PDF pro .NET?
Můžete navštívit [dokumentace zde](https://reference.aspose.com/pdf/net/) pro podrobnější informace a pokročilé případy použití.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}