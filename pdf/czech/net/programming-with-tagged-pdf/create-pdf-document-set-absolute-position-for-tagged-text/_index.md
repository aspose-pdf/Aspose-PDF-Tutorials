---
category: general
date: 2026-03-24
description: Vytvořte PDF dokument a naučte se, jak nastavit absolutní pozici pro
  označený text. Tento tutoriál ukazuje, jak přidat element span, jak přidat označený
  obsah a jak umístit text na stránku.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: cs
og_description: Vytvořte PDF dokument a okamžitě zjistěte, jak nastavit absolutní
  pozici, přidat prvek span a umístit text na stránku s označeným PDF obsahem.
og_title: Vytvořit PDF dokument – Absolutní umístění označeného textu
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Vytvořit PDF dokument – Nastavit absolutní pozici pro označený text
url: /cs/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF dokumentu – nastavení absolutní pozice pro označený text

Už jste někdy potřebovali **vytvořit pdf dokument**, který obsahuje přístupný, označený text umístěný přesně tam, kde ho chcete? Možná vytváříte PDF podobné formuláři, kde štítek musí být na přesné souřadnici, nebo generujete certifikát a jméno se musí dokonale zarovnat s obrázkem na pozadí.  

V tomto průvodci projdeme kompletním, spustitelným příkladem, který ukazuje **jak přidat označený** obsah, **nastavit absolutní pozici** a **přidat span element**, abyste mohli **umístit text na stránku** bez hádání. Žádné externí odkazy – pouze kód, který můžete zkopírovat‑vložit, a vysvětlení „proč“ za každým řádkem.

## Požadavky

- .NET 6+ (nebo .NET Framework 4.6+) s C# kompilátorem  
- Aspose.Pdf for .NET (nejnovější verze v době psaní, 23.12) nainstalovaná přes NuGet  
- Základní znalost syntaxe C#  

Pokud máte vše připravené, pojďme na to.

---

## Vytvoření PDF dokumentu – nastavení absolutní pozice

Prvním krokem je vytvořit prázdný objekt `Document`. Tento objekt představuje celý PDF soubor a poskytuje přístup ke stromu označeného – content.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Proč je to důležité:**  
`Document` je kořen PDF struktury. Vytvořením nejdříve zajišťujeme, že existuje plátno jak pro vizuální prvky (stránky, grafika), tak pro logickou strukturu (tagy). Příkaz `using` zaručuje správné uvolnění souboru, což zabraňuje únikům souborových handle na Windows.

## Povolení označeného obsahu (Jak přidat tagy)

Než můžeme vložit jakékoli označené elementy, musí být dokument označen jako *tagged*. Aspose.Pdf automaticky vytvoří objekt `TaggedContent`, ale je třeba zapnout příznak.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Co se děje pod kapotou?**  
Nastavení `TaggedContent` na `true` říká PDF čtečkám, že soubor obsahuje logický strom struktury. To je klíčové pro čtečky obrazovky a pro správnou funkci metody `SetPosition` u span elementu.

## Získání kořenového elementu stromu označeného obsahu

Kořenový element je vstupní bod pro všechny strukturální tagy (jako `<Document>`, `<Section>`, `<Span>`). Představte si ho jako neviditelný „body“ PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Proč potřebujeme kořen:**  
Všechny následné tagy se musí někde v stromu připojit; jinak se neobjeví v hierarchii přístupnosti.

## Přidání Span elementu – stavební blok pro inline text

*Span* je PDF ekvivalent HTML `<span>` – ideální pro krátké úseky textu, které chcete umístit přesně.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Poznámka k návrhu:**  
Pokud potřebujete bohatší formátování (tučné, kurzíva, hypertextové odkazy), můžete span zabalit do `<Paragraph>` nebo později použít objekty `TextFragment`. Pro absolutní pozicování je prostý span nejlehčí.

## Nastavení absolutní pozice – X=100, Y=200

