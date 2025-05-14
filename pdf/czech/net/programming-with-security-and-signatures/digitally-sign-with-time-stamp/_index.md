---
"description": "Naučte se, jak digitálně podepsat PDF s časovým razítkem pomocí Aspose.PDF pro .NET. Tato podrobná příručka zahrnuje předpoklady, nastavení certifikátu, časové razítko a další."
"linktitle": "Digitální podpis s časovým razítkem v souboru PDF"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Digitální podpis s časovým razítkem v souboru PDF"
"url": "/cs/net/programming-with-security-and-signatures/digitally-sign-with-time-stamp/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Digitální podpis s časovým razítkem v souboru PDF

## Zavedení

Potřebovali jste někdy digitálně podepsat PDF a přidat k němu časové razítko pro větší zabezpečení? Ať už pracujete na právních dokumentech, smlouvách nebo čemkoli, co vyžaduje bezpečné ověřování, digitální podpis s časovým razítkem dodává další vrstvu důvěryhodnosti. V tomto tutoriálu si ukážeme, jak můžete pomocí Aspose.PDF pro .NET přidat digitální podpis spolu s časovým razítkem do vašich PDF dokumentů. Nebojte se, provedeme to krok za krokem!

## Předpoklady

Než se pustíme do kódu, je třeba nastavit několik věcí, abyste mohli pokračovat. Zde je stručný kontrolní seznam předpokladů pro začátek:

