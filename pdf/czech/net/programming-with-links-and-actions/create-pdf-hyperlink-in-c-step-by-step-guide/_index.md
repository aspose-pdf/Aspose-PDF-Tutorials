---
category: general
date: 2026-02-20
description: Rychle vytvořte hypertextový odkaz v PDF a vložte odkaz do PDF pomocí
  C#. Naučte se, jak propojit konkrétní stránku PDF a během několika minut převést
  DOCX na PDF odkaz.
draft: false
keywords:
- create pdf hyperlink
- link specific pdf page
- embed link pdf
- create clickable pdf link
- convert docx pdf link
language: cs
og_description: Vytvořte hypertextový odkaz na PDF okamžitě. Tento návod ukazuje,
  jak odkazovat na konkrétní stránku PDF, vložit odkaz do PDF a převést DOCX na PDF
  odkaz pomocí C#.
og_title: Vytvořte hypertextový odkaz na PDF v C# – kompletní tutoriál
tags:
- C#
- PDF
- Aspose
title: Vytvoření hypertextového odkazu v PDF v C# – krok za krokem
url: /cs/net/programming-with-links-and-actions/create-pdf-hyperlink-in-c-step-by-step-guide/
---

the image line unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření hypertextového odkazu PDF v C# – krok za krokem průvodce

Už jste někdy potřebovali **create PDF hyperlink**, ale nebyli jste si jisti, která API volání skutečně odkaz funguje? Nejste sami – většina vývojářů narazí na stejnou překážku při převodu DOCX na PDF, který přeskakuje přímo na konkrétní stránku. Dobrá zpráva? S několika řádky C# můžete vložit odkaz, nasměrovat jej na libovolnou stránku a během chvilky mít hotové PDF.

V tomto tutoriálu projdeme převodem Word dokumentu na PDF **a** přidáním klikatelné oblasti, která odkazuje na konkrétní stránku PDF. Během toho se také dotkneme toho, jak **embed link PDF** v jiných pracovních postupech a proč byste mohli chtít **link specific PDF page** místo pouhého připojení souboru. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu.

## Co se naučíte

- Načíst soubor DOCX a převést jej na PDF pomocí Aspose.Words (nebo jakékoli kompatibilní knihovny).
- Vytvořit anotaci **create clickable PDF link**, která ukazuje na cílovou stránku.
- Definovat obdélníkovou oblast, na kterou uživatelé skutečně klikají.
- Uložit finální PDF a ověřit, že hypertextový odkaz funguje.
- Běžné úskalí při **convert docx pdf link** a jak se jim vyhnout.

### Požadavky

- .NET 6.0 nebo novější (kód funguje také s .NET Framework 4.6+).
- Nainstalované NuGet balíčky Aspose.Words a Aspose.Pdf (`dotnet add package Aspose.Words` a `dotnet add package Aspose.Pdf`).
- Jednoduchý soubor DOCX pojmenovaný `input.docx` umístěný ve složce, kterou ovládáte.

Žádná složitá konfigurace není potřeba – stačí několik using direktiv a jste připraveni.

![Create PDF Hyperlink example](image.png "Create PDF Hyperlink")

## Vytvoření PDF hypertextového odkazu – přehled

Základní myšlenka operace **create PDF hyperlink** má dva aspekty:

1. **Annotation** – PDF používá *link annotations* k popisu klikatelné oblasti.  
2. **Destination** – Anotace ukazuje na objekt *destination*, který může být číslo stránky, pojmenovaný pohled nebo externí URL.

Když spojíte tyto dva prvky, získáte plně funkční odkaz, který se chová jako ty, které vidíte v Adobe Readeru. Níže uvedený kód přesně tento vzor následuje.

## Step 1: Load the Source DOCX

Nejprve musíme načíst Word dokument do paměti. Aspose.Words se stará o těžkou práci převodu DOCX na PDF v pozadí.

```csharp
using Aspose.Words;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source DOCX file
Document docx = new Document("YOUR_DIRECTORY/input.docx");

// Convert the Word document to a PDF object (in memory)
using var pdfStream = new MemoryStream();
docx.Save(pdfStream, SaveFormat.Pdf);
pdfStream.Position = 0;

// Create an Aspose.Pdf Document from the memory stream
Document pdfDoc = new Document(pdfStream);
```

*Proč tento krok?*  
Načtení DOCX pomocí `Aspose.Words.Document` zaručuje, že všechny styly, obrázky a zalomení stránek přežijí převod. Uložením do `MemoryStream` se vyhneme vytvoření mezisouboru na disku – malý výkonový zisk a čistší workflow, když později **embed link pdf** do dalších služeb.

## Step 2: Create a Link Annotation

Nyní, když máme PDF objekt, můžeme přidat link anotaci. Představte si ji jako lepkavou poznámku, která říká divákovi „klikněte zde“.

```csharp
// Create a new link annotation object
LinkAnnotation link = pdfDoc.Pages[1].Annotations.AddLink(
    new Rectangle(0, 0, 0, 0)); // Temporary rectangle; we'll set proper coordinates next
```

*Proč použít `AddLink`?*  
`AddLink` automaticky registruje anotaci do kolekce anotací stránky, což je nezbytné, aby PDF prohlížeč rozpoznal klikací oblast. Můžete také ručně vytvořit `LinkAnnotation`, ale pomocná metoda udržuje kód stručný.

## Step 3: Define the Clickable Rectangle

Obdélník určuje, kde na stránce může uživatel kliknout. PDF souřadnice jsou měřeny v bodech (1/72 palce) s počátkem v levém dolním rohu.

