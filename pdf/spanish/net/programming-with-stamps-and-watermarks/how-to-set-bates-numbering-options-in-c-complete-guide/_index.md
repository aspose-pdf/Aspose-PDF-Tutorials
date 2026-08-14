---
category: general
date: 2026-08-14
description: Cómo configurar las opciones de numeración Bates en C# usando GroupDocs.
  Sigue este tutorial paso a paso para agregar prefijos personalizados y números de
  inicio al convertir Word a PDF.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set bates numbering options
- Bates numbering C#
- GroupDocs API
- document conversion C#
- AddBatesNumbering method
- C# PDF generation
language: es
lastmod: 2026-08-14
og_description: Cómo configurar rápidamente las opciones de numeración Bates en C#.
  Esta guía le muestra cómo agregar prefijos personalizados y números iniciales al
  convertir Word a PDF.
og_image_alt: Screenshot of C# code applying Bates numbering to a PDF
og_title: Cómo configurar las opciones de numeración Bates en C# – tutorial paso a
  paso
schemas:
- author: GroupDocs
  dateModified: '2026-08-14'
  description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  headline: How to set bates numbering options in C# – complete guide
  type: TechArticle
- description: How to set bates numbering options in C# using GroupDocs. Follow this
    step‑by‑step tutorial to add custom prefixes and start numbers when converting
    Word to PDF.
  name: How to set bates numbering options in C# – complete guide
  steps:
  - name: '`Document` – loads the source file.'
    text: '`Document` – loads the source file.'
  - name: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
    text: '`BatesNumberingOptions` – holds the start number, prefix, and other formatting
      details.'
  - name: '`AddBatesNumbering` – the method that injects the numbering into each page.'
    text: '`AddBatesNumbering` – the method that injects the numbering into each page.'
  type: HowTo
tags:
- Bates numbering
- C#
- .NET
- GroupDocs
- PDF conversion
title: Cómo configurar las opciones de numeración Bates en C# – guía completa
url: /es/net/programming-with-stamps-and-watermarks/how-to-set-bates-numbering-options-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer opciones de numeración Bates en C# – guía completa

Si necesitas **cómo establecer opciones de numeración Bates** en C#, esta guía te lleva paso a paso. Aprenderás a configurar el número inicial, añadir un prefijo y aplicar la numeración mientras conviertes un documento Word a PDF usando la API de GroupDocs.

El procesamiento de documentos a menudo requiere identificadores únicos en cada página para fines legales o de archivo. Al final de este tutorial tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET, ya sea que estés construyendo una herramienta de soporte de litigios o un generador de informes automatizado. No se necesitan herramientas externas, solo la biblioteca GroupDocs.Conversion y unas pocas líneas de C#.

## Lo que necesitarás

* SDK de .NET 6.0 o posterior instalado  
* Visual Studio 2022 (o cualquier IDE que soporte .NET)  
* Una licencia válida de GroupDocs.Conversion (la prueba gratuita funciona para pruebas)  
* Un documento Word de ejemplo (`input.docx`) que deseas numerar  

Estos requisitos previos garantizan que el código se ejecute sin configuración adicional.

## Cómo establecer opciones de numeración Bates – visión general

El núcleo de **cómo establecer opciones de numeración Bates** se basa en tres objetos:

1. `Document` – carga el archivo fuente.  
2. `BatesNumberingOptions` – contiene el número inicial, el prefijo y otros detalles de formato.  
3. `AddBatesNumbering` – el método que inserta la numeración en cada página.  

Entender por qué existe cada componente te ayuda a adaptar la solución a escenarios más complejos, como fuentes personalizadas o numeración multilingüe.

## Paso 1: Instalar el paquete NuGet GroupDocs.Conversion

Abre una terminal en la carpeta de tu solución y ejecuta:

```bash
dotnet add package GroupDocs.Conversion
```

## Paso 2: Cargar el documento fuente

```csharp
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;

// Step 2: Load the source Word document
Document document = new Document(@"C:\Docs\input.docx");
```

*¿Por qué este paso?*  
Cargar el archivo crea una representación en memoria que el motor de conversión puede manipular. Sin una instancia de `Document` no puedes aplicar la numeración Bates ni ninguna otra transformación.

## Paso 3: Crear las opciones de numeración Bates

```csharp
// Step 3: Configure Bates numbering
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // The first page will be numbered 1000
    StartNumber = 1000,
    // Each page will be prefixed with "CASE-"
    Prefix = "CASE-",
    // Optional: set the number format (e.g., 4 digits)
    NumberFormat = "#0000",
    // Optional: choose where the number appears (header/footer)
    Position = BatesNumberingPosition.FooterRight
};
```

*¿Por qué este paso?*  
`BatesNumberingOptions` encapsula todas las configuraciones que podrías necesitar al **establecer opciones de numeración Bates**. Ajustar `StartNumber` y `Prefix` te permite alinear la salida con tu sistema de gestión de casos. La propiedad `Position` controla la ubicación visual, lo cual a menudo es un requisito de cumplimiento.

## Paso 4: Aplicar la numeración Bates al documento

```csharp
// Step 4: Apply the numbering to every page
document.AddBatesNumbering(batesOptions);
```

El método `AddBatesNumbering` recorre cada página del `Document` cargado e inserta la cadena configurada. Como el método funciona sobre la representación en memoria, puedes encadenar pasos de procesamiento adicionales (p. ej., marcas de agua) antes de guardar.

