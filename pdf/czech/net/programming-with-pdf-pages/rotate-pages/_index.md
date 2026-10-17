---
title: Otočte každou stránku PDF o 180° pomocí Aspose.Pdf pro .NET
weight: 260
limit:
description: Postupný návod, jak otočit všechny stránky PDF o 180 stupňů pomocí Aspose.Pdf pro .NET.
keywords: [rotate pdf pages .net, Aspose.Pdf for .NET, rotate all pages 180 degrees, pdf page rotation, c# pdf manipulation]
url: /net/programming-with-pdf-pages/rotate-pages/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Postupný návod, jak otočit všechny stránky PDF o 180 stupňů pomocí
    Aspose.Pdf pro .NET.
  headline: Otočte každou stránku PDF o 180° pomocí Aspose.Pdf pro .NET
  type: TechArticle
- description: Postupný návod, jak otočit všechny stránky PDF o 180 stupňů pomocí
    Aspose.Pdf pro .NET.
  name: Otočte každou stránku PDF o 180° pomocí Aspose.Pdf pro .NET
  steps:
  - name: Deklarujte cesty ke zdrojovému a cílovému souboru PDF.
    text: Deklarujte cesty ke zdrojovému a cílovému souboru PDF.
  - name: Zkontrolujte, zda zdrojový soubor existuje, a v případě, že ne, ukončete
      program s chybovou zprávou.
    text: Zkontrolujte, zda zdrojový soubor existuje, a v případě, že ne, ukončete
      program s chybovou zprávou.
  - name: Vytvořte objekt Document pro zdrojové PDF uvnitř bloku using, aby se spravovaly
      prostředky.
    text: Vytvořte objekt Document pro zdrojové PDF uvnitř bloku using, aby se spravovaly
      prostředky.
  - name: Procházejte každou stránku v pdfDoc.Pages a nastavte její vlastnost Rotate
      na Rotation.on180, čímž otočíte každou stránku vzhůru nohama.
    text: Procházejte každou stránku v pdfDoc.Pages a nastavte její vlastnost Rotate
      na Rotation.on180, čímž otočíte každou stránku vzhůru nohama.
  - name: Uložte upravený Document do cílového souboru, čímž trvale zachováte otočení.
    text: Uložte upravený Document do cílového souboru, čímž trvale zachováte otočení.
  - name: Vypište potvrzovací zprávu do konzole, která naznačuje, že operace byla
      dokončena.
    text: Vypište potvrzovací zprávu do konzole, která naznačuje, že operace byla
      dokončena.
  type: HowTo
- questions:
  - answer: Kód kontroluje `File.Exists(sourceFile)` a zapíše chybu do `Console.Error`
      před návratem, takže není vyhozena žádná výjimka a program se ukončí elegantně.
    question: Co se stane, pokud zdrojový PDF soubor neexistuje?
  - answer: Ano, nahraďte `Rotation.on180` jinou hodnotou výčtu, například `Rotation.on90`
      (po směru hodinových ručiček) nebo `Rotation.on270` (proti směru hodinových
      ručiček), abyste použili jiné otočení.
    question: Mohu otočit stránky o jiný úhel, např. 90° po směru hodinových ručiček?
  - answer: Kolekce `Pages` v Aspose.Pdf je indexována od jedné, ale iterátor `foreach`
      to abstrahuje a prochází každým objektem `Page` bez ohledu na podkladový index.
    question: Je kolekce stránek indexována od nuly? Jak funguje smyčka `foreach`?
  - answer: Volání `pdfDoc.Save(destinationFile)` přepíše jakýkoli existující soubor
      s tímto názvem, takže použijte jiný název souboru nebo zálohujte originál, pokud
      jej potřebujete zachovat.
    question: Přepíše se původní PDF, pokud použiji stejný název souboru pro `destinationFile`?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/rotate-pages/og-image.png
og_title: Otočte každou stránku PDF o 180°
og_description: Naučte se, jak převrátit všechny stránky PDF vzhůru nohama pomocí několika řádků kódu v C#.
og_image_alt: Průvodce, který ukazuje, jak otočit každou stránku PDF o 180 stupňů pomocí Aspose.Pdf pro .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Otočte každou stránku PDF o 180° pomocí Aspose.Pdf pro .NET
Tento tutoriál ukazuje, jak otočit každou stránku existujícího PDF dokumentu o 180 stupňů pomocí třídy Aspose.Pdf Document. Použitím otočení celé stránky můžete rychle opravit převrácené skeny nebo přenastavit dokumenty, aniž byste je museli znovu vytvářet. Příklad je napsán v C# a funguje na platformě .NET.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/rotate-pages" >}}


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

**Q: Co se stane, pokud zdrojový PDF soubor neexistuje?**  
A: Kód kontroluje `File.Exists(sourceFile)` a zapíše chybu do `Console.Error` před návratem, takže není vyhozena žádná výjimka a program se ukončí elegantně.

**Q: Mohu otočit stránky o jiný úhel, např. 90° po směru hodinových ručiček?**  
A: Ano, nahraďte `Rotation.on180` jinou hodnotou výčtu, například `Rotation.on90` (po směru hodinových ručiček) nebo `Rotation.on270` (proti směru hodinových ručiček), abyste použili jiné otočení.

**Q: Je kolekce stránek indexována od nuly? Jak funguje smyčka `foreach`?**  
A: Kolekce `Pages` v Aspose.Pdf je indexována od jedné, ale iterátor `foreach` to abstrahuje a prochází každým objektem `Page` bez ohledu na podkladový index.

**Q: Přepíše se původní PDF, pokud použiji stejný název souboru pro `destinationFile`?**  
A: Volání `pdfDoc.Save(destinationFile)` přepíše jakýkoli existující soubor s tímto názvem, takže použijte jiný název souboru nebo zálohujte originál, pokud jej potřebujete zachovat.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}