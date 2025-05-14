---
"description": "Naučte se, jak extrahovat digitální podpisy a informace o certifikátech z PDF dokumentů pomocí Aspose.PDF pro .NET. Kompletní podrobný návod pro vývojáře v C#."
"linktitle": "Extrahovat informace o podpisu"
"second_title": "Aspose.PDF pro referenční příručku k .NET API"
"title": "Extrahovat informace o podpisu"
"url": "/cs/net/programming-with-security-and-signatures/extract-signature-info/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat informace o podpisu

## Zavedení

dnešním digitálním světě je zajištění bezpečnosti a integrity dokumentů klíčové. Jednou z běžných metod používaných k zabezpečení PDF souborů je přidání digitálního podpisu. Načtení a ověření údajů o podpisu však může být někdy náročné, zejména pokud pracujete s různými certifikáty. V této příručce vás provedeme procesem extrakce informací o podpisu z PDF dokumentů pomocí Aspose.PDF pro .NET, což vám tento úkol usnadní. Naučíte se, jak přistupovat k polím podpisu, extrahovat informace o certifikátu a ukládat je do souboru.

## Předpoklady

Než začneme, ujistěte se, že máte vše připravené k zahájení.

- Aspose.PDF pro knihovnu .NET: Pokud ji ještě nemáte, můžete si ji stáhnout z [Stránka ke stažení souboru Aspose.PDF pro .NET](https://releases.aspose.com/pdf/net/). 
- Vývojové prostředí .NET: Budete potřebovat IDE, jako je Visual Studio.
- Základní znalost jazyka C#: Znalost jazyka C# je užitečná pro pochopení úryvků kódu v tomto tutoriálu.
- PDF dokument s digitálním podpisem: Pro účely testování se ujistěte, že máte PDF soubor, který obsahuje alespoň jeden digitální podpis.

## Import požadovaných jmenných prostorů

Než se pustíme do kódu, je důležité importovat potřebné jmenné prostory. Tyto jmenné prostory vám umožní přístup k funkcím Aspose.PDF a práci s dokumenty PDF.

```csharp
using System.IO;
using Aspose.Pdf.Forms;
using Aspose.Pdf;
using System;
```

Nyní, když jste si nastavili základní nastavení, pojďme se přesunout k samotnému procesu extrakce informací o podpisu z PDF.

## Krok 1: Nastavení adresáře dokumentů

Než začnete pracovat s dokumentem PDF, je třeba určit umístění souboru, který budete používat. Můžete nahradit `"YOUR DOCUMENT DIRECTORY"` se skutečnou cestou k adresáři, kde jsou uloženy vaše PDF soubory.

```csharp
// Cesta k adresáři s dokumenty.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string input = dataDir + "ExtractSignatureInfo.pdf";
```

Zde zadáme adresář obsahující PDF soubor a samotný název souboru. Ujistěte se, že soubor v tomto adresáři existuje!

## Krok 2: Načtení dokumentu PDF

Nyní, když jste si nastavili adresář, dalším krokem je načtení PDF dokumentu pomocí `Document` třída z Aspose.PDF.

```csharp
using (Document pdfDocument = new Document(input))
{
    // Zpracujte PDF zde.
}
```

Tento řádek kódu inicializuje `Document` objekt, který představuje soubor PDF. `using` Příkaz zajišťuje, že se zdroje po zpracování dokumentu vyčistí.

## Krok 3: Přístup k polím formuláře

V tomto kroku projdeme všechna pole formuláře v dokumentu PDF. Protože podpisy jsou obvykle uloženy jako pole formuláře, pomůže nám tento krok identifikovat pole podpisu.

```csharp
foreach (Field field in pdfDocument.Form)
{
    // Zde identifikujte pole pro podpis.
}
```

Iterací skrz `Form` majetek `Document` objekt, můžeme prozkoumat každé pole formuláře a zkontrolovat, zda se jedná o pole podpisu.

## Krok 4: Identifikace polí pro podpis

Jakmile máte přístup k polím formuláře, dalším krokem je identifikovat, která z nich jsou pole pro podpis. Toho dosáhneme přetypováním každého pole na `SignatureField` objekt.

```csharp
SignatureField sf = field as SignatureField;
if (sf != null)
{
    // Extrahujte informace o podpisu.
}
```

Zde používáme `as` klíčové slovo pro pokus o přetypování každého pole formuláře na `SignatureField`Pokud je obsazení úspěšné, víme, že pole je podpisové.

## Krok 5: Extrahování certifikátu

Nyní, když jste identifikovali pole podpisu, je dalším úkolem extrahovat certifikát z podpisu. Certifikáty obsahují klíčové informace o podepisujícím a platnosti podpisu.

```csharp
Stream cerStream = sf.ExtractCertificate();
```

Ten/Ta/To `ExtractCertificate` metoda vrací `Stream` objekt obsahující data certifikátu. Tento stream lze použít k uložení certifikátu pro další analýzu nebo úložiště.

## Krok 6: Uložení certifikátu do souboru

Jakmile certifikát extrahujete, posledním krokem je jeho uložení do souboru. V tomto případě certifikát uložíme jako `.cer` soubor.

```csharp
if (cerStream != null)
{
    using (cerStream)
    {
        byte[] bytes = new byte[cerStream.Length];
        using (FileStream fs = new FileStream(dataDir + @"input.cer", FileMode.CreateNew))
        {
            cerStream.Read(bytes, 0, bytes.Length);
            fs.Write(bytes, 0, bytes.Length);
        }
    }
}
```

V tomto bloku kódu:

1. Zkontrolujte, zda proud certifikátů není null.
2. Načtěte data certifikátu do bajtového pole.
3. Zapište bajtové pole do `.cer` soubor v adresáři dokumentů.

## Závěr

Extrakce digitálních podpisů a souvisejících informací o certifikátech z PDF dokumentů pomocí Aspose.PDF pro .NET je poměrně jednoduchá, pokud ji rozdělíme na několik jednoduchých kroků. Ať už provádíte audit dokumentů, ověřujete podpisy nebo jen ukládáte certifikáty pro bezpečné uložení, tento tutoriál vám poskytne znalosti potřebné k efektivnímu provedení této činnosti. Nezapomeňte, že zabezpečení a ověřování dokumentů je v dnešním digitálním světě klíčové a použití nástrojů, jako je Aspose.PDF pro .NET, to značně usnadňuje.

## Často kladené otázky

### Mohu extrahovat více podpisů z PDF pomocí Aspose.PDF pro .NET?
Ano, kód prochází všemi poli formuláře v dokumentu, což vám umožňuje extrahovat více podpisů, pokud existují.

### Co se stane, když se v PDF nenajde žádný podpis?
Pokud nejsou k dispozici žádná pole pro podpis, kód je jednoduše přeskočí bez vyvolání chyby.

### Mohu tento přístup použít k ověření platnosti podpisu?
když certifikát můžete extrahovat, ověření platnosti podpisu vyžaduje další kroky, jako je například kontrola řetězce důvěryhodnosti certifikátu.

### Je možné extrahovat data z dalších polí formuláře pomocí Aspose.PDF pro .NET?
Ano, Aspose.PDF umožňuje přístup a manipulaci s různými typy polí formuláře v PDF, nejen s poli pro podpis.

### Jak si mohu zobrazit podrobnosti extrahovaného certifikátu?
Jakmile je certifikát uložen jako `.cer` soubor, můžete jej otevřít pomocí libovolného prohlížeče certifikátů nebo jej importovat do systémového úložiště certifikátů pro další kontrolu.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}