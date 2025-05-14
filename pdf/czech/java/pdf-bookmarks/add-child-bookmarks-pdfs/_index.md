---
"description": "Naučte se, jak vylepšit PDF dokumenty pomocí podřízených záložek pomocí Aspose.PDF pro Javu. Podrobný návod s příklady kódu pro lepší navigaci a organizaci."
"linktitle": "Přidání podřízených záložek do PDF souborů"
"second_title": "API pro zpracování PDF v Javě Aspose.PDF"
"title": "Přidání podřízených záložek do PDF souborů"
"url": "/cs/java/pdf-bookmarks/add-child-bookmarks-pdfs/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Přidání podřízených záložek do PDF souborů


## Úvod k přidávání podzáložek do PDF

tomto článku se podíváme na to, jak přidat podřízené záložky do PDF dokumentů pomocí Aspose.PDF pro Javu. Podřízené záložky představují pohodlný způsob, jak uspořádat a procházet obsah PDF dokumentu, což uživatelům usnadňuje nalezení konkrétních sekcí nebo témat v dokumentu.

## Předpoklady

Než se pustíme do implementace, ujistěte se, že máte splněny následující předpoklady:

- Vývojové prostředí Java nainstalované ve vašem systému.
- Aspose.PDF pro knihovnu Java. Můžete si ji stáhnout z [zde](https://releases.aspose.com/pdf/java/).

## Nastavení prostředí

1. Stáhněte si knihovnu Aspose.PDF pro Javu z uvedeného odkazu.
2. Přidejte knihovnu do svého projektu v Javě.

Nyní začněme vytvořením nového dokumentu PDF a postupným přidáváním podřízených záložek.

## Vytvoření nového PDF dokumentu

Pro začátek musíme inicializovat dokument PDF a přidat do něj stránky. Zde je úryvek kódu pro začátek:

```java
// Inicializace dokumentu PDF
Document pdfDocument = new Document();

// Přidání stránek do PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();
```

tomto příkladu jsme vytvořili nový dokument PDF a přidali do něj dvě stránky.

## Přidávání nadřazených záložek

Nadřazené záložky slouží jako hlavní sekce nebo kategorie ve vašem dokumentu PDF. Vytvořme si několik nadřazených záložek:

```java
// Vytvořit nadřazené záložky
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);
```

Přidali jsme dvě nadřazené záložky, „Nadřazená záložka 1“ a „Nadřazená záložka 2“.

## Přidávání podřízených záložek

Nyní je čas přidat podřízené záložky k nadřazeným záložkám, které jsme vytvořili dříve. Podřízené záložky představují specifická témata nebo podsekce v rámci každé nadřazené záložky. Zde je návod, jak to udělat:

```java
// Přidat podřízené záložky k nadřazené záložce 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Přidat podřízené záložky do nadřazené záložky 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);
```

Přidali jsme podzáložky do obou záložek „Nadřazená záložka 1“ i „Nadřazená záložka 2“.

## Přizpůsobení vzhledu záložek

Vzhled záložek si můžete přizpůsobit změnou jejich textu a stylu. Kromě toho můžete k záložkám přidat ikony pro lepší vizuální reprezentaci. Zde je příklad, jak to udělat:

```java
// Přizpůsobení vzhledu záložek
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());
```

V tomto příkladu jsme nadřazenou záložku zobrazili kurzívou, barvu textu podřízené záložky jsme změnili na zelenou a k podřízené záložce jsme přidali ikonu kurzívy.

## Zpracování událostí

Záložky mohou mít také přiřazené akce. Můžete například přidat akce, které se spustí, když uživatel klikne na záložku. Zde je návod, jak můžete zpracovat události kliknutí na záložku:

```java
// Přidání akce do záložky
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);
```

V tomto kódu jsme do podřízené záložky přidali akci „Přejít na“, která po kliknutí přesměruje uživatele na druhou stránku PDF.

## Uložení PDF souboru

Jakmile přidáte všechny potřebné záložky a upravíte jejich vzhled a akce, můžete upravený dokument PDF uložit:

```java
// Uložit dokument PDF
pdfDocument.save("output.pdf");
```

Váš PDF dokument s podřízenými záložkami je nyní připraven.

## Kompletní zdrojový kód

Zde je kompletní zdrojový kód pro přidání podřízených záložek do PDF dokumentu pomocí Aspose.PDF pro Javu:

```java
// Inicializace dokumentu PDF
Document pdfDocument = new Document();

// Přidání stránek do PDF
pdfDocument.getPages().add();
pdfDocument.getPages().add();

// Vytvořit nadřazené záložky
OutlineItemCollection outline = pdfDocument.getOutlines();
OutlineItemCollection parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 1");
outline.add(parentBookmark);

parentBookmark = new OutlineItemCollection(outline);
parentBookmark.setTitle("Parent Bookmark 2");
outline.add(parentBookmark);

// Přidat podřízené záložky k nadřazené záložce 1
OutlineItemCollection childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.1");
parentBookmark.add(childBookmark);

childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 1.2");
parentBookmark.add(childBookmark);

// Přidat podřízené záložky do nadřazené záložky 2
childBookmark = new OutlineItemCollection(outline);
childBookmark.setTitle("Child Bookmark 2.1");
parentBookmark.add(childBookmark);

// Přizpůsobení vzhledu záložek
parentBookmark.setItalic(true);
childBookmark.setForegroundColor(Color.getGreen());
childBookmark.setIcon(OutlineItemCollection.getItalicIcon());

// Přidání akce do záložky
GoToAction action = new GoToAction(pdfDocument.getPages().get_Item(1));
childBookmark.setAction(action);

// Uložit dokument PDF
pdfDocument.save("output.pdf");
```

## Závěr

Přidávání podřízených záložek do PDF souborů pomocí Aspose.PDF pro Javu je výkonná funkce, která vylepšuje navigaci a organizaci vašich dokumentů. Dodržováním kroků popsaných v tomto článku můžete vytvářet dobře strukturované PDF soubory s nadřazenými a podřízenými záložkami, přizpůsobovat jejich vzhled a dokonce přidávat akce pro zlepšení uživatelského prostředí.

## Často kladené otázky

### Jak si mohu stáhnout Aspose.PDF pro Javu?

Soubor Aspose.PDF pro Javu si můžete stáhnout z webových stránek [zde](https://releases.aspose.com/pdf/java/).

### Jsou podřízené záložky podporovány ve všech prohlížečích PDF?

Ano, podřízené záložky jsou podporovány ve většině moderních prohlížečů PDF a poskytují vylepšený uživatelský zážitek při navigaci v dokumentech PDF.

### Mohu si vzhled záložek dále přizpůsobit?

Ano, vzhled záložek si můžete přizpůsobit úpravou stylů textu, barev a ikon tak, aby odpovídaly designu vašeho dokumentu.

### Jaké další akce mohu přidat do záložek?

Kromě akcí „Přejít na“ můžete přidat akce jako „URI“ pro otevření webových odkazů nebo akce „JavaScript“ pro spuštění vlastních skriptů po kliknutí na záložku.

### Je Aspose.PDF pro Javu vhodný pro komerční projekty?

Ano, Aspose.PDF pro Javu je vhodný pro osobní i komerční projekty a nabízí širokou škálu funkcí pro manipulaci s PDF a jejich generování.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}