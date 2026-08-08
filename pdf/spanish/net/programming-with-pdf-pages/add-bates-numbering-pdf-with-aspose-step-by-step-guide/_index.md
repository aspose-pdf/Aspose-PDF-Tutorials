---
category: general
date: 2026-08-08
description: Agregar numeración Bates a PDF usando Aspose.Pdf en C#. Este tutorial
  también muestra cómo agregar una página en blanco al PDF y generar PDF programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering pdf
- add blank page pdf
- generate pdf programmatically
- create pdf aspose
language: es
lastmod: 2026-08-08
og_description: Agregar numeración Bates a PDF con Aspose.Pdf en C#. Aprende a añadir
  una página en blanco al PDF, generar PDF programáticamente y guardar el documento
  final en minutos.
og_image_alt: Screenshot of C# code adding Bates numbering and a blank page to a PDF
  using Aspose.Pdf
og_title: Agregar numeración Bates a PDF con Aspose – guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  headline: Add bates numbering pdf with Aspose – step‑by‑step guide
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. This tutorial also
    shows how to add blank page pdf and generate pdf programmatically.
  name: Add bates numbering pdf with Aspose – step‑by‑step guide
  steps:
  - name: What if I need a different font or position?
    text: 'The `BatesNumberingArtifact` exposes properties such as `FontSize`, `FontColor`,
      `HorizontalAlignment`, and `VerticalAlignment`. For example:'
  - name: How do I exclude a specific page from numbering?
    text: Create a separate `BatesNumberingArtifact` for the pages you want to number
      and add it only to those pages. Pages without an attached artifact will remain
      unnumbered.
  - name: Does this work with existing PDFs?
    text: 'Yes. Instead of `new Document()`, load an existing file:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF generation
- Bates numbering
title: Agregar numeración Bates a PDF con Aspose – guía paso a paso
url: /es/net/programming-with-pdf-pages/add-bates-numbering-pdf-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates a PDF con Aspose – guía paso a paso

Añadir numeración Bates a PDF con Aspose.Pdf es sencillo una vez que entiendes los pasos fundamentales. Si también necesitas añadir una página en blanco al PDF o generar PDF programáticamente, esta guía cubre todo lo que necesitas.

En este tutorial tú:

* Crear un nuevo documento PDF desde cero.  
* Añadir una página en blanco al PDF que alojará los números Bates.  
* Configurar el artefacto de numeración Bates con un prefijo personalizado.  
* Guardar el PDF para que los números aparezcan en el archivo generado.  

Al final tendrás una aplicación de consola C# totalmente funcional que produce un PDF que contiene números Bates como **CASE‑1000**, **CASE‑1001**, … – un requisito común para flujos de trabajo legales y de e‑discovery.

## Requisitos previos

* .NET 6.0 SDK o posterior (el código también funciona con .NET Framework 4.8).  
* Visual Studio 2022 o cualquier IDE compatible con C#.  
* Una licencia válida de Aspose.Pdf para .NET (o una clave de evaluación gratuita).  
* Familiaridad básica con la sintaxis de C#.

> **Consejo profesional:** Si ejecutas el código sin una licencia, Aspose añadirá una pequeña marca de agua al PDF de salida.

## Paso 1: Configurar el proyecto e importar Aspose.Pdf

Crear un nuevo proyecto de consola y añadir el paquete NuGet Aspose.Pdf:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
dotnet add package Aspose.Pdf
```

Las directivas `using` requeridas para el ejemplo son:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;
```

Estos espacios de nombres te dan acceso a las clases `Document`, `Page` y `BatesNumberingArtifact` que se usarán más adelante.

## Paso 2: Añadir una página en blanco al PDF

Un número Bates debe estar adjunto a una página, así que primero creamos una página en blanco que recibirá el artefacto de numeración.

```csharp
// Step 2: Add a blank page pdf
Document pdfDocument = new Document();          // creates an empty PDF
Page pdfPage = pdfDocument.Pages.Add();         // adds the first (blank) page
```

La clase `Document` representa todo el archivo PDF, mientras que `Pages.Add()` inserta una nueva página vacía al final de la colección de páginas del documento. Como el documento comienza vacío, esta llamada también crea la primera página.

## Paso 3: Configurar el artefacto de numeración Bates

Ahora definimos cómo deben verse los números Bates. El `BatesNumberingArtifact` te permite establecer el número inicial, prefijo, sufijo y opciones de formato.

```csharp
// Step 3: Define Bates numbering settings
BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
{
    StartNumber = 1000,          // first number in the sequence
    Prefix = "CASE-",            // custom prefix before each number
    // Optional: you can also set Suffix, FontSize, FontColor, etc.
};
```

**Por qué esto es importante:**  
Establecer `StartNumber` a **1000** coincide con las convenciones típicas de archivos de casos legales. El `Prefix` asegura que cada número aparezca como **CASE‑1000**, **CASE‑1001**, … lo que facilita la búsqueda y el ordenamiento.