- Knihovna Aspose.PDF pro .NET: V projektu budete potřebovat nainstalovanou knihovnu Aspose.PDF pro .NET. Můžete [stáhněte si nejnovější verzi zde](https://releases.aspose.com/pdf/net/) nebo jej přidejte do svého projektu přes NuGet.
- Dokument PDF: Budete potřebovat vzorový soubor PDF, se kterým budete moci pracovat. Ujistěte se, že máte v adresáři projektu soubor, který chcete podepsat.
- Digitální certifikát (soubor PFX): Ujistěte se, že máte digitální certifikát (soubor `.pfx` soubor) pro digitální podpis dokumentu.
- URL pro časové razítko: Toto je online služba pro časové razítko, která bude použita k připojení časového razítka k digitálnímu podpisu. 
- Základní znalost C#: Nemusíte být expert, ale znalost základů C# vám pomůže porozumět kódu a přizpůsobit si ho.

Jakmile zaškrtnete všechna tato políčka, můžete začít programovat!

## Importovat balíčky

Pro začátek budete muset do svého projektu C# importovat následující jmenné prostory. Tím zajistíte přístup k příslušným třídám a funkcím Aspose.PDF.

```csharp
using System.IO;
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using Aspose.Pdf.Forms;
using System.Collections;
```

## Krok 1: Načtěte dokument PDF

První věc, kterou musíme udělat, je načíst PDF dokument, který chceme podepsat. Zde je návod, jak to udělat:

```csharp
// Definujte cestu k adresáři s dokumenty
string dataDir = "YOUR DOCUMENTS DIRECTORY";

// Načíst PDF dokument
Document document = new Document(dataDir + @"DigitallySign.pdf");
```

Tento krok je docela jednoduchý. Jednoduše definujeme cestu k dokumentu, který chceme podepsat. `Document` Třída z Aspose.PDF zpracovává načítání souboru.

## Krok 2: Nastavení digitálního podpisu

Dále vytvoříme digitální podpis pomocí třídy PKCS7 a načteme soubor PFX. Tento soubor PFX obsahuje váš certifikát a soukromý klíč, které jsou nezbytné pro podepsání dokumentu.

```csharp
// Cesta k vašemu souboru .pfx
string pfxFile = "YOUR DOCUMENTS DIRECTORY\\certificate.pfx";

// Inicializujte objekt podpisu
PdfFileSignature signature = new PdfFileSignature(document);

// Načíst soubor PFX s heslem
PKCS7 pkcs = new PKCS7(pfxFile, "pfx_password");
```

V tomto okamžiku říkáte Aspose, aby k podepsání dokumentu použil váš digitální certifikát. `PKCS7` objekt se postará o veškerou kryptografickou práci za vás, takže se nemusíte starat o detaily.

## Krok 3: Přidání nastavení časového razítka

Jednou z klíčových součástí robustního digitálního podpisu je časové razítko. To zajišťuje, že podpis dokumentu lze ověřit i po vypršení platnosti certifikátu. Nastavme časové razítko pomocí online autority pro časové razítko.

```csharp
// Definování nastavení časového razítka
TimestampSettings timestampSettings = new TimestampSettings("https://vaše_časové_razítko_url", "uživatel:heslo");

// Přidání nastavení časového razítka k objektu PKCS7
pkcs.TimestampSettings = timestampSettings;
```

Zde zadáváte URL adresu služby časového razítka, která automaticky přiřadí čas a datum vašemu podpisu. To lze provést s ověřováním nebo bez něj.

## Krok 4: Definujte umístění a vzhled podpisu

Nyní definujeme, kde se podpis v PDF zobrazí a jaké budou jeho rozměry. Můžete si přizpůsobit polohu pole pro podpis na stránce a také jeho velikost.

```csharp
// Definujte vzhled a umístění podpisu (stránka 1, se zadaným obdélníkem)
System.Drawing.Rectangle rect = new System.Drawing.Rectangle(100, 100, 200, 100);
```

Zde definujeme obdélník, který umístí podpis na souřadnice (100, 100) na první stránce PDF, o šířce 200 a výšce 100. Tyto hodnoty můžete změnit podle svého návrhu.

## Krok 5: Podepište dokument PDF

Jakmile je vše nastaveno, je čas skutečně použít digitální podpis na PDF. Tento krok spojuje certifikát, časové razítko a umístění do jednoho jednoduchého příkazu.

```csharp
// Podepište dokument na první stránce
signature.Sign(1, "Signature Reason", "Contact", "Location", true, rect, pkcs);
```

Zde se dozvíte, co se děje:
- 1: Toto znamená, že podpis by měl být použit na první stránku.
- „Důvod podpisu“: Zde můžete uvést, proč dokument podepisujete.
- „Kontakt“: Zadejte kontaktní údaje podepisující osoby.
- „Místo“: Zadejte umístění podepisující osoby.
- true: Tato booleovská hodnota označuje, zda je podpis v dokumentu viditelný.
- obdélník: Obdélník, který jsme definovali dříve, určuje velikost a polohu podpisu.
- pkcs: Objekt PKCS7 obsahuje nastavení digitálního certifikátu a časového razítka.

## Krok 6: Uložení podepsaného PDF

Jakmile je dokument podepsán, zbývá jej už jen uložit. Můžete zvolit nový název souboru, abyste zachovali původní i podepsanou verzi.

```csharp
// Uložit podepsaný dokument PDF
signature.Save(dataDir + "DigitallySignWithTimeStamp_out.pdf");
```

Váš nově podepsaný a časově orazítkovaný PDF soubor je nyní uložen do zadaného adresáře!

## Závěr

tady to máte! Úspěšně jste digitálně podepsali PDF s časovým razítkem pomocí Aspose.PDF pro .NET. Tento proces zajišťuje autenticitu a integritu vašich dokumentů a poskytuje vám i příjemci klid. Digitální podpisy se v dnešním digitálním světě stávají stále důležitějšími, takže zvládnutí tohoto procesu je rozhodně dovednost, která stojí za to.

## Často kladené otázky

### Mohu pro certifikát použít jiný formát souboru?  
Ano, ale tutoriál se zaměřuje na použití souboru PFX, což je nejběžnější formát pro digitální certifikáty.

### Potřebuji k použití časového razítka připojení k internetu?  
Ano, protože časové razítko je získáváno z online autority pro udělování časových razítek, budete potřebovat přístup k internetu.

### Mohu podepsat více stránek v PDF souboru?  
Rozhodně! Můžete to upravit `signature.Sign()` metoda pro cílení na více stránek nebo procházení všech stránek.

### Co se stane, když je heslo k souboru PFX nesprávné?  
Pokud je heslo nesprávné, zobrazí se vám výjimka, proto se ujistěte, že je zadáno správně.

### Můžu podpis zneviditelnit?  
Ano, můžete projít `false` k `Sign` parametr viditelnosti metody, aby byl podpis neviditelný.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}