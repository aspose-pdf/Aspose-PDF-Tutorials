---
"description": "Tanuld meg, hogyan adhatsz meg sorközt PDF-ben az Aspose.PDF for .NET használatával ebből a lépésről lépésre szóló útmutatóból. Tökéletes azoknak a fejlesztőknek, akik precíz szövegformázást keresnek."
"linktitle": "Sorköz megadása PDF fájlban"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Sorköz megadása PDF fájlban"
"url": "/hu/net/programming-with-text/specify-line-spacing/"
"weight": 510
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Sorköz megadása PDF fájlban

## Bevezetés

Nehezen tudtad már szabályozni a sorközt egy PDF fájlban? Talán volt már olyan szöveged, ami túl zsúfoltnak tűnt, vagy egyszerűen nem tűnt olyan kidolgozottnak, mint szeretnéd. Ebben az oktatóanyagban bemutatjuk, hogyan adhatod meg egyszerűen a sorközt egy PDF-ben az Aspose.PDF for .NET segítségével. Egy egyszerű, lépésről lépésre bemutatott útmutató segítségével áttérhetsz egy üres PDF-ről egy olyanra, amely egyéni sorközt tartalmaz. Ez tökéletes, ha precíz szövegelrendezésre van szükséged olyan dokumentumokban, mint a jelentések, számlák vagy igazolások.

## Előfeltételek

Mielőtt belevágnánk a kódba, ellenőrizzük, hogy minden szükséges dolog megvan-e:

