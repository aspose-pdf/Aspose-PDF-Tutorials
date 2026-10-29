---
title: Testreszabja a táblázat celláinak háttérszínét, szegélyeit és kitöltését (padding) PDF-ekben az Aspose.Pdf for .NET segítségével
weight: 101
limit:
description: Tudja meg, hogyan hozhat létre PDF-et egy kétoszlopos táblázattal, és alkalmazhat egyedi háttérszíneket, szegélyeket és kitöltést minden cellára az Aspose.Pdf for .NET segítségével.
keywords: [Aspose.Pdf for .NET, style table cells pdf, pdf table cell background, pdf table cell border, pdf cell padding, Aspose PDF table styling]
url: /net/tables-lists/style-table-cells/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Tudja meg, hogyan hozhat létre PDF-et egy kétoszlopos táblázattal,
    és alkalmazhat egyedi háttérszíneket, szegélyeket és kitöltést minden cellára
    az Aspose.Pdf for .NET segítségével.
  headline: Testreszabja a táblázat celláinak háttérszínét, szegélyeit és kitöltését
    (padding) PDF-ekben az Aspose.Pdf for .NET segítségével
  type: TechArticle
- description: Tudja meg, hogyan hozhat létre PDF-et egy kétoszlopos táblázattal,
    és alkalmazhat egyedi háttérszíneket, szegélyeket és kitöltést minden cellára
    az Aspose.Pdf for .NET segítségével.
  name: Testreszabja a táblázat celláinak háttérszínét, szegélyeit és kitöltését (padding)
    PDF-ekben az Aspose.Pdf for .NET segítségével
  steps:
  - name: Hozzon létre egy új üres PDF dokumentumot egy using blokkban.
    text: Hozzon létre egy új üres PDF dokumentumot egy using blokkban.
  - name: Adjon hozzá egy üres oldalt a PDF dokumentumhoz.
    text: Adjon hozzá egy üres oldalt a PDF dokumentumhoz.
  - name: Hozzon létre egy Table objektumot, amely két 200 pontos oszlopból áll, vékony
      fekete külső szegéllyel, és alapértelmezett cella kitöltéssel (padding) 5 pont.
    text: Hozzon létre egy Table objektumot, amely két 200 pontos oszlopból áll, vékony
      fekete külső szegéllyel, és alapértelmezett cella kitöltéssel (padding) 5 pont.
  - name: Adja hozzá az első sort a táblázathoz.
    text: Adja hozzá az első sort a táblázathoz.
  - name: Hozza létre az első cellát, illessze be a "First cell" szöveget, állítsa
      be a világossárga háttérszínt, a 2 pontos piros szegélyt és a 4 pontos margót.
    text: Hozza létre az első cellát, illessze be a "First cell" szöveget, állítsa
      be a világossárga háttérszínt, a 2 pontos piros szegélyt és a 4 pontos margót.
  - name: Hozza létre a második cellát, adja hozzá a "Second cell" szöveget, állítsa
      be a világoszöld háttérszínt, a 2 pontos kék szegélyt és a 4 pontos margót.
    text: Hozza létre a második cellát, adja hozzá a "Second cell" szöveget, állítsa
      be a világoszöld háttérszínt, a 2 pontos kék szegélyt és a 4 pontos margót.
  - name: Adja hozzá a második sort a táblázathoz.
    text: Adja hozzá a második sort a táblázathoz.
  - name: Hozza létre a harmadik cellát, illessze be a "Third cell" szöveget, állítsa
      be a világos cián háttérszínt, a sötétszürke 2 pontos szegélyt és a 4 pontos
      margót.
    text: Hozza létre a harmadik cellát, illessze be a "Third cell" szöveget, állítsa
      be a világos cián háttérszínt, a sötétszürke 2 pontos szegélyt és a 4 pontos
      margót.
  - name: Hozza létre a negyedik cellát, adja hozzá a "Fourth cell" szöveget, állítsa
      be a világos rózsaszín háttérszínt, a lila 2 pontos szegélyt és a 4 pontos margót.
    text: Hozza létre a negyedik cellát, adja hozzá a "Fourth cell" szöveget, állítsa
      be a világos rózsaszín háttérszínt, a lila 2 pontos szegélyt és a 4 pontos margót.
  - name: Adja hozzá a teljesen stílusos táblázatot az oldalhoz, hogy megjelenjen
      a PDF-ben.
    text: Adja hozzá a teljesen stílusos táblázatot az oldalhoz, hogy megjelenjen
      a PDF-ben.
  - name: Mentse a PDF dokumentumot egy fájlba, és zárja le a using blokkot.
    text: Mentse a PDF dokumentumot egy fájlba, és zárja le a using blokkot.
  - name: Írjon ki egy megerősítő üzenetet a konzolra.
    text: Írjon ki egy megerősítő üzenetet a konzolra.
  type: HowTo
