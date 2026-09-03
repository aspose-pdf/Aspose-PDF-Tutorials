---
category: general
date: 2026-02-14
description: Adjon hozzá Bates-számozást PDF-hez dokumentumaihoz könnyedén. Tanulja
  meg, hogyan lehet lábléc oldalszámokat és sorozatszámokat hozzáadni PDF-hez az Aspose.Pdf
  segítségével percek alatt.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: hu
og_description: Adjon hozzá Bates-számozást a PDF-hez gyorsan. Ez az útmutató bemutatja,
  hogyan lehet lábléc oldalszámokat és sorozatszámokat hozzáadni a PDF-hez az Aspose.Pdf
  használatával, teljes kóddal és tippekkel.
og_title: Bates-számozás hozzáadása PDF-hez – Lépésről lépésre C# útmutató
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Bates-számozás hozzáadása PDF-hez – Teljes C# útmutató
url: /hu/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bates-számozás PDF-hez – Teljes C# útmutató

Valaha szükséged volt **add Bates numbering PDF** fájlok hozzáadására, de nem tudtad, hol kezdj? Nem vagy egyedül. Jogcsapatok, auditorok és mindenki, aki nagy dokumentumkészletekkel dolgozik, folyamatosan kérdezi: „Hogyan adhatok hozzá Bates-számokat anélkül, hogy tönkretenném az elrendezést?” A jó hír, hogy az Aspose.Pdf for .NET segítségével ezeket a számokat egyszerű láblécként illesztheted be – manuális szerkesztés nélkül.

Ebben az útmutatóban egy gyakorlati, vég‑től‑végig megoldáson vezetünk végig, amely nem csak **adds footer page numbers**-t ad hozzá, hanem lehetővé teszi **add sequential numbers PDF** fájlok hozzáadását egy egyedi előtaggal, betűmérettel és igazítással. A végére egy azonnal futtatható C# programmal, a beállítások jelentőségének világos megértésével és néhány profi tippel fogsz rendelkezni, hogy elkerüld a leggyakoribb buktatókat.

## Amit megtanulhatsz

- Hogyan töltsünk be egy meglévő PDF-et, és készítsük elő Bates-számozáshoz.  
- Mely **BatesNumberingOptions** tulajdonságok szabályozzák a megjelenést és elhelyezést.  
- Hogyan alkalmazzuk a számozást minden oldalra egy hívással.  
- Módszerek az előtag, kezdő szám és margók testreszabására különböző jogi formátumokhoz.  
- Régió‑eset kezelése – mit tegyünk titkosított PDF-ekkel vagy olyan dokumentumokkal, amelyek már tartalmaznak láblécet.

**Prerequisites**: .NET 6+ (vagy .NET Framework 4.7+), egy friss Aspose.Pdf verzió (a példában a 23.10 van használva), és egy bemeneti PDF, amelynek módosításához jogod van. Más harmadik‑fél könyvtárra nincs szükség.

---

## 1. lépés – Töltsd be a számozandó PDF-et

Az első dolog, amit teszünk, egy `Document` példány létrehozása, amely a forrásfájlra mutat. A `using var` minta használata biztosítja, hogy a fájlkezelő automatikusan felszabaduljon.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Why this matters:** Az Aspose.Pdf beolvassa a teljes PDF struktúrát a memóriába, lehetővé téve, hogy oldalakat, annotációkat és metaadatokat manipuláljunk anélkül, hogy az eredeti fájlt a lemezen érintenénk. Ha a PDF jelszóval védett, a jelszót átadhatod a konstruktorba – lásd a „Encrypted PDFs” megjegyzést a végén.

## 2. lépés – Határozd meg a Bates-számozási beállításokat

A Bates-számok lényegében oldal láblécek, amelyek konfigurálható előtaggal és sorozatszámlálóval rendelkeznek. A `BatesNumberingOptions` osztály lehetővé teszi minden vizuális aspektus finomhangolását.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Gyors tipp

- **Prefix**: Használj egy rövid, egyedi azonosítót (pl. ügyszám), hogy a lábléc olvasható maradjon.  
- **StartNumber**: Jogirodák gyakran a `1`‑től vagy egy egyedi eltolástól kezdik; válaszd azt, ami a nyilvántartási rendszeredhez illeszkedik.  
- **Margins**: A `20` pont alsó margó biztosítja, hogy a szöveg ne érjen a lábjegyzetekhez vagy aláírásokhoz, amelyek már az oldal szélén lehetnek.

## 3. lépés – Alkalmazd a számozást az összes oldalra