1. Aspose.PDF for .NET telepítve van. Ha nincs meg, töltse le innen: [Aspose.PDF letöltési oldal](https://releases.aspose.com/pdf/net/).
2. Egy .NET fejlesztői környezet (például a Visual Studio).
3. Egy TrueType betűtípusfájl (`.ttf`), amelyet a példában fogunk használni. Bármilyen betűtípust használhatsz, de ebben az útmutatóban a következőt fogjuk használni: `HPSimplified.TTF` betűtípus.
4. C# és PDF manipuláció alapismeretek.

Ha készen állsz, akkor folytassuk a szükséges csomagok importálásával.

## Csomagok importálása

A C# projektedben importálnod kell az Aspose.PDF névtereket a PDF funkciók használatához. Ezt így teheted meg:

```csharp
using Aspose.Pdf.Text;
using System.IO;
```

Ezek a névterek lehetővé teszik PDF dokumentumok létrehozását és kezelését, valamint a szövegformázási és betűtípus-beállítások módosítását.

Rövid lépésekre bontjuk, hogy könnyen követhesd. Minden lépés a folyamat egy kulcsfontosságú részére összpontosít, a PDF beállításától a sorköz megadásáig.

## 1. lépés: A projekt beállítása és a dokumentumkönyvtár meghatározása

Az első dolog, amit tennünk kell, az a fájljaink helyének meghatározása. Ez segít a programnak megtalálni a betűtípust és a PDF mentési helyét.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string fontFile = dataDir + "HPSimplified.TTF";
```

Ebben a lépésben kicseréled `"YOUR DOCUMENT DIRECTORY"` a fájlok tárolási helyének tényleges elérési útjával. Ide kell helyezni a betűtípusfájlt (`HPSimplified.TTF`) és hogy hová kerüljön a PDF mentésre.

## 2. lépés: PDF dokumentum betöltése

Most létre kell hoznunk egy új PDF dokumentumot. Ebben az útmutatóban egy üres dokumentummal kezdünk, de szükség esetén betölthetsz egy meglévő PDF-et is.

```csharp
Document doc = new Document();
```

Ez egy új, üres PDF dokumentumot hoz létre. Könnyű, ugye?

## 3. lépés: Szövegformázási beállítások megadása

Itt történik a varázslat. Megadjuk a PDF-hez hozzáadni kívánt szöveg sorközét. Az Aspose.PDF számos lehetőséget kínál, de ebben az útmutatóban a következőket fogjuk használni: `LineSpacingMode.FullSize`, amely biztosítja a sorköz teljes betartását.

```csharp
TextFormattingOptions formattingOptions = new TextFormattingOptions();
formattingOptions.LineSpacing = TextFormattingOptions.LineSpacingMode.FullSize;
```

Ez a kód a sorköz módját a következőre állítja be: `FullSize`biztosítva, hogy a szöveg megfelelő térközzel jelenjen meg. Vannak más lehetőségek is, például `Proportional` ha más térközhasználati viselkedést szeretnél, de most maradjunk ennél `FullSize`.

## 4. lépés: Szövegrészlet létrehozása

Most létrehozzuk a PDF-be helyezendő szöveget. Ez a szöveg tiszteletben fogja tartani az általunk meghatározott sorközt.

```csharp
TextFragment textFragment = new TextFragment("Hello world");
```

Létrehoztunk egy szövegrészletet a következő karakterlánccal: `"Hello world"`Természetesen ezt a szöveget tetszés szerint testreszabhatja.

## 5. lépés: Egyéni betűtípus betöltése és alkalmazása

Hogy a szöveg kiemelkedjen, betöltünk egy egyéni TrueType betűtípust egy fájlból. Ez a lépés opcionális, de professzionális megjelenést kölcsönözhet a PDF-fájloknak.

```csharp
if (fontFile != "")
{
    using (FileStream fontStream = System.IO.File.OpenRead(fontFile))
    {
        textFragment.TextState.Font = FontRepository.OpenFont(fontStream, FontTypes.TTF);
```

Itt betöltjük a betűtípusfájlt, és alkalmazzuk a szövegrészre. Ha a fájl elérési útja érvényes, a betűtípus kerül felhasználásra. Ellenkező esetben az alapértelmezett betűtípus kerül alkalmazásra.

## 6. lépés: A szöveg pozíciójának és formázásának beállítása

Ezután el kell helyeznünk a szöveget a PDF-en. Alkalmazzuk a korábban létrehozott formázási beállításokat is.

```csharp
textFragment.Position = new Position(100, 600);
textFragment.TextState.FormattingOptions = formattingOptions;
```

A `Position` metódus beállítja a szöveg megjelenítési helyét az oldalon (ebben az esetben 100 egység balról és 600 egység alulról). A formázási beállítások, beleértve a sorköz módját is, itt érvényesülnek.

## 7. lépés: Szöveg hozzáadása a PDF oldalhoz

Most, hogy a szöveg formázása és elhelyezése megtörtént, itt az ideje, hogy hozzáadjuk a PDF dokumentumhoz.

```csharp
var page = doc.Pages.Add();
page.Paragraphs.Add(textFragment);
```

Ez a kód létrehoz egy új oldalt a PDF dokumentumban, és hozzáadja a szövegrészletet.

## 8. lépés: Mentse el a PDF-et

Elértük az utolsó lépést! Most, hogy minden beállítva van, mentsük el a PDF-et.

```csharp
dataDir = dataDir + "SpecifyLineSpacing_out.pdf";
doc.Save(dataDir);
```

Ez a megadott sorközzel menti a PDF-et, és a fájl készen áll!

## Következtetés

És ennyi! Most létrehoztál egy PDF dokumentumot egyéni sorközzel az Aspose.PDF for .NET segítségével. Ez egy hatékony eszköz, amely lehetővé teszi a PDF fájlok minden aspektusának szabályozását, és ez csak egy példa arra, hogy mit érhetsz el. A szöveg elhelyezésétől a formázásig a lehetőségek végtelenek.

Ha mélyebben szeretnél belemerülni a PDF-manipulációba, az Aspose.PDF rengeteg funkciót kínál a felfedezésre. Ne habozz kísérletezni, és feszegesd a dokumentumokkal való munkavégzés határait!

## GYIK

### Be tudom állítani a sorközt más módokhoz?  
Igen, használhatsz más módokat is, pl. `Propvagytional` or `Fixed` az igényeidtől függően.

### Lehetséges betűtípusokat fájl helyett a rendszerből betölteni?  
Igen, betöltheti a rendszer által telepített betűtípusokat a következő használatával: `FontRepository`.

### Használhatom az Aspose.PDF for .NET fájlt más fájlformátumokkal?  
Abszolút! Az Aspose.PDF for .NET számos formátumot támogat, például XML-t, HTML-t és egyebeket.

### Szükségem van licencre az Aspose.PDF for .NET használatához?  
Igen, a teljes funkcionalitáshoz licencre lesz szükséged, amelyet beszerezhetsz [itt](https://purchase.aspose.com/buy).

### Hogyan tudom beállítani a sorközt több bekezdéshez?  
Jelentkezhet `TextFormattingOptions` mindegyikhez `TextFragment` vagy `TextParagraph` több sor vagy bekezdés térközének szabályozására.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}