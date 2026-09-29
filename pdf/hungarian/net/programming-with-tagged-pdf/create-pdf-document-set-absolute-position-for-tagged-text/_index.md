---
category: general
date: 2026-03-24
description: PDF-dokumentum létrehozása és a címkézett szöveg abszolút pozicionálásának
  megtanulása. Ez az útmutató bemutatja, hogyan adjon hozzá span elemet, hogyan adjon
  hozzá címkézett tartalmat, és hogyan helyezze el a szöveget az oldalon.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: hu
og_description: PDF dokumentum létrehozása, és azonnal megtekintheted, hogyan állíts
  be abszolút pozíciót, adj hozzá span elemet, és helyezd el a szöveget az oldalon
  címkézett PDF tartalommal.
og_title: PDF-dokumentum létrehozása – Címkézett szöveg abszolút pozicionálása
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF-dokumentum létrehozása – Címkézett szöveg abszolút pozíciójának beállítása
url: /hu/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF dokumentum létrehozása – Címkézett szöveg abszolút pozicionálása

Volt már szükséged **pdf dokumentum** létrehozására, amely hozzáférhető, címkézett szöveget tartalmaz, pontosan ott, ahol szeretnéd? Lehet, hogy egy űrlapszerű PDF-et építesz, ahol a címkét egy pontos koordinátán kell elhelyezni, vagy egy bizonyítványt generálsz, és a nevet tökéletesen kell illeszteni egy háttérképhez.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely megmutatja, **hogyan adhatunk hozzá címkézett** tartalmat, **abszolút pozíciót állíthatunk be**, és **span elemet adhatunk hozzá**, hogy **oldalon szöveget helyezhessünk el** találgatás nélkül. Nincsenek külső hivatkozások – csak a másolás‑beillesztésre készen álló kód, valamint a sorok mögötti „miért” magyarázatok.

## Előkövetelmények

- .NET 6+ (vagy .NET Framework 4.6+) C# fordítóval  
- Aspose.Pdf for .NET (a cikk írásakor legújabb verzió, 23.12) telepítve NuGet-en keresztül  
- Alapvető ismeretek a C# szintaxisról  

Ha ezek megvannak, kezdjünk bele.

---

## PDF dokumentum létrehozása – Az abszolút pozíció beállítása

Az első lépés egy üres `Document` példányosítása. Ez az objektum a teljes PDF fájlt képviseli, és hozzáférést biztosít a címkézett‑tartalom fához.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Miért fontos ez:**  
`Document` a PDF struktúra gyökere. Először létrehozva biztosítjuk, hogy legyen egy vászon a vizuális elemek (oldalak, grafikák) és a logikai struktúra (címkék) számára is. A `using` utasítás garantálja, hogy a fájl megfelelően el legyen engedve, ami megakadályozza a fájl‑kezelő szivárgásokat Windows rendszeren.

---

## Címkézett tartalom engedélyezése (Hogyan adjunk hozzá címkézetet)

Mielőtt bármilyen címkézett elemet beilleszthetnénk, a dokumentumnak *címkézett*ként kell legyen megjelölve. Az Aspose.Pdf automatikusan létrehozza a `TaggedContent` objektumot, de a jelzőt még mindig be kell kapcsolni.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Mi történik a háttérben?**  
`TaggedContent` `true`-ra állítása azt jelzi a PDF olvasóknak, hogy a fájl logikai struktúrafát tartalmaz. Ez kulcsfontosságú a képernyőolvasók számára, és ahhoz, hogy a `SetPosition` metódus helyesen működjön egy span elemen.

---

## A címkézett‑tartalom fa gyökérelemének lekérése

A gyökérelem a belépési pont minden strukturális címkéhez (például `<Document>`, `<Section>`, `<Span>`). Tekintsd úgy, mint a PDF láthatatlan „body”-ját.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Miért van szükségünk a gyökérre:**  
Minden későbbi címkét valahová a fában kell csatolni; ellenkező esetben nem jelennek meg a hozzáférhetőségi hierarchiában.

---

## Span elem hozzáadása – Az inline szöveg építőköve

A *span* a PDF megfelelője egy HTML `<span>`-nek – tökéletes rövid szövegrészekhez, amelyeket pontosan szeretnél elhelyezni.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Tervezési megjegyzés:**  
Ha gazdagabb formázásra (félkövér, dőlt, hiperhivatkozások) van szükséged, a span-t egy `<Paragraph>`-be csomagolhatod, vagy később `TextFragment` objektumokat használhatsz. Az abszolút pozicionáláshoz egy egyszerű span a legkönnyebb.

---

## Abszolút pozíció beállítása – X=100, Y=200