## Paso 5: Convertir y guardar el resultado como PDF

```csharp
// Step 5: Define PDF conversion options (optional)
PdfConvertOptions pdfOptions = new PdfConvertOptions
{
    // Preserve original layout
    EmbedStandardFonts = true
};

// Save the numbered document as PDF
document.Save(@"C:\Docs\output.pdf", pdfOptions);
```

*¿Por qué este paso?*  
Guardar como PDF es un formato final común para documentos legales. El objeto `PdfConvertOptions` te permite afinar la salida, pero no es necesario para la numeración básica. La llamada `Save` escribe el PDF completamente numerado en el disco.

## Ejemplo completo y ejecutable

Poniendo todo junto, aquí tienes una aplicación de consola autosuficiente que puedes compilar y ejecutar:

```csharp
using System;
using GroupDocs.Conversion;
using GroupDocs.Conversion.Options.Convert;
using GroupDocs.Conversion.Options.Convert.Pdf;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the source Word document
            Document document = new Document(@"C:\Docs\input.docx");

            // Configure Bates numbering options
            BatesNumberingOptions batesOptions = new BatesNumberingOptions
            {
                StartNumber = 1000,
                Prefix = "CASE-",
                NumberFormat = "#0000",
                Position = BatesNumberingPosition.FooterRight
            };

            // Apply numbering to each page
            document.AddBatesNumbering(batesOptions);

            // Optional: set PDF conversion preferences
            PdfConvertOptions pdfOptions = new PdfConvertOptions
            {
                EmbedStandardFonts = true
            };

            // Save the numbered PDF
            document.Save(@"C:\Docs\output.pdf", pdfOptions);

            Console.WriteLine("Bates numbering applied successfully. Output saved to output.pdf");
        }
    }
}
```

**Salida esperada**  
Ejecutar el programa crea `output.pdf` donde cada página muestra una etiqueta como `CASE-1000`, `CASE-1001`, etc., posicionada en el pie de página derecho. Abre el PDF en cualquier visor para verificar que los números aparecen como se pretende.

## Problemas comunes y buenas prácticas

| Problema | Por qué ocurre | Cómo evitarlo |
|----------|----------------|----------------|
| **Rutas relativas causan `FileNotFoundException`** | El directorio de trabajo de una aplicación de consola puede diferir del de Visual Studio. | Utiliza rutas absolutas o `Path.Combine(AppContext.BaseDirectory, "input.docx")`. |
| **La numeración se superpone a los pies de página existentes** | Si el documento fuente ya tiene contenido en el área de pie de página elegida, el nuevo número puede quedar oculto. | Elige una `Position` diferente (p. ej., `HeaderLeft`) o ajusta la plantilla fuente. |
| **Los documentos grandes son lentos** | La numeración Bates itera sobre cada página; el uso de memoria crece con el tamaño del archivo. | Procesa el documento en fragmentos usando `Document.Split` si superas las 500 páginas. |
| **Expiración de la licencia** | La prueba gratuita de GroupDocs expira después de 30 días, provocando una excepción en `AddBatesNumbering`. | Aplica una clave de licencia válida antes de cargar el documento: `License license = new License(); license.SetLicense("license.lic");`. |

**Consejo profesional:** Si necesitas un formato de número diferente por caso (p. ej., `2023-CASE-001`), construye el prefijo de forma dinámica antes de crear `BatesNumberingOptions`.

## Ampliando la solución

El mismo enfoque de **Bates numbering C#** funciona con otros formatos de origen como `.txt`, `.html` o incluso imágenes. Simplemente cambia la extensión del archivo al crear el objeto `Document`, y el motor de conversión se encargará del resto.

También podrías combinar **document conversion C#** con OCR para PDFs escaneados:

```csharp
// Example: add OCR before numbering (requires GroupDocs.Viewer)
using GroupDocs.Viewer;
using GroupDocs.Viewer.Options;

Document scannedPdf = new Document(@"C:\Docs\scanned.pdf");
var viewer = new Viewer(scannedPdf);
var viewOptions = new HtmlViewOptions();
viewer.View(viewOptions); // OCR step
// Then apply Bates numbering as shown earlier
```

## Conclusión

Ahora sabes **cómo establecer opciones de numeración Bates** en C# de principio a fin. Creando un objeto `BatesNumberingOptions`, aplicándolo con `AddBatesNumbering` y guardando el resultado como PDF, puedes automatizar la producción de documentos legalmente compatibles y con identificadores únicos.  

A partir de aquí puedes explorar temas relacionados como **generación de PDF en C#**, **conversión de documentos C#**, o funciones avanzadas de la **API de GroupDocs** como marcas de agua y firmas digitales. Experimenta con diferentes prefijos, posiciones y formatos de número para adaptarlos a tu flujo de trabajo.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Agregar numeración Bates a PDF en C# – Guía completa](/pdf/english/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-in-c-complete-guide/)
- [Cómo agregar y personalizar números de página en PDFs usando Aspose.PDF para .NET \| Guía de manipulación de documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cómo agregar un pie de página de sello de texto en PDFs usando Aspose.PDF para .NET: Guía paso a paso](/pdf/english/net/document-manipulation/add-text-stamp-footer-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}