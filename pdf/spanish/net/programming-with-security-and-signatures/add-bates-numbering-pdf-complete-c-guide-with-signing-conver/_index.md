---
category: general
date: 2026-06-21
description: Añade numeración Bates a PDF y aprende cómo agregar números Bates, convertir
  PDF a PDF/X‑4, convertir PDF a PDF/A‑4 y firmar digitalmente PDF con C# en una única
  guía paso a paso.
draft: false
keywords:
- add bates numbering pdf
- how to add bates numbers
- digitally sign pdf c#
- convert pdf to pdf/x-4
- convert pdf to pdfa-4
language: es
og_description: Agregar numeración Bates a PDF, ver cómo agregar números Bates, convertir
  PDF a PDF/X-4, convertir PDF a PDF/A-4 y firmar digitalmente PDF en C# con Aspose.Pdf.
og_title: Agregar numeración Bates a PDF – Tutorial paso a paso en C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add bates numbering pdf and learn how to add bates numbers, convert
    pdf to pdf/x-4, convert pdf to pdfa-4, and digitally sign pdf c# in a single walkthrough.
  headline: Add Bates Numbering PDF – Complete C# Guide with Signing & Conversion
  type: TechArticle
- questions:
  - answer: Yes. Use `BatesNumberingOptions` properties such as `Location` and `FontSize`
      to fine‑tune placement.
    question: Can I change the position of the Bates numbers?
  - answer: Switch `PdfFormat.PDF_X_4` to `PdfFormat.PDFA_4` in the conversion options.
      That satisfies the **convert pdf to pdfa-4** requirement.
    question: What if I need PDF/A‑4 instead of PDF/X‑4?
  - answer: Absolutely. Replace `DigestHashAlgorithm.Sha384` with `DigestHashAlgorithm.Sha256`
      (or any supported algorithm).
    question: My certificate uses a different hash algorithm—can I use SHA‑256?
  - answer: 'Not strictly. In this flow we save after conversion and after Bates numbering
      to give you intermediate files. You could defer saving until the end if you
      prefer a single write operation. ## Wrap‑Up We’ve just demonstrated a practical,
      end‑to‑end solution that **add bates numbering pdf**, explains **'
    question: Do I need to call `document.Save` after each step?
  type: FAQPage
tags:
- Aspose.Pdf
- C#
- PDF processing
- Bates numbering
title: Agregar numeración Bates a PDF – Guía completa de C# con firma y conversión
url: /es/net/programming-with-security-and-signatures/add-bates-numbering-pdf-complete-c-guide-with-signing-conver/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates a PDF – Guía completa en C# con firma y conversión

¿Alguna vez te has preguntado **add bates numbering pdf** sin volverte loco? No eres el único. Los equipos legales, auditores y cualquiera que necesite documentos rastreables preguntan constantemente *cómo añadir números Bates* a un PDF, y además requieren que el archivo cumpla con los estándares PDF/X‑4 o PDF/A‑4 y esté firmado digitalmente.  

En este tutorial recorreremos exactamente eso: usando Aspose.Pdf para .NET **add bates numbering pdf**, mostraremos **cómo añadir números Bates**, **convertir pdf a pdf/x-4**, **convertir pdf a pdfa-4**, y finalmente **firmar digitalmente pdf c#**. Al final tendrás un programa listo‑para‑ejecutar que produce tres PDFs pulidos: una versión PDF/X‑4, una versión con numeración Bates y una versión firmada digitalmente.

![add bates numbering pdf example](image-placeholder.png "Screenshot showing add bates numbering pdf in action")

## Lo que necesitarás

- **.NET 6+** (o .NET Framework 4.6+). Aspose.Pdf admite ambos.
- Una **licencia válida de Aspose.Pdf para .NET** (o puedes trabajar con la evaluación, pero aparecerán marcas de agua).
- Un **archivo de certificado PKCS#7** (`.pfx`) y su contraseña para la firma.
- El **PDF de ejemplo** que deseas transformar (colócalo en una carpeta que controles).
- Visual Studio, Rider o cualquier IDE de C# que prefieras.

