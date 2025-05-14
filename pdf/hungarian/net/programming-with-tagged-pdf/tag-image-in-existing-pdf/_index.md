---
"description": "Ismerje meg, hogyan címkézheti a képeket meglévő PDF-fájlokban az Aspose.PDF for .NET használatával. Lépésről lépésre útmutató a PDF/UA-megfelelőség biztosításához és az akadálymentesítés javításához."
"linktitle": "Kép címkézése meglévő PDF-ben"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Kép címkézése meglévő PDF-ben"
"url": "/hu/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kép címkézése meglévő PDF-ben

## Bevezetés

Ebben az oktatóanyagban bemutatjuk, hogyan címkézhetsz fel egy képet egy meglévő PDF-ben az Aspose.PDF for .NET használatával. Az útmutató végére képes leszel alternatív szöveget beállítani a képekhez, módosítani az elrendezési attribútumokat, és biztosítani, hogy a PDF megfeleljen az akadálymentesítési szabványoknak.

## Előfeltételek

Mielőtt belevágnánk, nézzük át, mire lesz szükséged a kezdéshez:

- Aspose.PDF .NET-hez: Győződjön meg róla, hogy letöltötte és telepítette az Aspose.PDF .NET-hez legújabb verzióját. [Letöltés itt](https://releases.aspose.com/pdf/net/).
- .NET-keretrendszer: Győződjön meg arról, hogy rendelkezik egy .NET fejlesztői környezettel, például a Visual Studio-val.
- A PDF szerkezetének alapvető ismerete: Ismeri a PDF szerkezeti elemeit, például a bekezdéseket, a szakaszokat, a táblázatokat és a képeket.
- Érvényes licenc: Vagy vásárolhat licencet [itt](https://purchase.aspose.com/buy) vagy használjon egy ideigleneset [itt](https://purchase.aspose.com/temporary-license/).

## Csomagok importálása

A kódolás megkezdéséhez importálnod kell a szükséges névtereket az Aspose.PDF for .NET fájlból. Ezek hozzáférést biztosítanak a PDF dokumentum manipulálásához szükséges osztályokhoz és metódusokhoz.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Most, hogy előkészítettük a terepet, bontsuk le a kép címkézésének folyamatát több lépésre.

## 1. lépés: Töltse be a meglévő PDF dokumentumot

Az első lépés a kívánt PDF-fájl betöltése. Ez bármilyen PDF-fájl lehet, amelyben egy címkézni kívánt kép található.

```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Nyissa meg a dokumentumot
Document document = new Document(inFile);
```

- Csere `"YOUR DOCUMENT DIRECTORY"` a fájl tényleges elérési útjával.
- A `Document` Az osztály lehetővé teszi egy meglévő PDF betöltését. Ezt a PDF-et fogod módosítani a kép címkézéséhez.

## 2. lépés: Hozzáférés a címkézett tartalomhoz és a gyökérszerkezeti elemhez

Miután megnyitotta a PDF-et, a következő lépés a címkézett tartalom elérése és a gyökérstruktúra elem azonosítása. Ez kulcsfontosságú, mivel lehetővé teszi a PDF elemei közötti navigálást és a módosítások elvégzését.

```csharp
// Címkézett tartalom és gyökérstruktúra elem beszerzése
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` hozzáférést biztosít a PDF strukturált elemeihez.
- A `RootElement` a legfelső szerkezeti elem, amelyről lefelé haladva más elemekhez, például bekezdésekhez, táblázatokhoz és képekhez juthatunk el.

## 3. lépés: Címkézés beállítása a címkézett PDF dokumentumhoz

A címkézett PDF dokumentumhoz cím hozzáadása biztosítja a dokumentum megfelelő címkézését, ami hasznos az akadálymentesítés és a PDF/UA-megfelelőség szempontjából.

```csharp
// Címkézett PDF dokumentum címének beállítása
taggedContent.SetTitle("Document with images");
```

- címkézett PDF-hez cím beállítása javítja az akadálymentességet és a dokumentum áttekinthetőségét a képernyőolvasók és a kisegítő technológiák számára.

## 4. lépés: Keresd meg és címkézd meg a képet

Most keressük meg a képelemet (amelyet ún. `FigureElement` az Aspose.PDF fájlban), állítson be hozzá egy alternatív szöveget, és konfigurálja az elrendezési attribútumokat.

```csharp
// Végigmegy az összes ábraelemen (képen), és beállítja az alternatív szöveget és az elrendezési attribútumokat.
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Alternatív szöveg beállítása az ábrához
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // BBox attribútum (határolókeret) létrehozása és beállítása
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Az ábra elrendezési attribútumainak beállítása
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Ez a kód végigmegy az összes `FigureElement` a gyökérstruktúrában lévő objektumok, amelyek képeket ábrázolnak.
- Beállítja az akadálymentesítés alternatív szövegét (a képernyőolvasók ezt fogják használni a kép leírásához).
- A határolókeret (`BBox`) meghatározza a kép elrendezésének koordinátáit, biztosítva, hogy az helyesen jelenjen meg a dokumentumban.

## 5. lépés: Módosítsa a táblázatban található Span elemeket

Bizonyos esetekben szükség lehet a táblázaton belüli span elemek módosítására. Itt bemutatjuk, hogyan találhat meg egy `SpanElement` és helyezd át egy bekezdésbe.

```csharp
// A táblázat, a span és a paragraph elemek megkeresése
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// A span elem áthelyezése a bekezdésbe
spanElement.ChangeParentElement(paragraph);
```

- Itt találjuk meg a `TableElement`, `SpanElement`, és `ParagraphElement` a PDF-en belül.
- A `ChangeParentElement` módszerrel a szakaszt a bekezdésbe helyezzük a megfelelő címkézés és szerkezet biztosítása érdekében.

## 6. lépés: Mentse el a dokumentumot, és ellenőrizze a PDF/UA megfelelőségét

Miután az összes módosítást elvégezte, az utolsó lépés a frissített PDF mentése és annak ellenőrzése, hogy megfelel-e a PDF/UA szabványoknak.

```csharp
// Mentse el a frissített PDF dokumentumot
document.Save(outFile);

// PDF/UA megfelelőség ellenőrzése
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- A `Validate` A metódus ellenőrzi a PDF dokumentumot a PDF/UA szabványok alapján, és naplózza az eredményeket.
- A megfelelőség biztosítása segít javítani az akadálymentességet és megfelelni a dokumentumok közzétételére vonatkozó szabályozási követelményeknek.

## Következtetés

Ebben az oktatóanyagban bemutattuk, hogyan címkézhet képeket egy meglévő PDF-ben az Aspose.PDF for .NET használatával. Alternatív szöveg beállításával, elrendezési attribútumok módosításával és a dokumentum PDF/UA-megfelelőségének ellenőrzésével biztosíthatja, hogy PDF-fájljai akadálymentesek legyenek és megfeleljenek a modern szabványoknak. Az Aspose.PDF megkönnyíti a strukturált elemekkel való munkát, így Ön szabályozhatja a dokumentum elrendezését és akadálymentesítését.

## GYIK

### Mire használják az Aspose.PDF for .NET fájlt?
Az Aspose.PDF for .NET egy hatékony könyvtár, amely PDF dokumentumok programozott létrehozására, szerkesztésére és manipulálására szolgál .NET környezetben.

### Hogyan biztosíthatom a PDF/UA megfelelőséget?
Használhatod az Aspose.PDF fájlokat `Validate` módszer a PDF/UA megfelelőség ellenőrzésére a dokumentum módosítása után.

### Mi az alternatív szöveg a PDF fájlokban?
Az alternatív szöveg egy olyan leírás, amelyet a PDF-ekben található képekhez adnak a könnyebb hozzáférhetőség érdekében, különösen a képernyőolvasókat használó felhasználók számára.

### Lehetséges a táblázatok és terjedelmek módosítása egy PDF-ben az Aspose.PDF segítségével?
Igen, az Aspose.PDF lehetővé teszi a táblázatok, átfedések és más strukturált elemek kezelését egy PDF dokumentumban.

### Hol tudom letölteni az Aspose.PDF fájlt .NET-hez?
Letöltheti az Aspose.PDF legújabb verzióját .NET-hez [itt](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}