```csharp
// Define the rectangle (left, bottom, right, top) in points
// Here we place the link near the top of the page, spanning 150 points wide
link.Rect = new Rectangle(50, 700, 200, 720);
```

*Proč tyto hodnoty?*  
Hodnoty `50, 700, 200, 720` vytvoří krabici širokou 150 bodů a vysokou 20 bodů, umístěnou přibližně 1 palec od levého okraje a blízko horní části standardní stránky Letter. Přizpůsobte souřadnice svému rozvržení – pokud umisťujete odkaz pod nadpis, pravděpodobně budete potřebovat nižší hodnotu `bottom`.

## Step 4: Set the Destination Page (Link Specific PDF Page)

Chceme, aby odkaz přeskákal na stránku 2 (index od nuly 1) ve stejném PDF. To je klasický scénář „link specific PDF page“.

```csharp
// Destination page index is zero‑based; 1 points to the second page
Destination dest = new Destination(1);

// Assign the destination to the annotation
link.Destination = dest;

// Optional: Change the appearance to look like a typical hyperlink (blue, underlined)
link.Color = Color.Blue;
link.Border = new Border(link) { Width = 0 };
```

*Proč objekt `Destination`?*  
PDF podporuje mnoho typů destinací (fit page, zoom, atd.). Použitím jednoduchého konstruktoru s indexem stránky získáme výchozí chování „fit page“, což je to, co většina uživatelů očekává při kliknutí na odkaz.

## Step 5: Save the Modified PDF

Nakonec zapíšeme aktualizované PDF na disk. Výstupní soubor nyní obsahuje **create clickable PDF link**, který přeskakuje na druhou stránku.

```csharp
// Save the PDF with the new hyperlink
pdfDoc.Save("YOUR_DIRECTORY/output.pdf");
```

A to je vše – vaše PDF je připravené a odkaz funguje v jakémkoli standardním prohlížeči.

## Testování hypertextového odkazu

Otevřete `output.pdf` v Adobe Readeru nebo jakémkoli moderním PDF prohlížeči. Přesuňte kurzor nad modrý obdélník; kurzor by se měl změnit na ruku. Kliknutím se okamžitě přepne na stránku 2. Pokud se nic nestane, zkontrolujte souřadnice obdélníku a ujistěte se, že index destinace odpovídá existující stránce.

## Běžná úskalí a jak se jim vyhnout

| Symptom | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| Odkaz nefunguje | Index cílové stránky mimo rozsah | Ověřte `pdfDoc.Pages.Count` a použijte platný index (od nuly). |
| Obdélník se zobrazuje na špatném místě | Zmatek v souřadnicovém systému PDF (počátek dole vlevo) | Pamatujte, že Y = 0 je spodní část stránky; zvýšením Y posunete nahoru. |
| Barva odkazu neviditelná | Barva anotace není nastavena nebo ji přepisuje prohlížeč | Explicitně nastavte `link.Color = Color.Blue` a `link.Border.Width = 0`. |
| Velikost PDF roste | Ukládání mezilehlého PDF na disk před přidáním anotace | Použijte `MemoryStream` jak je ukázáno, aby byl celý proces v paměti. |

## Okrajové případy a varianty

### Odkaz na externí URL

Pokud potřebujete **embed link PDF**, který ukazuje mimo dokument, nahraďte přiřazení `Destination` za `LinkAction`:

```csharp
link.Action = new LinkAction("https://example.com");
```

### Přidání více odkazů na různých stránkách

Jednoduše projděte stránky v cyklu a pro každou vytvořte nový `LinkAnnotation`. Nezapomeňte upravit souřadnice obdélníku pro rozvržení každé stránky.

```csharp
for (int i = 1; i <= pdfDoc.Pages.Count; i++)
{
    var page = pdfDoc.Pages[i];
    var link = page.Annotations.AddLink(new Rectangle(50, 50, 150, 70));
    link.Destination = new Destination(i - 1); // Jump to the same page (self‑link)
}
```

### Použití pojmenovaných destinací

Místo číselného indexu můžete vytvořit pojmenovanou destinaci, což je užitečné, pokud se pořadí stránek později může změnit.

```csharp
pdfDoc.NamedDestinations.Add("ChapterTwo", new Destination(1));
link.Destination = new Destination("ChapterTwo");
```

## Další kroky – Embed Link PDF ve větších pracovních postupech

Nyní, když můžete programově **create PDF hyperlink**, zvažte následující nápady:

- **Batch processing**: Procházet složku souborů DOCX, převést každý a přidat odkaz na stránku obsahu.  
- **Dynamic PDF reports**: Vygenerovat souhrnnou stránku s odkazy na podrobné sekce – ideální pro auditní záznamy.  
- **Web services**: Zveřejnit API endpoint, který přijme DOCX, přidá **create clickable PDF link** a vrátí PDF jako bajty.  

Všechny tyto scénáře staví na stejných základních konceptech, které jsme pokryli: načítání, anotování a ukládání.

---

### TL;DR

Ukázali jsme, jak **create PDF hyperlink** v C# pomocí načtení DOCX, přidání link anotace, definování klikatelného obdélníku, nastavení destinace na **link specific PDF page** a nakonec uložení výsledku. Stejný vzor vám umožní **embed link PDF**, **create clickable PDF link**, nebo dokonce **convert DOCX PDF link** pro složitější automatizační pipeline.

Klidně experimentujte – změňte velikost obdélníku, nasměrujte na jiné stránky nebo zaměňte externí URL. Pokud narazíte na problémy, podívejte se znovu na tabulku „Běžná úskalí“ nebo zanechte komentář níže. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}