A beállítások konfigurálása után a tényleges beillesztés egyetlen soros kóddal megoldható. Az Aspose.Pdf kezeli az oldalszámozást, frissíti a meglévő tartalomszámokat, és automatikusan figyelembe veszi az oldal forgását.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **What’s happening under the hood?** A könyvtár végigiterál minden `Page` objektumon, létrehoz egy `TextFragment`‑et, amely tartalmazza az előtagot és az aktuális számlálót, majd a oldal koordináta‑rendszerét használva rajzolja ki. Mivel a `HorizontalAlignment.Right` és a `VerticalAlignment.Bottom` értékeket állítottuk be, a szöveg az oldal jobb‑alsó sarkába helyezkedik el, függetlenül az oldal méretétől.

## 4. lépés – Mentsd el a módosított PDF-et

Végül írd az eredményt egy új fájlba. Az eredeti felülírása lehetséges, de egy másolat megtartása segít a verziókezelésben.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Ha meg kell őrizned az eredeti metaadatokat (szerző, létrehozás dátuma), az Aspose.Pdf alapértelmezés szerint másolja azokat. Emellett megadhatsz egy `SaveOptions` objektumot PDF/A kompatibilitáshoz vagy tömörítéshez.

## Teljes működő példa

Az alábbiakban a teljes, azonnal futtatható program található. Illeszd be egy konzolos alkalmazás projektbe, állítsd be a fájlutakat, és nyomd meg a **F5**‑öt.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Expected result:** A `output.pdf` minden oldala most egy `ABC-1000`, `ABC-1001`, … formátumú láblécet jelenít meg, amely a jobb‑alsó sarokba van rögzítve. Nyisd meg a fájlt bármely PDF-olvasóval a ellenőrzéshez.

## Gyakori változatok kezelése

### Csak lábléc oldalszámok hozzáadása

Ha csak egyszerű oldalszámokra van szükséged előtag nélkül, állítsd be a `Prefix = ""` értéket, és esetleg módosítsd a margót, hogy elkerüld az ütközést a meglévő láblécekkel.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Másik igazítás használata

Jogos dokumentumok esetén előfordulhat, hogy a számot középre kell helyezni az alján. Váltsd meg az igazítást:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Titkosított PDF-ek kezelése

Ha a forrás PDF jelszóval védett, add meg a jelszót a következő módon:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

A munkafolyamat többi része változatlan marad.

### Létező láblécek kihagyása

Ha egy dokumentum már tartalmaz láblécet, amelyet nem akarsz felülírni, előtoldalhatod egy egyedi karakterlánccal, amely megkülönbözteti az új számot, vagy manuálisan iterálhatsz az oldalakon, és csak ott adsz hozzá egy `TextFragment`‑et, ahol a lábléc hiányzik. A könyvtár `Page` osztálya elérhetővé teszi a `Annotations` és `Contents` gyűjteményeket a finomhangolt vezérléshez.

## Profi tippek és buktatók

- **Avoid clipping**: Nagyon kis alsó margók esetén a szöveg levágódhat a nyomtatón. Teszteld fizikai nyomtatással, ha nyomtatott példányt terjesztesz.  
- **Performance**: Bates-számok hozzáadása egy 500 oldalas PDF-hez kevesebb, mint egy másodperc egy modern laptopon, de nagy kötegek esetén előnyös a párhuzamos feldolgozás – csak ne feledd, hogy a `Document` nem szálbiztos, ezért minden szálnak saját példányra van szüksége.  
- **Version compatibility**: A kód az Aspose.Pdf 23.10 és újabb verziókkal működik. Régebbi verzió esetén a tulajdonságnevek ugyanazok, de a `MarginInfo` konstruktor `float` argumentumokat igényelhet.  
- **Legal compliance**: Egyes joghatóságok megkövetelik, hogy a Bates-szám egy meghatározott helyen legyen elhelyezve (pl. bal‑alsó). Ennek megfelelően állítsd be a `HorizontalAlignment`‑t.

## Összegzés

Most bemutattuk, hogyan **add Bates numbering PDF** fájlokhoz használhatod az Aspose.Pdf for .NET-et, lefedve mindent a dokumentum betöltésétől a tiszta lábléccel ellátott végső verzió mentéséig. Néhány tulajdonság finomhangolásával képes vagy **add footer page numbers**, **add sequential numbers PDF** funkciókat is megvalósítani, vagy a megjelenést testre szabni bármely jogi szabványnak megfelelően.

Készen állsz a következő lépésre? Próbáld meg kombinálni ezt a technikát OCR szövegkivonással, hogy kereshető kulcsszavakat ágyazz a Bates-számok mellé, vagy automatizáld a folyamatot teljes mappákra a `Directory.GetFiles` használatával. A lehetőségek végtelenek, és az alap, amelyet most szereztél, könnyűvé teszi ezeket a bővítéseket.

Boldog kódolást, és legyenek a PDF-jeid mindig tökéletesen számozva!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}