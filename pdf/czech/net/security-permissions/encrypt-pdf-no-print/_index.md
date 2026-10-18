---
title: Zašifrujte PDF bez oprávnění k tisku pomocí Aspose.PDF pro .NET
weight: 101
limit:
description: Naučte se, jak zašifrovat PDF pomocí AES‑256 a zakázat tisk pomocí Aspose.PDF pro .NET.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Naučte se, jak zašifrovat PDF pomocí AES‑256 a zakázat tisk pomocí
    Aspose.PDF pro .NET.
  headline: Zašifrujte PDF bez oprávnění k tisku pomocí Aspose.PDF pro .NET
  type: TechArticle
- description: Naučte se, jak zašifrovat PDF pomocí AES‑256 a zakázat tisk pomocí
    Aspose.PDF pro .NET.
  name: Zašifrujte PDF bez oprávnění k tisku pomocí Aspose.PDF pro .NET
  steps:
  - name: Definujte cestu ke zdrojovému PDF, název výstupního chráněného souboru a
      hesla pro prohlížeč i vlastníka.
    text: Definujte cestu ke zdrojovému PDF, název výstupního chráněného souboru a
      hesla pro prohlížeč i vlastníka.
  - name: Zkontrolujte, zda zdrojový soubor existuje, a v případě, že chybí, ukončete
      s chybovou zprávou.
    text: Zkontrolujte, zda zdrojový soubor existuje, a v případě, že chybí, ukončete
      s chybovou zprávou.
  - name: Otevřete původní PDF, nastavte žádná oprávnění, zašifrujte jej pomocí AES‑256
      s uvedenými hesly a uložte chráněný soubor.
    text: Otevřete původní PDF, nastavte žádná oprávnění, zašifrujte jej pomocí AES‑256
      s uvedenými hesly a uložte chráněný soubor.
  - name: Znovu otevřete zašifrované PDF pomocí hesla pro prohlížeč a vypište jeho
      příznak IsEncrypted do konzole pro potvrzení ochrany.
    text: Znovu otevřete zašifrované PDF pomocí hesla pro prohlížeč a vypište jeho
      příznak IsEncrypted do konzole pro potvrzení ochrany.
  - name: Vytiskněte závěrečnou zprávu, která uvádí, že šifrování je dokončeno, a
      název výstupního souboru.
    text: Vytiskněte závěrečnou zprávu, která uvádí, že šifrování je dokončeno, a
      název výstupního souboru.
  type: HowTo
- questions:
  - answer: '`Permissions` je výčtový typ s příznaky; přiřazením hodnoty `0` nejsou
      nastaveny žádné bity oprávnění, takže Aspose.Pdf nepřidělí právo PrintDocument
      a prohlížeč PDF nemůže dokument vytisknout.'
    question: Proč nastavení `Permissions rights = 0;` zakáže tisk?
  - answer: Ano, v volání `pdfDoc.Encrypt` nahraďte `CryptoAlgorithm.AESx256` za `CryptoAlgorithm.AESx128`
      (nebo jinou podporovanou hodnotu výčtu); zbytek kódu zůstane beze změny.
    question: Mohu použít jiný šifrovací algoritmus, například AES‑128, se stejným
      kódem?
  - answer: Aspose.Pdf přijme identická hesla, ale vlastnické heslo již neposkytne
      žádná další oprávnění; PDF bude i nadále zašifrováno a použijí se zadaná oprávnění
      (žádná).
    question: Co se stane, pokud jsou heslo pro prohlížeč a hlavní (vlastnické) heslo
      stejné?
  - answer: Otevřete chráněný soubor pomocí hesla pro prohlížeč (`new Document(securedFile,
      viewerPwd)`) a pokuste se jej vytisknout v PDF prohlížeči; protože nebylo nastaveno
      žádné oprávnění `PrintDocument`, prohlížeč tiskový příkaz odmítne.
    question: Jak mohu potvrdit, že tisk je po šifrování skutečně zablokován?
  - answer: Kód kontroluje `File.Exists(sourceFile)` a před návratem zapíše chybu
      do `Console.Error`, čímž zabraňuje vyhození `FileNotFoundException` konstruktoru
      `Document`.
    question: Jaká chyba se vyhodí, pokud `original.pdf` neexistuje, a jak by se měla
      ošetřit?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: Zašifrujte PDF a zablokujte tisk
og_description: Zabezpečte své PDF šifrováním AES‑256 a ujistěte se, že jej nelze vytisknout – průvodce krok za krokem.
og_image_alt: Snímek obrazovky ukazující kód Aspose.PDF pro .NET, který šifruje PDF a zakazuje tisk.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zašifrujte PDF bez oprávnění k tisku pomocí Aspose.PDF pro .NET
Tento tutoriál ukazuje, jak otevřít existující PDF pomocí Aspose.PDF pro .NET, použít šifrování AES‑256 a nepřidělit žádná oprávnění – čímž se prakticky zakáže tisk – uložit zabezpečený dokument a potvrdit ochranu jeho otevřením pomocí hesla pro prohlížeč. Postupujte podle krok‑za‑krokem kódu, aby vaše PDF po šifrování nebylo možné vytisknout.

---

{{< tutorial-widget sourcePath="pdf/net/security-permissions/encrypt-pdf-no-print" >}}


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

**Q: Proč nastavení `Permissions rights = 0;` zakáže tisk?**  
A: `Permissions` je výčtový typ s příznaky; přiřazením hodnoty `0` nejsou nastaveny žádné bity oprávnění, takže Aspose.Pdf nepřidělí právo PrintDocument a prohlížeč PDF nemůže dokument vytisknout.

**Q: Mohu použít jiný šifrovací algoritmus, například AES‑128, se stejným kódem?**  
A: Ano, v volání `pdfDoc.Encrypt` nahraďte `CryptoAlgorithm.AESx256` za `CryptoAlgorithm.AESx128` (nebo jinou podporovanou hodnotu výčtu); zbytek kódu zůstane beze změny.

**Q: Co se stane, pokud jsou heslo pro prohlížeč a hlavní (vlastnické) heslo stejné?**  
A: Aspose.Pdf přijme identická hesla, ale vlastnické heslo již neposkytne žádná další oprávnění; PDF bude i nadále zašifrováno a použijí se zadaná oprávnění (žádná).

**Q: Jak mohu potvrdit, že tisk je po šifrování skutečně zablokován?**  
A: Otevřete chráněný soubor pomocí hesla pro prohlížeč (`new Document(securedFile, viewerPwd)`) a pokuste se jej vytisknout v PDF prohlížeči; protože nebylo nastaveno žádné oprávnění `PrintDocument`, prohlížeč tiskový příkaz odmítne.

**Q: Jaká chyba se vyhodí, pokud `original.pdf` neexistuje, a jak by se měla ošetřit?**  
A: Kód kontroluje `File.Exists(sourceFile)` a před návratem zapíše chybu do `Console.Error`, čímž zabraňuje vyhození `FileNotFoundException` konstruktoru `Document`.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}