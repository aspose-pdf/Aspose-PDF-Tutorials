---
"description": "Ismerje meg, hogyan lehet szöveget kinyerni egy PDF dokumentumból a .NET-hez készült Aspose.PDF szövegeszközével."
"linktitle": "Szöveg kinyerése szöveges eszközzel"
"second_title": "Aspose.PDF .NET API referenciafájlhoz"
"title": "Szöveg kinyerése szöveges eszközzel"
"url": "/hu/net/programming-with-text/extract-text-using-text-device/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése szöveges eszközzel

## Bevezetés

A szöveg kinyerése PDF-ből bonyolult lehet, különösen, ha olyan dokumentumokról van szó, amelyek különböző formátumúak, beágyazott betűtípusokkal vagy összetett elrendezésekkel rendelkeznek. De az Aspose.PDF for .NET segítségével ez a folyamat gyerekjáték lesz! Akár egy PDF oldalait szeretnéd egyszerű szöveggé konvertálni további elemzés céljából, akár csak bizonyos részeket kell kinyerned, az Aspose.PDF ezt is segíti. Ebben az oktatóanyagban lépésről lépésre bemutatjuk, hogyan lehet szöveget kinyerni egy PDF-ből az Aspose.PDF TextDevice osztályának használatával. Világos magyarázatokat is adunk, így könnyedén alkalmazhatod ugyanazokat a módszereket a saját projektjeidben.

## Előfeltételek

Mielőtt belevágnánk a kódba, győződjünk meg róla, hogy minden a helyén van a folytatáshoz. Íme, amire szükséged lesz:

1. Aspose.PDF .NET-hez: Töltse le a legújabb verziót innen: [Aspose.PDF .NET letöltési oldalhoz](https://releases.aspose.com/pdf/net/).
2. Fejlesztői környezet: Visual Studio vagy bármilyen más C# fejlesztői környezet.
3. .NET-keretrendszer: Győződjön meg arról, hogy a projekt a .NET-keretrendszer 4.x-es vagy újabb verzióját célozza meg.
4. Bemeneti PDF-fájl: Egy PDF-fájl, amelyet szöveg kinyerésére fog használni. Helyezze el ezt a gépén egy könyvtárban (erre a továbbiakban úgy hivatkozunk, mint `YOUR DOCUMENT DIRECTORY`).

## Csomagok importálása

A kód tetején importálnod kell a szükséges névtereket az Aspose.PDF használatához:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Devices;
using System;
using System.Text;
```

## 1. lépés: Töltse be a PDF dokumentumot

A szöveg kinyerése előtt be kell töltenünk a PDF dokumentumot a memóriába. Ebben a lépésben az Aspose.PDF fájljaival nyitjuk meg a PDF dokumentumot. `Document` osztály. Ez lehetővé teszi a fájlban található összes oldal és tartalom elérését.

```csharp
// Adja meg a PDF dokumentum elérési útját
string dataDir = "YOUR DOCUMENT DIRECTORY";

// PDF dokumentum betöltése
Document pdfDocument = new Document(dataDir + "input.pdf");
```

Itt használjuk `Document pdfDocument = new Document(dataDir + "input.pdf");` a PDF betöltéséhez. `dataDir` változó a PDF-fájl könyvtárelérési útját tartalmazza. Ez hozzáférést biztosít a teljes dokumentumhoz, lehetővé téve számunkra, hogy az oldalak között végighaladjunk és a tartalmat kinyerjük.

## 2. lépés: Szövegtároláshoz használható karakterlánc-szerkesztő beállítása

Most, hogy a dokumentum betöltődött, szükségünk van egy módszerre a kinyert szöveg tárolására. Ehhez egy `StringBuilder` amely lehetővé teszi a hatékony karakterlánc-összefűzést.

```csharp
// StringBuilder a kivont szöveg tárolására
StringBuilder builder = new StringBuilder();
```

Inicializálunk egy `StringBuilder` példány, amely az egyes oldalakról kinyert szöveget gyűjti össze. Ez egy hatékonyabb módja a nagy karakterláncok kezelésének, mint a ciklusban történő hagyományos karakterlánc-összefűzés.

## 3. lépés: PDF oldalak ismétlése

Ezután végigmegyünk a PDF dokumentum minden oldalán, hogy kinyerjük a szöveget. Minden oldalt külön-külön fogunk feldolgozni a `TextDevice` osztály, amely a PDF tartalom szöveges formátumba konvertálásáért felelős.

```csharp
// Végigpörgetés a PDF összes oldalán
foreach (Page pdfPage in pdfDocument.Pages)
{
    // Minden oldal feldolgozása szöveg kinyeréséhez
}
```

Ez a ciklus végigmegy a PDF minden oldalán (`pdfDocument.Pages`). Minden oldalról kinyerjük a szöveget, és hozzáadjuk a `StringBuilder`.

## 4. lépés: Szöveg kinyerése minden oldalról

Most beállítjuk a szövegkinyerési folyamatot minden oldalhoz. Itt létrehozunk egy `TextDevice` objektumot, és használja azt a PDF oldalak feldolgozásához. `TextDevice` nyers vagy formázott szöveget nyer ki a beállított kinyerési beállítások alapján.

```csharp
using (MemoryStream textStream = new MemoryStream())
{
    // Szöveges eszköz létrehozása szöveg kinyeréséhez
    TextDevice textDevice = new TextDevice();
    
    // A szövegkiemelési beállításokat „Tiszta” módra kell állítani
    TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);
    textDevice.ExtractionOptions = textExtOptions;

    // Szöveg kinyerése az aktuális oldalról és mentése a memóriafolyamba
    textDevice.Process(pdfPage, textStream);

    // Memóriafolyam szöveggé konvertálása
    string extractedText = Encoding.Unicode.GetString(textStream.ToArray());

    // A kivont szöveg hozzáfűzése a StringBuilderhez
    builder.Append(extractedText);
}
```

- `TextDevice textDevice = new TextDevice();`A `TextDevice` Az osztály szöveg kinyerésére szolgál a PDF-ből.
- `TextExtractionOptions textExtOptions = new TextExtractionOptions(TextExtractionOptions.TextFormattingMode.Pure);`: Ez a beállítás a nyers szöveget kinyeri a formázás, például a betűtípusok vagy a pozíciók megőrzése nélkül. Használhatja ezt is: `TextFormattingMode.Raw` ha nagyobb kontrollra van szükséged a formázás felett.
- `textDevice.Process(pdfPage, textStream);`: Ez a funkció feldolgozza a PDF minden egyes oldalát, és a kinyert szöveget egy fájlban tárolja. `MemoryStream`.
- Végül konvertáljuk a szöveget a következőből: `MemoryStream` egy karakterlánchoz, és hozzáfűzi a `StringBuilder`.

## 5. lépés: Mentse el a kibontott szöveget egy fájlba

Az összes oldal feldolgozása után a szöveg a következő helyen tárolódik: `StringBuilder`Az utolsó lépés a kibontott szöveg fájlba mentése.

```csharp
// A szövegfájl kimeneti elérési útjának meghatározása
dataDir = dataDir + "input_Text_Extracted_out.txt";

