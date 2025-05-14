---
"description": "Naučte se, jak přidat JavaScript do PDF souboru pomocí Aspose.PDF pro .NET. Podrobný návod s tutoriály pro skriptování na úrovni dokumentů a stránek."
"linktitle": "Přidat PDF soubor s JavaScriptem v jazyce Java"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidání Java skriptu do PDF souboru"
"url": "/cs/net/programming-with-document/addjavascripttopage/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání Java skriptu do PDF souboru

## Zavedení

Přemýšleli jste někdy, jak vylepšit své PDF soubory interaktivními prvky, jako jsou vyskakovací upozornění nebo funkce automatického tisku? Dobrá zpráva – můžete! Pomocí Aspose.PDF pro .NET můžete bez problémů přidat JavaScript do svých PDF dokumentů. Ať už automatizujete úlohy nebo vytváříte dynamické uživatelské prostředí, vložení JavaScriptu do PDF souborů dodá vašim souborům další úroveň funkčnosti.

## Předpoklady

Než se pustíme do kódování, je třeba mít nastaveno několik věcí:

- Aspose.PDF pro .NET: Stáhněte si knihovnu z [Aspose Releases](https://releases.aspose.com/pdf/net/) nebo si pořiďte [bezplatná zkušební verze](https://releases.aspose.com/).
- Vývojové prostředí: Jakékoli IDE kompatibilní s .NET, například Visual Studio.
- Základní znalost C#: Tato příručka předpokládá, že jste obeznámeni se základní syntaxí C#.
- Dočasný řidičský průkaz (volitelný): Můžete získat [dočasná licence](https://purchase.aspose.com/temporary-license/) pokud se chcete během vývoje vyhnout omezením.

## Importovat balíčky

Než začnete psát kód, budete muset importovat potřebné jmenné prostory z knihovny Aspose.PDF. Tyto jmenné prostory vám umožní snadno manipulovat s PDF soubory a přidávat akce JavaScriptu.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
```

Nyní, když jste importovali správné jmenné prostory, jste připraveni začít s kódováním.

## Krok 1: Načtení existujícího PDF souboru

Nejdříve je potřeba načíst PDF dokument, do kterého chcete přidat JavaScript. Tento krok připraví půdu pro všechny další úpravy. Představte si, že máte PDF, který chcete vylepšit dynamickými funkcemi, například automatickým tiskem dokumentu při jeho otevření.

Zde je návod, jak načíst tento soubor PDF:

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Načíst existující soubor PDF
Document doc = new Document(dataDir + "input.pdf");
```

V tomto úryvku kódu používáme `Document` třída pro načtení existujícího PDF souboru ze zadaného adresáře. Nezapomeňte nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k vašemu PDF souboru.

## Krok 2: Přidání JavaScriptu na úrovni dokumentu

Nyní přidáme JavaScript, který se spustí při otevření dokumentu. V tomto příkladu napíšeme skript, který otevře dialogové okno pro tisk, jakmile uživatel otevře PDF.

JavaScript na úrovni dokumentu je ideální pro akce, které chcete aplikovat na celý PDF. Představte si to jako nastavení globálního pravidla pro váš dokument.

Zde je kód:

```csharp
// Přidání JavaScriptu na úrovni dokumentu
// Vytvořte instanci JavascriptAction s požadovaným JavaScriptovým příkazem
JavascriptAction javaScript = new JavascriptAction("this.print({bUI:true,bSilent:false,bShrinkToFit:true});");

// Přiřaďte objekt JavascriptAction k akci OpenAction v dokumentu.
doc.OpenAction = javaScript;
```

V tomto kroku vytvoříme `JavascriptAction` objekt, který definuje funkci JavaScriptu pro otevření tiskového dialogu při otevření dokumentu. `doc.OpenAction` Vlastnost je pak přiřazena této akci JavaScriptu.

## Krok 3: Přidání JavaScriptu na úrovni stránky

Ne každá akce musí ovlivnit celý dokument. Někdy chcete, aby se při otevření nebo zavření určitých stránek provedly určité akce. Zde nastavíme akce JavaScriptu pro otevření a zavření konkrétní stránky (řekněme stránky 2).

JavaScript na úrovni stránky je užitečný pro cílené interakce. Může se jednat o cokoli od zobrazení zprávy, když uživatel přejde na stránku, až po vlastní akce, jako je automatické vyplňování polí formuláře.

Zde je návod, jak to udělat:

```csharp
// Přidání JavaScriptu na úrovni stránky
doc.Pages[2].Actions.OnOpen = new JavascriptAction("app.alert('Page 2 opened')");
doc.Pages[2].Actions.OnClose = new JavascriptAction("app.alert('Page 2 closed')");
```

V tomto úryvku kódu přidáme dvě akce JavaScriptu:
1. Akce OnOpen: Zobrazí upozornění „Stránka 2 otevřena“, když uživatel otevře stránku 2.
2. Akce OnClose: Zobrazí upozornění „Stránka 2 zavřena“, když uživatel opustí stránku 2.

To přidá vašemu PDF dokumentu vrstvu interaktivity. Představte si, že uživatele provedete řadou kroků na různých stránkách s upozorněními, která se zobrazí, když na stránku vstoupí nebo ji opustí.

## Krok 4: Uložení dokumentu PDF

Právě jste přidali JavaScript do dokumentu i na konkrétní stránky. Posledním krokem je uložení upraveného PDF souboru do požadovaného umístění. Tato část je jednoduchá, ale klíčová – nezapomeňte si práci uložit!

Zde je kód:

```csharp
// Zadejte cestu k výstupnímu souboru
dataDir = dataDir + "JavaScript-Added_out.pdf";

// Uložit aktualizovaný dokument PDF
doc.Save(dataDir);

Console.WriteLine("\nJavaScript added successfully to the PDF.\nFile saved at " + dataDir);
```

V tomto úryvku uložíme aktualizovaný dokument s přidaným JavaScriptem do nového souboru s názvem `"JavaScript-Added_out.pdf"`Díky tomu nepřepíšete původní soubor a získáte zálohu, se kterou můžete pracovat.

## Závěr

Přidání JavaScriptu do PDF souborů pomocí Aspose.PDF pro .NET je výkonný způsob, jak vytvářet interaktivní a dynamické PDF soubory. Ať už automatizujete úkoly, jako je tisk, nebo vytváříte vlastní upozornění, možnost vložit JavaScript do PDF souborů učiní vaše dokumenty poutavějšími a funkčnějšími.

## Často kladené otázky

### Mohu přidat více akcí JavaScriptu na různé stránky v PDF?
Ano, jednotlivým stránkám nebo celému dokumentu můžete přiřadit různé akce JavaScriptu.

### Je možné JavaScript z PDF po jeho přidání odstranit?
Ano, existující akce JavaScriptu můžete odstranit nebo upravit zrušením zaškrtnutí políčka `Actions` vlastnosti dokumentu nebo stránky.

### Jaké funkce JavaScriptu mohu použít v PDF?
Můžete použít jakýkoli JavaScript podporovaný JavaScriptovým enginem aplikace Adobe Acrobat, například pro tisk, upozornění a manipulaci s formuláři.

### Funguje JavaScript ve všech prohlížečích PDF?
Většina akcí JavaScriptu bude fungovat v prohlížečích PDF, které podporují interaktivní PDF, jako je Adobe Acrobat. Některé základní čtečky PDF však JavaScript podporovat nemusí.

### Mohu spouštět akce JavaScriptu na základě vstupu uživatele v PDF?
Ano, můžete navázat JavaScript na pole formuláře a spouštět akce na základě vstupu uživatele.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}