Eso es todo—no se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`. Si aún no has añadido la biblioteca, ejecuta:

```bash
dotnet add package Aspose.Pdf
```

Ahora vamos al código.

## Paso 1: Cargar el documento PDF de origen

Primero, necesitamos cargar el archivo original en memoria. Esta es la base para todas las operaciones posteriores.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

// Load the source PDF – adjust the path to your environment
var document = new Document("YOUR_DIRECTORY/sample.pdf");
```

> **Por qué es importante:** Cargar el PDF crea un objeto `Document` que representa todo el archivo, dándonos acceso a las APIs de conversión, campos de formulario y seguridad.

## Paso 2: Convertir PDF a PDF/X‑4 (cumplimiento PDF/A‑4)

Si tu flujo de trabajo requiere calidad de archivo, PDF/X‑4 (un subconjunto de PDF/A‑4) es la opción adecuada. Así es como **convert pdf to pdf/x-4** con Aspose.

```csharp
// Set conversion options – PDF/X‑4 is the target format
var conversionOptions = new PdfFormatConversionOptions(PdfFormat.PDF_X_4, ConvertErrorAction.Delete);

// Perform the conversion
document.Convert(conversionOptions);
```

> **Consejo:** La bandera `ConvertErrorAction.Delete` elimina cualquier contenido que rompería el cumplimiento, garantizando una salida limpia de PDF/X‑4.

## Paso 3: Guardar la versión PDF/X‑4

Ahora que el documento cumple con PDF/X‑4, lo guardamos en disco.

```csharp
document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");
```

Ya tienes un archivo compatible con **convert pdf to pdfa-4** (PDF/X‑4 es miembro de la familia PDF/A‑4). Siéntete libre de abrirlo en Acrobat para verificar la insignia de cumplimiento.

## Paso 4: Añadir numeración Bates – El núcleo de “Add Bates Numbering PDF”

La numeración Bates es un identificador secuencial colocado en cada página. Esta es la respuesta exacta a *cómo añadir números Bates* programáticamente.

```csharp
// Configure Bates numbering options
var batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",   // Optional prefix
    Start = 5000        // Starting number
};

// Apply Bates numbering to the document
document.AddBatesNumbering(batesOptions);
```

> **Por qué funciona:** `AddBatesNumbering` recorre cada página y estampa el número en la ubicación predeterminada (abajo‑derecha). Puedes ajustar la posición más adelante mediante `BatesNumberingOptions` si lo deseas.

## Paso 5: Guardar el PDF con numeración Bates

Después de **add bates numbering pdf**, necesitamos un archivo separado que preserve los números.

```csharp
document.Save("YOUR_DIRECTORY/sample_bates.pdf");
```

Abre el archivo; deberías ver “CASE‑5000”, “CASE‑5001”, etc., en la parte inferior de cada página.

## Paso 6: Firmar digitalmente el PDF – “Digitally Sign PDF C#” en acción

Una firma digital garantiza autenticidad e integridad. A continuación **digitally sign pdf c#** usando un hash SHA‑384.

```csharp
// Prepare the signature handler
var signature = new PdfFileSignature(document);

// Load the PKCS#7 certificate (adjust password)
var pkcs7 = new PKCS7Detached(
    "YOUR_DIRECTORY/mycert.pfx", // Path to .pfx
    "pwd",                       // Certificate password
    DigestHashAlgorithm.Sha384   // Strong hashing algorithm
);

// Sign page 1, place signature rectangle at (100,100)-(200,150)
signature.Sign(
    pageNumber: 1,
    signatureAppearance: true,
    rectangle: new Rectangle(100, 100, 200, 150),
    pkcs7: pkcs7
);
```

> **Pro tip:** El `Rectangle` define dónde aparece la firma visible. Si no necesitas una pista visual, establece `signatureAppearance` en `false`.

## Paso 7: Guardar el PDF firmado digitalmente

Finalmente, escribe el documento firmado en disco.

```csharp
signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
```

Ahora tienes un archivo **digitally sign pdf c#** que puede validarse en cualquier lector PDF que admita firmas digitales.