Most jön a szórakoztató rész: a span elhelyezése egy pontos helyen az oldalon. A koordináta-rendszer a bal‑alsó sarokból (0,0) indul, és pontokat használ (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Miért abszolút pozicionálás?**  
Amikor pixel‑pontos elrendezésre van szükség – gondolj bizonyítványokra, számlákra vagy űrlapokra – a relatív folyamat (például balról jobbra szöveg) nem elegendő. A `SetPosition` megkerüli a normál szövegfolyamatot, és a megadott helyre rögzíti az elemet.

---

## Szöveg hozzáadása a Span-hez

Miután a span el lett helyezve, most beillesztjük a tényleges karakterláncot.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Tipp:**  
Ha Unicode karakterekre vagy jobbról balra író írásrendszerekre van szükséged, egyszerűen add át a karakterláncot; az Aspose.Pdf automatikusan kezeli a kódolást.

---

## Span csatolása a gyökérelemhez

Végül csatoljuk a span-t a dokumentum logikai fához, hogy a végső PDF része legyen.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Mi van, ha kihagyod ezt a lépést?**  
A span a memóriában létezne, de soha nem lenne sorosítva a fájlba, így nem látnál szöveget, és a hozzáférhetőségi fa hiányos lenne.

---

## Teljes, futtatható példa

Az alábbiakban a teljes program látható, amelyet egy konzolos alkalmazásba illeszthetsz. Egy egyoldalas PDF-et hoz létre, egy címkézett span-t ad hozzá a (100, 200) koordinátán, és a fájlt `TaggedPositioned.pdf` néven menti.

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

**Várható kimenet:**  
Nyisd meg a `TaggedPositioned.pdf`-et bármely nézőben (Adobe Acrobat, Foxit stb.). Látni fogod a **„Positioned tagged text”** kifejezést pontosan 100 pt-re a bal szélétől és 200 pt-re az oldal alsó szélétől. Ha megnézed a *Tags* panelt, egy `<Span>` elem lesz felsorolva a dokumentum gyökere alatt, ami megerősíti, hogy a tartalom megfelelően címkézett.

---

## Gyakori kérdések és szélhelyzetek

### Mi van, ha egy adott oldalon kell elhelyezni a szöveget, nem az elsőn?

Add hozzá a kívánt oldalt (`var page = pdfDocument.Pages[3];`) a `SetPosition` hívása előtt. A span automatikusan az aktív oldal kontextusához csatolódik.

### Beállíthatom a pozíciót hüvelykben vagy centiméterben?

`SetPosition` pontokat fogad. Alakítsd át a következő képletekkel:  
- **Hüvelyk → pont:** `points = inches * 72`  
- **Centiméter → pont:** `points = cm * 28.3465`

### Hogyan változtathatom meg a span betűtípusát vagy színét?

A span létrehozása után lekérheted a `TextState`-jét és módosíthatod:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Mi van, ha a dokumentumnak már vannak meglévő címkéi?

Még mindig létrehozhatsz egy új span-t és hozzáfűzheted bármely meglévő elemhez (`rootElement`, egy konkrét `<Section>` stb.). Ügyelj arra, hogy logikai hierarchiát tarts fenn – a képernyőolvasók jól felépített fát várnak.

### Működik ez PDF/A vagy PDF/UA megfelelőséggel?

Igen. A címkézett PDF-ek alapkövetelményei a PDF/UA-nak. Ha PDF/A-ra van szükséged, a tartalom építése után állítsd be a `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));`-t.

---

## Pro tippek és buktatók

- **Pro tipp:** Mindig adj hozzá egy oldalt a tartalom pozicionálása előtt. Oldal nélkül a `SetPosition` csendben hibázik, mert nincs hová renderelni.  
- **Figyelj az egységekre:** A UI tervezésből származó pixelek keverése PDF pontokkal eltolja a szöveget. Ellenőrizd a konverziót.  
- **Teljesítmény tipp:** Ha több ezer PDF-et generálsz, használd újra ugyanazt a `Document` példányt, és a futások között hívd meg a `pdfDocument.Pages.Clear()`-t, hogy elkerüld a túlzott memóriafoglalást.  
- **Hozzáférhetőségi emlékeztető:** A címkézés nem csak egy plusz funkció; számos szabályozás (Section 508, EN 301 549) megköveteli. A `CreateSpanElement` használata biztosítja, hogy a szöveg felfedezhető legyen a segítő technológiák által.

---

## Következtetés

Most **pdf dokumentumot** hoztunk létre a semmiből, **abszolút pozíciót állítottunk be**, **span elemet adtunk hozzá**, és bemutattuk, **hogyan adjunk hozzá címkézett** tartalmat, hogy **oldalon szöveget helyezzünk el** pixel‑pontos pontossággal. A teljes példa készen áll a futtatásra, és a magyarázat mind a *hogyan*, mind a *miért* kérdésre választ ad – pontosan azt, amit a fejlesztők (és AI asszisztensek) keresnek, amikor megbízható megoldásra van szükségük.

Ezután érdemes lehet felfedezni:

- Képek hozzáadása a pozicionált szöveg mögé vízjelezett bizonyítványokhoz.  
- `CreateParagraphElement` használata több soros blokkokhoz, amelyeknek továbbra is abszolút elhelyezésre van szükségük.  
- Exportálás PDF/UA formátumba a szigorú hozzáférhetőségi auditok teljesítéséhez.  

Nyugodtan módosítsd a koordinátákat, betűtípusokat vagy színeket – a kísérletezés a leggyorsabb módja a címkézett PDF generálásának elsajátításához. Ha elakadsz, hagyj egy megjegyzést alább; jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}