// Mentse el a kibontott szöveget egy fájlba
File.WriteAllText(dataDir, builder.ToString());

Console.WriteLine("\nText extracted successfully from PDF document.\nFile saved at " + dataDir);
```

- `File.WriteAllText(dataDir, builder.ToString());`: Ez kiírja a teljes tartalmat `StringBuilder` egy szövegfájlba.
- A kimeneti fájl elérési útját egy fájlnév hozzáfűzésével állítjuk be (`"input_Text_Extracted_out.txt"`) a `dataDir` útvonal.

## Következtetés

A szöveg kinyerése PDF-ből az Aspose.PDF for .NET segítségével egy egyszerű és hatékony folyamat. Az útmutatóban ismertetett lépéseket követve könnyedén megnyithatja a PDF dokumentumokat, végiglapozhatja az oldalakat, és kinyerheti a szöveget egy szövegfájlba. Ez különösen hasznos nagy mennyiségű PDF adat feldolgozásakor, szövegelemzés elvégzéséhez vagy dokumentumok további kezelés céljából történő konvertálásához.

Az Aspose.PDF segítségével nem csak szöveget lehet kinyerni – kezelni lehet a jegyzeteket, manipulálni a képeket, sőt PDF-eket is lehet konvertálni más formátumokba, például HTML-be vagy Wordbe. A könyvtár rugalmassága és teljesítménye felbecsülhetetlen értékű eszközzé teszi a PDF-ek kezeléséhez a .NET alkalmazásokban.

## GYIK

### Az Aspose.PDF képes szöveget kinyerni képalapú PDF-ekből?
Nem, az Aspose.PDF tartalomalapú PDF-ekből való szöveg kinyerésére szolgál. Képalapú PDF-ekhez OCR technológia szükséges.

### Az Aspose.PDF megőrzi a formázást a szöveg kinyerésekor?
Alapértelmezés szerint a szöveg formázás nélkül kerül kinyerésre, de a kinyerési beállítások módosításával megőrizheti a formázás egy részét.

### Ki tudok nyerni szöveget egy adott oldaltartományból?
Igen, módosíthatod a kódot úgy, hogy az összes oldal helyett csak egy adott oldaltartományon menjen végig.

### Milyen szövegkiemelési módok vannak az Aspose.PDF fájlban?
Az Aspose.PDF két módot kínál: Nyers és Tiszta. A Nyers mód megpróbálja megőrizni az eredeti elrendezést, míg a Tiszta mód csak a szöveget nyeri ki formázás nélkül.

### Az Aspose.PDF for .NET kompatibilis a .NET Core-ral?
Igen, az Aspose.PDF for .NET teljes mértékben kompatibilis a .NET Core-ral és a .NET Frameworkkel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}