## Paso 4: Adjuntar el artefacto a la página

El artefacto debe añadirse a la colección `Artifacts` de la página para que Aspose lo renderice en cada página durante el guardado.

```csharp
// Step 4: Attach the Bates numbering artifact to the PDF page
pdfPage.Artifacts.Add(batesArtifact);
```

Cuando el documento se guarda, Aspose repite automáticamente el artefacto en todas las páginas, incrementando el número para cada página subsiguiente.

## Paso 5: (Opcional) Añadir páginas adicionales

Si necesitas más páginas, simplemente repite `pdfDocument.Pages.Add()`. El artefacto de numeración Bates que adjuntaste en el paso anterior aparecerá automáticamente en cada nueva página.

```csharp
// Example: add two more pages
pdfDocument.Pages.Add();
pdfDocument.Pages.Add();
```

## Paso 6: Guardar el PDF – generar PDF programáticamente

Finalmente, persiste el documento en disco. Este es el punto en el que los números Bates se renderizan sobre las páginas.

```csharp
// Step 6: Save the PDF – generate pdf programmatically
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumberedDocument.pdf");

// Ensure the directory exists
Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);

pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved to: {outputPath}");
```

**Resultado esperado:**  
Abre *BatesNumberedDocument.pdf* y verás un PDF de tres páginas. Cada página muestra un número Bates en la esquina inferior derecha:

* Página 1 → **CASE‑1000**  
* Página 2 → **CASE‑1001**  
* Página 3 → **CASE‑1002**

Los números se incrementan automáticamente porque el artefacto está adjunto a la colección de páginas.

## Ejemplo completo y ejecutable

Juntando todo, aquí tienes un programa de consola completo que puedes copiar, pegar y ejecutar:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Artifacts;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new PDF document
            Document pdfDocument = new Document();

            // Add a blank page pdf
            Page pdfPage = pdfDocument.Pages.Add();

            // Define Bates numbering settings (add bates numbering pdf)
            BatesNumberingArtifact batesArtifact = new BatesNumberingArtifact(pdfPage)
            {
                StartNumber = 1000,
                Prefix = "CASE-"
            };

            // Attach the artifact to the page
            pdfPage.Artifacts.Add(batesArtifact);

            // (Optional) add more pages to see incremented numbers
            pdfDocument.Pages.Add(); // page 2
            pdfDocument.Pages.Add(); // page 3

            // Save the PDF – generate pdf programmatically
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "BatesNumberedDocument.pdf");

            Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
            pdfDocument.Save(outputPath);

            Console.WriteLine($"PDF saved to: {outputPath}");
        }
    }
}
```

Ejecuta el programa con `dotnet run`. Después de la ejecución, localiza el archivo en tu escritorio y verifica los números Bates.

![Ejemplo de añadir numeración Bates a PDF](/images/bates-numbering.png "Ejemplo de añadir numeración Bates a PDF")

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito una fuente o posición diferente?

El `BatesNumberingArtifact` expone propiedades como `FontSize`, `FontColor`, `HorizontalAlignment` y `VerticalAlignment`. Por ejemplo:

```csharp
batesArtifact.FontSize = 12;
batesArtifact.FontColor = Color.Blue;
batesArtifact.HorizontalAlignment = HorizontalAlignment.Left;
batesArtifact.VerticalAlignment = VerticalAlignment.Top;
```

### ¿Cómo excluyo una página específica de la numeración?

Crea un `BatesNumberingArtifact` separado para las páginas que deseas numerar y añádelo solo a esas páginas. Las páginas sin un artefacto adjunto permanecerán sin numerar.

### ¿Esto funciona con PDFs existentes?

Sí. En lugar de `new Document()`, carga un archivo existente:

```csharp
Document pdfDocument = new Document("input.pdf");
```

Luego adjunta el artefacto a las páginas deseadas y guarda.

## Conclusión

Ahora sabes cómo **añadir numeración Bates a PDF** usando Aspose.Pdf, cómo **añadir una página en blanco al PDF**, y cómo **generar PDF programáticamente** en una solución C# limpia y reutilizable. El enfoque funciona con cualquier número de páginas, prefijos personalizados y opciones de estilo, dándote control total sobre el documento final.

Los siguientes pasos que podrías explorar:

* Usar **create pdf as

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo añadir y personalizar números de página en PDFs usando Aspose.PDF para .NET \| Guía de manipulación de documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Cómo añadir una página vacía al final de un PDF usando Aspose.PDF para .NET \| Guía paso a paso](/pdf/english/net/document-manipulation/add-empty-page-end-pdf-aspose-pdf-net/)
- [Crear documento PDF con Aspose.PDF – Añadir página, forma y guardar](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}