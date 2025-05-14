---
"description": "Naučte se, jak pomocí Aspose.PDF pro .NET určit stránku, kterou chcete v PDF zobrazit. Vylepšete navigaci uživatelů pomocí tohoto jednoduchého průvodce."
"linktitle": "Při prohlížení uveďte stránku"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Při prohlížení uveďte stránku"
"url": "/cs/net/programming-with-links-and-actions/specify-page-when-viewing/"
"weight": 110
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Při prohlížení uveďte stránku

## Zavedení

Chcete vylepšit své PDF aplikace tím, že uživatele po otevření dokumentu přesměrujete na konkrétní stránky? Jste na správném místě! V této příručce se ponoříme do detailů používání Aspose.PDF pro .NET k určení stránky, která se má zobrazit při otevření PDF. Tato funkce může výrazně zlepšit uživatelský komfort, zejména pokud potřebujete upozornit na kritické části dokumentu.

## Předpoklady

Než se pustíme do kódování, ujistěte se, že máte vše, co potřebujete k zahájení. Zde je to, co budete potřebovat:

1. Základní znalost .NET: Znalost frameworku .NET je nezbytná. Pokud ovládáte C# a máte základní znalosti objektově orientovaného programování, máte hotovo!

2. Aspose.PDF pro .NET: Budete muset mít ve svém projektu nainstalovanou knihovnu Aspose.PDF. Pokud ji ještě nemáte nainstalovanou, můžete si ji stáhnout. [zde](https://releases.aspose.com/pdf/net/).

3. Visual Studio: V tomto tutoriálu se předpokládá, že jako IDE používáte Visual Studio. Ujistěte se, že ho máte na svém počítači nainstalované.

4. Soubor PDF: Budete potřebovat existující soubor PDF, se kterým budete pracovat. Pokud žádný nemáte, můžete si vytvořit vzorový dokument nebo použít libovolný soubor PDF dle vlastního výběru.

Jakmile budete mít tyto předpoklady splněny, můžeme si vyhrnout rukávy a začít programovat!

## Importovat balíčky

Nyní, když máme vše nastavené, importujme potřebné balíčky do našeho projektu. Postupujte takto:

### Spuštění Visual Studia

Otevřete Visual Studio a buď vytvořte nový projekt, nebo načtěte existující, kam chcete implementovat funkci prohlížení stránek PDF.

### Odkaz Aspose.PDF

Chcete-li použít knihovnu Aspose.PDF, musíte na ni přidat odkaz:

1. Klikněte pravým tlačítkem myši na svůj projekt v Průzkumníku řešení.
2. Vyberte možnost „Spravovat balíčky NuGet“.
3. Hledat `Aspose.PDF` a nainstalujte balíček.

### Importovat jmenné prostory

Přidejte následující direktivu using na začátek souboru s kódem:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

Nyní jste připraveni začít vytvářet logiku navigace po stránkách PDF!

Rozdělme si náš úkol na zvládnutelné kroky. Napíšeme kód, který otevře PDF dokument, určí konkrétní stránku, která se má při prohlížení zobrazit, a uloží aktualizovaný dokument. 

## Krok 1: Nastavení adresáře dokumentů

Nejprve je třeba nastavit cestu k dokumentům:

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Nahraďte svým adresářem
```

Tento řádek je v podstatě váš plán. Říkáte svému kódu, kde má najít soubor PDF. Nezapomeňte nahradit `YOUR DOCUMENT DIRECTORY` se skutečnou cestou na vašem počítači.

## Krok 2: Načtěte soubor PDF

Dále nahrajete soubor PDF do vaší aplikace:

```csharp
// Načíst PDF soubor
Document doc = new Document(dataDir + "SpecifyPageWhenViewing.pdf");
```

Co se zde děje, je to, že vytváříte novou instanci `Document` objekt při zadávání cesty k souboru PDF. Můžete si to představit jako otevření knihy, kterou jste právě položili na stůl.

## Krok 3: Přejděte na požadovanou stránku

Nyní se podívejme na stránku, kterou chcete zobrazit při otevření dokumentu:

```csharp
// Získání instance druhé stránky dokumentu
Page page2 = doc.Pages[2]; // Nezapomeňte, že indexování začíná od 1
```

Zde přistupujeme k druhé stránce vašeho dokumentu. Stojí za zmínku, že číslování stránek v tomto kontextu začíná od 1, takže pokud uvažujete o stránce 2, musíte použít index 2.

## Krok 4: Nastavení faktoru přiblížení

Můžete upravit úroveň přiblížení zobrazené stránky:

```csharp
// Vytvořte proměnnou pro nastavení faktoru přiblížení cílové stránky
double zoom = 1; // 1 znamená 100% přiblížení
```

Nastavení faktoru přiblížení pomáhá určit, jakou část stránky uživatel uvidí ihned po otevření. Hodnota 1 znamená, že se stránka zobrazí se 100% přiblížením, což je obecně dobré výchozí nastavení.

## Krok 5: Vytvoření instance GoToAction

Pojďme si vyzkoušet navigační funkce:

```csharp
// Vytvořit instanci GoToAction
GoToAction action = new GoToAction(doc.Pages[2]); 
```

V tomto kroku vytváříte instanci `GoToAction` což v podstatě představuje akci navigace na konkrétní místo v PDF – v tomto případě na druhou stránku.

## Krok 6: Definujte cíl

Nyní je třeba definovat, kam by měla akce vést:

```csharp
// Přejít na 2. stránku
action.Destination = new XYZExplicitDestination(page2, 0, page2.Rect.Height, zoom);
```

Tento řádek je jako nastavení GPS cíle pro GoToAction. Říkáte jí, aby přešla na stránku 2 v horní části stránky (výška) a na zadané úrovni přiblížení.

## Krok 7: Nastavení akce Otevřít

Zajistíme, aby se tato akce provedla při otevření dokumentu:

```csharp
// Nastavení akce pro otevření dokumentu
doc.OpenAction = action;
```

Tímto jste deklarovali, že při otevření PDF se aktivuje právě definovaná navigační akce. Je to, jako byste nastavili uvítací panel na úvodní dveře dokumentu.

## Krok 8: Uložte aktualizovaný dokument

Nakonec uložte dokument s provedenými změnami:

```csharp
// Uložit aktualizovaný dokument
doc.Save(dataDir + "goto2page_out.pdf");
```

Tímto krokem dokončíte svou práci! Budete mít nový PDF soubor s názvem `goto2page_out.pdf` která se otevře přímo na vámi zadané stránce.

Tím je kódovací část hotová! Úspěšně jste naprogramovali Aspose.PDF tak, aby při otevření PDF souboru zobrazoval konkrétní stránku. 

## Závěr

V této příručce jsme krok za krokem popsali, jak pomocí Aspose.PDF pro .NET zadat stránku v souboru PDF. Tato funkce nejen zlepšuje navigaci pro uživatele, ale také zefektivňuje jejich interakci s klíčovým obsahem ve vašich dokumentech. Využitím těchto funkcí vytváříte uživatelsky přívětivější prostředí, které může vaše aplikace pro práci s PDF odlišit.

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům vytvářet, upravovat a spravovat dokumenty PDF v aplikacích .NET.

### Mohu zadat více stránek k zobrazení?
Ne, dokument můžete nastavit tak, aby se otevíral pouze na jedné určené stránce. Můžete však vytvořit různé dokumenty pro různé počáteční stránky.

### Co když chci zobrazit stránku v jiném přiblížení?
Úroveň přiblížení můžete změnit úpravou `zoom` proměnnou před uložením dokumentu.

### Kde najdu další příklady použití Aspose.PDF?
Můžete zkontrolovat [dokumentace](https://reference.aspose.com/pdf/net/) pro další příklady a funkce.

### Je k dispozici bezplatná zkušební verze souboru Aspose.PDF pro .NET?
Ano! Můžete si stáhnout bezplatnou zkušební verzi Aspose.PDF [zde](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}