- questions:
  - answer: '`DefaultCellPadding` alap kitöltést biztosít minden cellához, de ha `Margin`-t
      (pl. `cellA1.Margin = new MarginInfo(...)`) ad meg, a margó értékek felülírják
      az alap kitöltést az adott cellában.'
    question: A `Table`-on beállított `DefaultCellPadding` hatással van-e azokra a
      cellákra, amelyeknél `Margin` is definiálva van?
  - answer: '`Table.Border` nélkül a teljes táblázatot körülvevő külső téglalap kimarad;
      csak az egyes cellákra beállított szegélyek (pl. `cellA2.Border`) lesznek láthatóak.'
    question: Mi lesz a PDF kinézete, ha eltávolítom a `Border` tulajdonságot a `Table`
      objektumból?
  - answer: Igen, hozzon létre egy `BorderInfo`-t egy adott `BorderSide`-del (pl.
      `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) és rendelje hozzá
      a cella `Border` tulajdonságához.
    question: Lehet-e egy cellának különböző szegélyvastagságot adni minden oldalra?
  - answer: Hozzon létre egy új `Row`-t a `Row newRow = dataTable.Rows.Add();` kóddal,
      majd adjon cellákat a `newRow.Cells`-hez, akárcsak a korábbi soroknál.
    question: Hogyan adhatok hozzá egy harmadik sort a táblázathoz a bemutatott kód
      után?
  type: FAQPage
images:
- /net/tables-lists/style-table-cells/og-image.png
og_title: PDF táblázat cellák stílusozása – háttér, szegély, kitöltés
og_description: Gyorsan formázza a PDF táblázat celláit egyedi színekkel, szegélyekkel és térközzel az Aspose.Pdf for .NET használatával.
og_image_alt: Útmutató, amely bemutatja, hogyan lehet stílusozni a táblázat cellák háttérszínét, szegélyét és kitöltését (padding) PDF-ben az Aspose.Pdf for .NET segítségével
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Testreszabja a táblázat celláinak háttérszínét, szegélyeit és kitöltését (padding) PDF-ekben az Aspose.Pdf for .NET segítségével
Ezen a bemutatón láthatja, hogyan lehet PDF dokumentumot generálni, egy kétoszlopos táblázatot hozzáadni, és pontosan szabályozni minden cella megjelenését. Háttérszínek beállításával, szegélyek meghatározásával és a kitöltés (padding) módosításával a táblázat adatai kiemelkedhetnek és kifinomultak lehetnek. A példa az Aspose.Pdf Document és Table osztályokat használja minden stílusbeállítás bemutatására.

---

{{< tutorial-widget sourcePath="pdf/net/tables-lists/style-table-cells" >}}


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

**Q: A `Table`-on beállított `DefaultCellPadding` hatással van-e azokra a cellákra, amelyeknél `Margin` is definiálva van?**  
A: `DefaultCellPadding` alap kitöltést biztosít minden cellához, de ha `Margin`-t (pl. `cellA1.Margin = new MarginInfo(...)`) ad meg, a margó értékek felülírják az alap kitöltést az adott cellában.

**Q: Mi lesz a PDF kinézete, ha eltávolítom a `Border` tulajdonságot a `Table` objektumból?**  
A: `Table.Border` nélkül a teljes táblázatot körülvevő külső téglalap kimarad; csak az egyes cellákra beállított szegélyek (pl. `cellA2.Border`) lesznek láthatóak.

**Q: Lehet-e egy cellának különböző szegélyvastagságot adni minden oldalra?**  
A: Igen, hozzon létre egy `BorderInfo`-t egy adott `BorderSide`-del (pl. `new BorderInfo(BorderSide.Left, 3, Aspose.Pdf.Color.Black)`) és rendelje hozzá a cella `Border` tulajdonságához.

**Q: Hogyan adhatok hozzá egy harmadik sort a táblázathoz a bemutatott kód után?**  
A: Hozzon létre egy új `Row`-t a `Row newRow = dataTable.Rows.Add();` kóddal, majd adjon cellákat a `newRow.Cells`-hez, akárcsak a korábbi soroknál.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}