Nyní přichází zábavná část: umístění span na přesnou pozici na stránce. Souřadnicový systém začíná v levém dolním rohu (0,0) a používá body (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Proč absolutní pozicování?**  
Když potřebujete layout pixel‑perfect – např. certifikáty, faktury nebo formuláře – relativní tok (jako text zleva doprava) nestačí. `SetPosition` obejde běžný textový tok a připne element tam, kde určíte.

## Přidání textu do Span

Po umístění span vložíme skutečný řetězec.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tip:**  
Pokud potřebujete Unicode znaky nebo skripty zprava doleva, stačí předat řetězec; Aspose.Pdf se postará o kódování automaticky.

## Připojení Span k kořenovému elementu

Nakonec span připojíme k logickému stromu dokumentu, aby se stal součástí finálního PDF.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Co se stane, když tento krok vynecháte?**  
Span bude existovat v paměti, ale nikdy se nezapíše do souboru, takže neuvidíte žádný text a strom přístupnosti bude neúplný.

## Kompletní, spustitelný příklad

Níže je celý program, který můžete vložit do konzolové aplikace. Vytvoří jednostránkový PDF, přidá označený span na (100, 200) a uloží soubor jako `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Očekávaný výstup:**  
Otevřete `TaggedPositioned.pdf` v libovolném prohlížeči (Adobe Acrobat, Foxit atd.). Uvidíte frázi **„Positioned tagged text“** přesně 100 pt od levého okraje a 200 pt od spodního okraje stránky. Pokud si prohlédnete panel *Tags*, bude pod kořenem dokumentu uveden element `<Span>`, což potvrzuje, že obsah je správně označen.

## Často kladené otázky a okrajové případy

### Co když potřebuji umístit text na konkrétní stránku jinou než první?

Přidejte požadovanou stránku (`var page = pdfDocument.Pages[3];`) před voláním `SetPosition`. Span se automaticky připojí k aktivnímu kontextu stránky.

### Můžu nastavit pozici v palcích nebo centimetrech?

`SetPosition` přijímá body. Převod provádějte podle vzorců:  
- **Palce → body:** `points = inches * 72`  
- **Centimetry → body:** `points = cm * 28.3465`

### Jak změním font nebo barvu span?

Po vytvoření span můžete získat jeho `TextState` a upravit jej:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Co když dokument už obsahuje existující tagy?

Stále můžete vytvořit nový span a připojit jej k libovolnému existujícímu elementu (`rootElement`, konkrétní `<Section>` atd.). Jen dbejte na logickou hierarchii – čtečky obrazovky očekávají dobře strukturovaný strom.

### Funguje to s kompatibilitou PDF/A nebo PDF/UA?

Ano. Označené PDF jsou základním požadavkem pro PDF/UA. Pokud potřebujete PDF/A, po vytvoření obsahu zavolejte `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));`.

## Profesionální tipy a úskalí

- **Pro tip:** Vždy přidejte stránku před pozicováním obsahu. Bez stránky `SetPosition` tiše selže, protože není kam renderovat.
- **Dejte pozor na jednotky:** Míchání pixelů z UI designu s PDF body posune text. Ověřte si převod.
- **Tip pro výkon:** Pokud generujete tisíce PDF, znovu použijte jedinou instanci `Document` a mezi běhy volajte `pdfDocument.Pages.Clear()`, abyste předešli nadměrnému alokování paměti.
- **Připomínka přístupnosti:** Tagování není jen hezký doplněk; mnoho předpisů (Section 508, EN 301 549) ho vyžaduje. Použití `CreateSpanElement` zajišťuje, že text je objevitelný asistivními technologiemi.

## Závěr

Právě jsme **vytvořili pdf dokument** od nuly, **nastavili absolutní pozici**, **přidali span element** a ukázali **jak přidat označený** obsah, abyste mohli **umístit text na stránku** s pixel‑perfect přesností. Kompletní příklad je připraven ke spuštění a vysvětlení pokrývá jak *jak*, tak *proč* – právě to, co vývojáři (a AI asistenti) hledají, když potřebují spolehlivé řešení.

Dále můžete zkusit:

- Přidat obrázky za umístěný text pro vodoznakové certifikáty.  
- Použít `CreateParagraphElement` pro víceřádkové bloky, které stále potřebují absolutní umístění.  
- Exportovat do PDF/UA pro splnění přísných auditů přístupnosti.  

Klidně upravujte souřadnice, fonty nebo barvy – experimentování je nejrychlejší cesta k mistrovství v generování označených PDF. Pokud narazíte na problém, zanechte komentář níže; šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}