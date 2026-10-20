---
title: PDF mit Keine‑Druck‑Berechtigung verschlüsseln mit Aspose.PDF für .NET
weight: 101
limit:
description: Erfahren Sie, wie Sie ein PDF mit AES‑256 verschlüsseln und das Drucken mit Aspose.PDF für .NET deaktivieren.
keywords: [Aspose.PDF for .NET, pdf encryption aes-256, disable pdf printing, pdf password protection, no print permission pdf]
url: /net/security-permissions/encrypt-pdf-no-print/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Erfahren Sie, wie Sie ein PDF mit AES‑256 verschlüsseln und das Drucken
    mit Aspose.PDF für .NET deaktivieren.
  headline: PDF mit Keine‑Druck‑Berechtigung verschlüsseln mit Aspose.PDF für .NET
  type: TechArticle
- description: Erfahren Sie, wie Sie ein PDF mit AES‑256 verschlüsseln und das Drucken
    mit Aspose.PDF für .NET deaktivieren.
  name: PDF mit Keine‑Druck‑Berechtigung verschlüsseln mit Aspose.PDF für .NET
  steps:
  - name: Definieren Sie den Pfad zur Quell‑PDF, den Namen der geschützten Ausgabedatei
      sowie die Viewer‑ und Owner‑Passwörter.
    text: Definieren Sie den Pfad zur Quell‑PDF, den Namen der geschützten Ausgabedatei
      sowie die Viewer‑ und Owner‑Passwörter.
  - name: Prüfen Sie, ob die Quelldatei existiert, und brechen Sie mit einer Fehlermeldung
      ab, falls sie fehlt.
    text: Prüfen Sie, ob die Quelldatei existiert, und brechen Sie mit einer Fehlermeldung
      ab, falls sie fehlt.
  - name: Öffnen Sie das ursprüngliche PDF, setzen Sie keine Berechtigungen, verschlüsseln
      Sie es mit AES‑256 unter Verwendung der angegebenen Passwörter und speichern
      Sie die geschützte Datei.
    text: Öffnen Sie das ursprüngliche PDF, setzen Sie keine Berechtigungen, verschlüsseln
      Sie es mit AES‑256 unter Verwendung der angegebenen Passwörter und speichern
      Sie die geschützte Datei.
  - name: Öffnen Sie das verschlüsselte PDF erneut mit dem Viewer‑Passwort und geben
      Sie das IsEncrypted‑Flag in der Konsole aus, um den Schutz zu bestätigen.
    text: Öffnen Sie das verschlüsselte PDF erneut mit dem Viewer‑Passwort und geben
      Sie das IsEncrypted‑Flag in der Konsole aus, um den Schutz zu bestätigen.
  - name: Geben Sie eine abschließende Meldung aus, die anzeigt, dass die Verschlüsselung
      abgeschlossen ist und den Namen der Ausgabedatei.
    text: Geben Sie eine abschließende Meldung aus, die anzeigt, dass die Verschlüsselung
      abgeschlossen ist und den Namen der Ausgabedatei.
  type: HowTo
- questions:
  - answer: '`Permissions` ist ein Flag‑Enum; die Zuweisung von `0` bedeutet, dass
      keine Berechtigungsbits gesetzt sind, sodass Aspose.Pdf das PrintDocument‑Recht
      nicht gewährt und der Viewer das PDF nicht drucken kann.'
    question: Warum deaktiviert das Setzen von `Permissions rights = 0;` das Drucken?
  - answer: Ja, ersetzen Sie `CryptoAlgorithm.AESx256` durch `CryptoAlgorithm.AESx128`
      (oder einen anderen unterstützten Enum‑Wert) im Aufruf `pdfDoc.Encrypt`; der
      Rest des Codes bleibt unverändert.
    question: Kann ich mit demselben Code einen anderen Verschlüsselungsalgorithmus,
      z. B. AES‑128, verwenden?
  - answer: Aspose.Pdf akzeptiert identische Passwörter, aber das Owner‑Passwort bietet
      dann keine zusätzlichen Rechte mehr; das PDF wird weiterhin verschlüsselt, und
      die von Ihnen angegebenen Berechtigungen (keine) gelten.
    question: Was passiert, wenn das Viewer‑Passwort und das Master‑(Owner‑)Passwort
      identisch sind?
  - answer: Öffnen Sie die geschützte Datei mit dem Viewer‑Passwort (`new Document(securedFile,
      viewerPwd)`) und versuchen Sie, aus einem PDF‑Viewer zu drucken; da keine `PrintDocument`‑Berechtigung
      gesetzt wurde, wird der Viewer den Druckbefehl ablehnen.
    question: Wie kann ich bestätigen, dass das Drucken nach der Verschlüsselung tatsächlich
      blockiert ist?
  - answer: Der Code prüft `File.Exists(sourceFile)` und schreibt einen Fehler in
      `Console.Error`, bevor er zurückkehrt, wodurch verhindert wird, dass der `Document`‑Konstruktor
      eine `FileNotFoundException` wirft.
    question: Welcher Fehler wird ausgelöst, wenn `original.pdf` nicht existiert,
      und wie sollte man damit umgehen?
  type: FAQPage
