---
"description": "Naučte se, jak přidat a odebrat JavaScript do PDF dokumentu pomocí Aspose.PDF pro .NET. Podrobný návod s tutoriály pro skriptování na úrovni dokumentu."
"linktitle": "Přidat a odebrat Javascript do dokumentu"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Přidat a odstranit Javascript z PDF dokumentu"
"url": "/cs/net/programming-with-document/addremovejavascripttodoc/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidat a odstranit Javascript z PDF dokumentu

## Zavedení

V této příručce si ukážeme, jak pomocí Aspose.PDF pro .NET vložit JavaScript do PDF souboru a jak jej v případě potřeby odebrat. Na konci tohoto tutoriálu budete mít jasnou představu o tom, jak snadno manipulovat s JavaScriptem v PDF souborech.

## Předpoklady

Než se ponoříme do kódu, je třeba mít nastavených několik věcí:

1. Aspose.PDF pro .NET: Budete potřebovat knihovnu Aspose.PDF pro .NET nainstalovanou ve vašem projektu. Pokud ji ještě nemáte, stáhněte si ji z [Stránka ke stažení souboru Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/).
2. IDE nebo textový editor: Můžete použít jakékoli IDE kompatibilní s .NET, například Visual Studio.
3. Základní znalost jazyka C#: Tento tutoriál předpokládá, že máte zkušenosti s jazykem C# a jste obeznámeni s manipulací s PDF.
4. Licence: Ujistěte se, že máte platnou licenci, abyste se vyhnuli omezením. Dočasnou licenci můžete získat od [zde](https://purchase.aspose.com/temporary-license/).

## Importovat balíčky

Abyste mohli začít používat Aspose.PDF pro .NET, budete muset do projektu importovat potřebné jmenné prostory. Postupujte takto:

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Text;
using System.Collections;
```

Tyto dva jmenné prostory jsou nezbytné. `Aspose.Pdf` umožňuje pracovat s PDF dokumenty, a zároveň `System.Collections` bude použit pro práci s klíči JavaScriptu.

Pojďme si celý proces přidávání a odebírání JavaScriptu z PDF rozebrat do snadno sledovatelných kroků.

## Krok 1: Inicializace nového dokumentu PDF

První věc, kterou budete muset udělat, je vytvořit nový PDF dokument. Tento dokument bude sloužit jako prázdné plátno pro přidání JavaScriptu.

```csharp
Document doc = new Document();
doc.Pages.Add();
```

Zde inicializujeme nový `Document` objekt a přidáním prázdné stránky k němu. Představte si to jako základ vašeho PDF.

## Krok 2: Přidání JavaScriptu do PDF

Nyní, když máme dokument, je čas do něj přidat JavaScript. JavaScript v PDF souborech lze použít k přidání vlastních funkcí, jako jsou upozornění nebo ověřování formulářů.

```csharp
doc.JavaScript["func1"] = "function func1() { hello(); }";
doc.JavaScript["func2"] = "function func2() { hello(); }";
```

V tomto úryvku kódu přidáváme dvě JavaScriptové funkce (`func1` a `func2`) do PDF. Tyto funkce mohou provádět různé úkoly v závislosti na vašich potřebách. Zde pouze voláme zástupnou funkci s názvem `hello()`.

## Krok 3: Uložení PDF souboru s JavaScriptem

Jakmile přidáte požadovaný JavaScript, je čas uložit PDF.

```csharp
doc.Save(dataDir + "AddJavascript.pdf");
```

Tím se dokument s JavaScriptem uloží pod názvem `AddJavascript.pdf` v zadaném adresáři (`dataDir`).

## Krok 4: Načtení a zobrazení JavaScriptu v existujícím PDF

Řekněme, že potřebujete zkontrolovat nebo upravit funkce JavaScriptu v existujícím PDF souboru. Prvním krokem je načtení PDF souboru a přístup k JavaScriptovým klíčům.

```csharp
Document doc1 = new Document(dataDir + "AddJavascript.pdf");
IList keys = (System.Collections.IList)doc1.JavaScript.Keys;
```

Načítáme stávající `AddJavascript.pdf` a uložení klíčů JavaScriptu do seznamu. `Keys` Vlastnost vrací názvy všech funkcí JavaScriptu připojených k dokumentu.

## Krok 5: Zobrazení funkcí JavaScriptu

Dále můžeme iterovat funkcemi JavaScriptu, abychom zjistili, co je v dokumentu k dispozici.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
```

Tím se do konzole vypíše název každé funkce JavaScriptu a její odpovídající kód. To je užitečné, pokud chcete ověřit, jaké funkce se aktuálně v dokumentu nacházejí.

## Krok 6: Odebrání JavaScriptu z PDF

Řekněme, že chcete odstranit konkrétní funkci JavaScriptu, například `func1`Zde je návod, jak to můžete udělat:

```csharp
doc1.JavaScript.Remove("func1");
Console.WriteLine("Key 'func1' removed ");
```

Ten/Ta/To `Remove` Metoda bere název JavaScriptové funkce jako argument a odstraní ji z dokumentu.

## Krok 7: Ověření odstranění JavaScriptu

Po odstranění JavaScriptu můžete znovu vytisknout zbývající funkce, abyste to potvrdili. `func1` byl úspěšně smazán.

```csharp
Console.WriteLine("=============================== ");
foreach (string key in keys)
{
    Console.WriteLine(key + " ==> " + doc1.JavaScript[key]);
}
Console.WriteLine("Javascript added/removed successfully.");
```

Tato poslední část kódu zajišťuje, že je vše na svém místě a funkce JavaScriptu jsou správně aktualizovány.

## Závěr

Gratulujeme! Právě jste se naučili, jak přidávat a odebírat JavaScript z PDF dokumentu pomocí Aspose.PDF pro .NET. Tuto výkonnou funkci lze využít pro řadu úkolů, od přidávání dynamických zpráv až po provádění vlastních výpočtů nebo validací. Manipulací s JavaScriptem v PDF můžete výrazně vylepšit uživatelský zážitek.

## Často kladené otázky

### Mohu do jednoho PDF přidat více funkcí JavaScriptu?
Rozhodně! Můžete přidat libovolný počet JavaScriptových funkcí pomocí `doc.JavaScript` sbírka.

### Co se stane, když se pokusím odstranit neexistující funkci JavaScriptu?
Pokud funkce neexistuje, pak `Remove` Metoda nevyvolá chybu, ale také nic neodstraní.

### Je možné spustit JavaScript ihned po otevření PDF souboru?
Ano! JavaScript můžete nakonfigurovat tak, aby se spouštěl při určitých spouštěčích, jako je otevření dokumentu nebo kliknutí na tlačítko.

### Mohu upravit JavaScript po jeho přidání do PDF?
Ano, můžete načíst existující PDF, přistupovat k jeho JavaScriptu, upravit kód a dokument znovu uložit.

### Ovlivní odstranění JavaScriptu zbytek obsahu PDF?
Ne, odstranění JavaScriptu ovlivní pouze skript. Obsah PDF zůstává nezměněn.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}