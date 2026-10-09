---
title: Přidání nadpisu, jazyka a názvu do PDF pomocí Aspose.PDF pro .NET
weight: 110
limit:
description: Vytvořte PDF, nastavte jeho jazyk a název a přidejte nadpis úrovně 1 pomocí Aspose.PDF pro .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Vytvořte PDF, nastavte jeho jazyk a název a přidejte nadpis úrovně 1
    pomocí Aspose.PDF pro .NET.
  headline: Přidání nadpisu, jazyka a názvu do PDF pomocí Aspose.PDF pro .NET
  type: TechArticle
- description: Vytvořte PDF, nastavte jeho jazyk a název a přidejte nadpis úrovně 1
    pomocí Aspose.PDF pro .NET.
  name: Přidání nadpisu, jazyka a názvu do PDF pomocí Aspose.PDF pro .NET
  steps:
  - name: Definujte název výstupního souboru pro vygenerovaný PDF.
    text: Definujte název výstupního souboru pro vygenerovaný PDF.
  - name: Vytvořte novou prázdnou instanci PDF dokumentu (`pdfDoc`) uvnitř bloku `using`.
    text: Vytvořte novou prázdnou instanci PDF dokumentu (`pdfDoc`) uvnitř bloku `using`.
  - name: Získejte rozhraní `ITaggedContent` pro práci se strukturovanými (tagovanými)
      PDF dokumenty.
    text: Získejte rozhraní `ITaggedContent` pro práci se strukturovanými (tagovanými)
      PDF dokumenty.
  - name: Nastavte výchozí jazyk dokumentu na angličtinu (US) a přiřaďte metadata
      názvu.
    text: Nastavte výchozí jazyk dokumentu na angličtinu (US) a přiřaďte metadata
      názvu.
  - name: Získejte kořenový prvek logického stromu struktury.
    text: Získejte kořenový prvek logického stromu struktury.
  - name: Vytvořte prvek nadpisu úrovně 1, nastavte jeho zobrazovaný text a určete
      jeho jazyk.
    text: Vytvořte prvek nadpisu úrovně 1, nastavte jeho zobrazovaný text a určete
      jeho jazyk.
  - name: Přidejte prvek nadpisu ke kořeni, čímž se nadpis zobrazí v PDF.
    text: Přidejte prvek nadpisu ke kořeni, čímž se nadpis zobrazí v PDF.
  - name: Uložte PDF do určeného souboru a uzavřete rozsah dokumentu.
    text: Uložte PDF do určeného souboru a uzavřete rozsah dokumentu.
  - name: Vypište potvrzovací zprávu do konzole.
    text: Vypište potvrzovací zprávu do konzole.
  type: HowTo
- questions:
  - answer: '`SetLanguage` určuje výchozí jazyk pro celou logickou strukturu dokumentu;
      jakýkoli prvek, který nemá vlastní jazyk nastavený, zdědí „en-US“.'
    question: Jaký je účinek volání `tagContent.SetLanguage(\"en-US\")` na PDF?
  - answer: Nastavení `header.Language` je volitelné; nadpis zdědí výchozí jazyk dokumentu,
      pokud mu nepřiřadíte jinou hodnotu, jak je ukázáno v příkladu.
    question: Musím nastavit `header.Language`, pokud jsem již na dokumentu zavolal
      `SetLanguage`?
  - answer: Použijte `tagContent.CreateHeaderElement(2)` k vytvoření nadpisu úrovně 2;
      číselný argument určuje úroveň nadpisu, která bude odražena ve stromu struktury
      PDF.
    question: Jak mohu vytvořit nadpis úrovně 2 místo nadpisu úrovně 1?
  - answer: '`SetTitle` zapíše zadaný řetězec do pole metadata názvu dokumentu PDF,
      které lze zobrazit v PDF prohlížečích a použít pro vyhledávání nebo indexování.'
    question: Co dělá `tagContent.SetTitle(\"PDF Example with Header\")`?
  - answer: Prvek nadpisu nebude přidán do logického stromu struktury, takže se neobjeví
      ve výstupním PDF ani nebude rozpoznán jako nadpis pro nástroje přístupnosti.
    question: Co se stane, pokud vynechám `rootElement.AppendChild(header)`?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Vložení nadpisu a nastavení jazyka v PDF
og_description: Naučte se vytvořit PDF, nastavit jeho jazyk a název a poté přidat nadpis úrovně 1 pomocí několika řádků .NET kódu.
og_image_alt: Průvodce ukazující, jak přidat nadpis, nastavit jazyk a název v PDF pomocí Aspose.PDF pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání nadpisu, jazyka a názvu do PDF pomocí Aspose.PDF pro .NET
Tento tutoriál vás provede vytvořením nového PDF dokumentu pomocí Aspose.PDF pro .NET, přiřazením výchozího jazyka a názvu dokumentu a vložením nadpisu úrovně 1. Ukážeme si, jak pracovat s třídami Document, ITaggedContent, StructureElement a HeaderElement k vytvoření řádně tagovaného PDF vhodného pro nástroje přístupnosti.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Jaký je účinek volání `tagContent.SetLanguage(\"en-US\")` na PDF?**  
A: `SetLanguage` určuje výchozí jazyk pro celou logickou strukturu dokumentu; jakýkoli prvek, který nemá vlastní jazyk nastavený, zdědí „en-US“.

**Q: Musím nastavit `header.Language`, pokud jsem již na dokumentu zavolal `SetLanguage`?**  
A: Nastavení `header.Language` je volitelné; nadpis zdědí výchozí jazyk dokumentu, pokud mu nepřiřadíte jinou hodnotu, jak je ukázáno v příkladu.

**Q: Jak mohu vytvořit nadpis úrovně 2 místo nadpisu úrovně 1?**  
A: Použijte `tagContent.CreateHeaderElement(2)` k vytvoření nadpisu úrovně 2; číselný argument určuje úroveň nadpisu, která bude odražena ve stromu struktury PDF.

**Q: Co dělá `tagContent.SetTitle(\"PDF Example with Header\")`?**  
A: `SetTitle` zapíše zadaný řetězec do pole metadata názvu dokumentu PDF, které lze zobrazit v PDF prohlížečích a použít pro vyhledávání nebo indexování.

**Q: Co se stane, pokud vynechám `rootElement.AppendChild(header)`?**  
A: Prvek nadpisu nebude přidán do logického stromu struktury, takže se neobjeví ve výstupním PDF ani nebude rozpoznán jako nadpis pro nástroje přístupnosti.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}