images:
- /net/security-permissions/encrypt-pdf-no-print/og-image.png
og_title: PDF verschlüsseln und Drucken blockieren
og_description: Sichern Sie Ihr PDF mit AES‑256‑Verschlüsselung und stellen Sie sicher, dass es nicht gedruckt werden kann – Schritt‑für‑Schritt‑Anleitung.
og_image_alt: Screenshot, der den Aspose.PDF für .NET‑Code zeigt, der ein PDF verschlüsselt und das Drucken deaktiviert.
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF mit Keine‑Druck‑Berechtigung verschlüsseln mit Aspose.PDF für .NET
Dieses Tutorial zeigt, wie man ein vorhandenes PDF mit Aspose.PDF für .NET öffnet, AES‑256‑Verschlüsselung anwendet, dabei keine Berechtigungen gewährt – wodurch das Drucken effektiv deaktiviert wird – das gesicherte Dokument speichert und den Schutz bestätigt, indem man es mit dem Viewer‑Passwort öffnet. Folgen Sie dem Schritt‑für‑Schritt‑Code, um sicherzustellen, dass Ihr PDF nach der Verschlüsselung nicht gedruckt werden kann.

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

**Q: Warum deaktiviert das Setzen von `Permissions rights = 0;` das Drucken?**  
A: `Permissions` ist ein Flag‑Enum; die Zuweisung von `0` bedeutet, dass keine Berechtigungsbits gesetzt sind, sodass Aspose.Pdf das PrintDocument‑Recht nicht gewährt und der Viewer das PDF nicht drucken kann.

**Q: Kann ich mit demselben Code einen anderen Verschlüsselungsalgorithmus, z. B. AES‑128, verwenden?**  
A: Ja, ersetzen Sie `CryptoAlgorithm.AESx256` durch `CryptoAlgorithm.AESx128` (oder einen anderen unterstützten Enum‑Wert) im Aufruf `pdfDoc.Encrypt`; der Rest des Codes bleibt unverändert.

**Q: Was passiert, wenn das Viewer‑Passwort und das Master‑(Owner‑)Passwort identisch sind?**  
A: Aspose.Pdf akzeptiert identische Passwörter, aber das Owner‑Passwort bietet dann keine zusätzlichen Rechte mehr; das PDF wird weiterhin verschlüsselt, und die von Ihnen angegebenen Berechtigungen (keine) gelten.

**Q: Wie kann ich bestätigen, dass das Drucken nach der Verschlüsselung tatsächlich blockiert ist?**  
A: Öffnen Sie die geschützte Datei mit dem Viewer‑Passwort (`new Document(securedFile, viewerPwd)`) und versuchen Sie, aus einem PDF‑Viewer zu drucken; da keine `PrintDocument`‑Berechtigung gesetzt wurde, wird der Viewer den Druckbefehl ablehnen.

**Q: Welcher Fehler wird ausgelöst, wenn `original.pdf` nicht existiert, und wie sollte man damit umgehen?**  
A: Der Code prüft `File.Exists(sourceFile)` und schreibt einen Fehler in `Console.Error`, bevor er zurückkehrt, wodurch verhindert wird, dass der `Document`‑Konstruktor eine `FileNotFoundException` wirft.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}