## Código fuente completo – Solución todo‑en‑uno

A continuación el programa completo, listo‑para‑ejecutar, que une todo. Copia‑pega, ajusta las rutas y pulsa **F5**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Security;
using Aspose.Pdf.Saving;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source PDF document
        // -------------------------------------------------
        var document = new Document("YOUR_DIRECTORY/sample.pdf");

        // -------------------------------------------------
        // Step 2: Convert the document to PDF/X‑4 format
        // (PDF/A‑4 compliance)
        // -------------------------------------------------
        var conversionOptions = new PdfFormatConversionOptions(
            PdfFormat.PDF_X_4,
            ConvertErrorAction.Delete);
        document.Convert(conversionOptions);

        // -------------------------------------------------
        // Step 3: Save the PDF/X‑4 version
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_pdfx4.pdf");

        // -------------------------------------------------
        // Step 4: Add Bates numbering – how to add bates numbers
        // -------------------------------------------------
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 5000
        };
        document.AddBatesNumbering(batesOptions);

        // -------------------------------------------------
        // Step 5: Save the Bates‑numbered PDF
        // -------------------------------------------------
        document.Save("YOUR_DIRECTORY/sample_bates.pdf");

        // -------------------------------------------------
        // Step 6: Sign the document using SHA‑384 hashing
        // -------------------------------------------------
        var signature = new PdfFileSignature(document);
        var pkcs7 = new PKCS7Detached(
            "YOUR_DIRECTORY/mycert.pfx",
            "pwd",
            DigestHashAlgorithm.Sha384);
        signature.Sign(
            pageNumber: 1,
            signatureAppearance: true,
            rectangle: new Rectangle(100, 100, 200, 150),
            pkcs7: pkcs7);

        // -------------------------------------------------
        // Step 7: Save the digitally signed PDF
        // -------------------------------------------------
        signature.Save("YOUR_DIRECTORY/sample_signed.pdf");
    }
}
```

### Resultado esperado

| Archivo | Propósito | Característica clave |
|---------|-----------|----------------------|
| `sample_pdfx4.pdf` | Versión PDF/X‑4 | Cumple con la conformidad PDF/A‑4 |
| `sample_bates.pdf` | PDF con numeración Bates | **add bates numbering pdf** aplicado |
| `sample_signed.pdf` | PDF firmado digitalmente | **digitally sign pdf c#** con SHA‑384 |

Abre cualquiera de los tres archivos en Adobe Acrobat Reader; verás los números Bates en el segundo archivo y un campo de firma en el tercero.

## Preguntas frecuentes (FAQ)

**P: ¿Puedo cambiar la posición de los números Bates?**  
R: Sí. Usa las propiedades de `BatesNumberingOptions` como `Location` y `FontSize` para afinar la colocación.

**P: ¿Qué pasa si necesito PDF/A‑4 en lugar de PDF/X‑4?**  
R: Cambia `PdfFormat.PDF_X_4` a `PdfFormat.PDFA_4` en las opciones de conversión. Eso satisface el requisito **convert pdf to pdfa-4**.

**P: Mi certificado usa un algoritmo de hash diferente—¿puedo usar SHA‑256?**  
R: Por supuesto. Reemplaza `DigestHashAlgorithm.Sha384` por `DigestHashAlgorithm.Sha256` (o cualquier algoritmo soportado).

**P: ¿Necesito llamar a `document.Save` después de cada paso?**  
R: No estrictamente. En este flujo guardamos después de la conversión y después de la numeración Bates para ofrecerte archivos intermedios. Podrías posponer el guardado hasta el final si prefieres una única operación de escritura.

## Conclusión

Acabamos de demostrar una solución práctica, de extremo a extremo, que **add bates numbering pdf**, explica **cómo añadir números Bates**, muestra **convert pdf to pdf/x-4**, y cubre

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/german/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/french/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)
- [Aspose Pdf Net Add Attachments Convert Pdfa](/pdf/japanese/net/pdfa-compliance/aspose-pdf-net-add-attachments-convert-pdfa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}