---
"description": "Naučte se, jak převést HTML do PDF pomocí Aspose.PDF pro .NET s tímto podrobným návodem. Ideální pro vývojáře, kteří chtějí zefektivnit generování dokumentů."
"linktitle": "Zadejte přihlašovací údaje během převodu HTML do PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Zadejte přihlašovací údaje během převodu HTML do PDF"
"url": "/cs/net/document-conversion/provide-credentials-during-html-to-pdf/"
"weight": 240
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zadejte přihlašovací údaje během převodu HTML do PDF

## Zavedení

Ve světě vývoje softwaru je převod HTML do PDF běžným požadavkem. Ať už generujete reporty, faktury nebo jakýkoli jiný dokument, spolehlivá knihovna pro tento úkol vám může ušetřit spoustu času a úsilí. Představujeme Aspose.PDF pro .NET, výkonnou knihovnu, která vývojářům umožňuje snadno vytvářet, manipulovat a převádět dokumenty PDF. V tomto tutoriálu vás provedeme procesem použití Aspose.PDF k převodu HTML do PDF a zároveň vám poskytneme přihlašovací údaje pro bezpečný přístup. Takže, vezměte si programátorskou čepici a pojďme se do toho pustit!

## Předpoklady

Než začneme, je potřeba mít připraveno několik věcí:

1. Visual Studio: Ujistěte se, že máte na svém počítači nainstalované Visual Studio. Toto bude naše vývojové prostředí.
2. Aspose.PDF pro .NET: Knihovnu si můžete stáhnout z [webové stránky](https://releases.aspose.com/pdf/net/)Pokud si to chcete nejdříve vyzkoušet, můžete si také pořídit [bezplatná zkušební verze](https://releases.aspose.com/).
3. Základní znalost C#: Znalost programování v C# vám pomůže lépe porozumět příkladům.
4. Přístup k internetu: Protože budeme načítat HTML obsah z URL adresy, ujistěte se, že máte aktivní připojení k internetu.

## Importovat balíčky

Abyste mohli začít s Aspose.PDF, musíte do svého projektu importovat potřebné balíčky. Zde je návod, jak to udělat:

1. Otevřete svůj projekt ve Visual Studiu.
2. V Průzkumníku řešení klikněte pravým tlačítkem myši na svůj projekt a vyberte možnost „Spravovat balíčky NuGet“.
3. Vyhledejte soubor „Aspose.PDF“ a nainstalujte nejnovější verzi.

```csharp
using System.IO;
using Aspose.Pdf;
using System;
using System.Net;
```
Nyní, když máme vše nastavené, pojďme si rozebrat proces převodu HTML do PDF s přihlašovacími údaji na zvládnutelné kroky.

## Krok 1: Nastavení adresáře dokumentů

Než budeme moci převést HTML do PDF, musíme určit, kam bude náš výstupní PDF uložen. To se provede definováním cesty k adresáři dokumentů.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou, kam chcete soubor PDF uložit. Může to být složka na ploše nebo jakékoli jiné umístění v systému.

## Krok 2: Vytvořte webový požadavek

Dále musíme vytvořit požadavek na načtení HTML obsahu z konkrétní URL adresy. Zde použijeme `WebRequest` třída.

```csharp
WebRequest request = WebRequest.Create("http://My.signchart.com/Report/PrintBook.asp?ProjectGuid=6FB9DBB0-");
```

Zde vytváříme požadavek na URL adresu obsahující HTML kód, který chceme převést. Ujistěte se, že URL adresu nahrazujete tou, kterou chcete použít.

## Krok 3: Nastavení přihlašovacích údajů (pokud je to nutné)

Pokud server vyžaduje pro přístup k obsahu přihlašovací údaje, musíme je nastavit. To se provádí pomocí `CredentialCache.DefaultCredentials`.

```csharp
request.Credentials = CredentialCache.DefaultCredentials;
```

Tento řádek zajišťuje, že požadavek použije výchozí přihlašovací údaje aktuálního uživatele. Pokud potřebujete zadat konkrétní přihlašovací údaje, můžete vytvořit nové. `NetworkCredential` objekt.

## Krok 4: Získejte odpověď

Nyní, když máme nastavený náš požadavek, je čas získat odpověď od serveru.

```csharp
HttpWebResponse response = (HttpWebResponse)request.GetResponse();
```

Tento řádek odešle požadavek a čeká na odpověď serveru. Pokud vše půjde dobře, obdržíme potřebný HTML obsah.

## Krok 5: Přečtěte si tok odpovědí

Jakmile obdržíme odpověď, musíme si přečíst obsah vrácený serverem. To se provádí pomocí `StreamReader`.

```csharp
Stream dataStream = response.GetResponseStream();
StreamReader reader = new StreamReader(dataStream);
string responseFromServer = reader.ReadToEnd();
reader.Close();
dataStream.Close();
response.Close();
```

Zde čteme celý obsah odpovědního proudu do řetězcové proměnné s názvem `responseFromServer`Nezapomeňte zavřít čtečku a stream, abyste uvolnili prostředky.

## Krok 6: Převod HTML do PDF

A teď přichází ta vzrušující část! Převedeme HTML obsah do PDF dokumentu pomocí Aspose.PDF.

```csharp
MemoryStream stream = new MemoryStream(System.Text.Encoding.UTF8.GetBytes(responseFromServer));
HtmlLoadOptions options = new HtmlLoadOptions("http://My.signchart.com/");
options.ExternalResourcesCredentials = CredentialCache.DefaultCredentials;

Document pdfDocument = new Document(stream, options);
```

V tomto kroku vytváříme `MemoryStream` z HTML obsahu a nastavení `HtmlLoadOptions`To nám umožňuje zadat základní URL pro jakékoli externí zdroje (jako jsou obrázky nebo styly), na které by HTML mohl odkazovat.

## Krok 7: Uložení dokumentu PDF

Nakonec musíme uložit vygenerovaný PDF dokument do zadaného adresáře.

```csharp
pdfDocument.Save(dataDir + "ProvideCredentialsDuringHTMLToPDF_out.pdf");
```

Tento řádek uloží PDF soubor s názvem `ProvideCredentialsDuringHTMLToPDF_out.pdf` adresáři, který jsme dříve uvedli.

## Závěr

A tady to máte! Úspěšně jste převedli HTML do PDF pomocí Aspose.PDF pro .NET a zároveň jste poskytli přihlašovací údaje pro zabezpečený přístup. Tato výkonná knihovna usnadňuje práci s PDF dokumenty a s pouhými několika řádky kódu můžete z HTML obsahu generovat profesionálně vypadající PDF soubory. 

## Často kladené otázky

### Co je Aspose.PDF pro .NET?
Aspose.PDF pro .NET je knihovna, která umožňuje vývojářům vytvářet, manipulovat a převádět PDF dokumenty v .NET aplikacích.

### Jak nainstaluji Aspose.PDF?
Soubor Aspose.PDF si můžete nainstalovat pomocí Správce balíčků NuGet ve Visual Studiu nebo si jej stáhnout z [webové stránky](https://releases.aspose.com/pdf/net/).

### Mohu používat Aspose.PDF zdarma?
Ano, Aspose nabízí bezplatnou zkušební verzi, kterou můžete použít k otestování knihovny před zakoupením.

### Jaké typy dokumentů mohu vytvářet pomocí Aspose.PDF?
Pomocí Aspose.PDF můžete vytvářet širokou škálu dokumentů, včetně zpráv, faktur a formulářů.

### Kde najdu podporu pro Aspose.PDF?
Podporu a dotazy můžete najít na [Fórum podpory Aspose](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}