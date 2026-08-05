---
category: general
date: 2026-08-04
description: Crea un nuevo documento PDF en C# y agrega numeración Bates al PDF rápidamente
  usando Aspose.Pdf – aprende a añadir una página en blanco al PDF y números de página
  personalizados.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new pdf document
- add bates numbering pdf
- how to add bates
- add blank page pdf
- add custom page numbers
language: es
lastmod: 2026-08-04
og_description: Crear un nuevo documento PDF en C# y agregar automáticamente numeración
  Bates al PDF para la gestión de casos legales – ejemplo de código completo incluido.
og_image_alt: Screenshot of a C# program creating a PDF document with Bates numbers
  applied
og_title: Crear un nuevo documento PDF con numeración Bates en C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create new PDF document in C# and add Bates numbering pdf quickly using
    Aspose.Pdf – learn to add blank page pdf and custom page numbers.
  headline: Create new PDF document with Bates numbering in C#
  type: TechArticle
tags:
- C#
- PDF
- Aspose.Pdf
- Bates numbering
title: Crear nuevo documento PDF con numeración Bates en C#
url: /es/net/document-creation/create-new-pdf-document-with-bates-numbering-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear un nuevo documento PDF con numeración Bates en C#

Si necesitas **crear un nuevo documento PDF** en C#, esta guía te muestra cómo **añadir numeración Bates al pdf** usando Aspose.Pdf. Aprenderás a **añadir una página en blanco al pdf**, configurar **añadir números de página personalizados**, y guardar el archivo final.

El tutorial cubre cada paso, desde la instalación de la biblioteca hasta la generación de un PDF que cumple con los estándares legales de expedientes. Al final podrás generar un PDF, insertar una página en blanco, aplicar números Bates y personalizar el formato de numeración, todo con un único programa ejecutable.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK o posterior instalado  
* Visual Studio 2022 (o cualquier IDE de C#)  
* Una licencia activa de Aspose.Pdf para .NET o una clave de evaluación gratuita  

No necesitas paquetes NuGet adicionales; el tutorial instala todo automáticamente.

## Paso 1: Instalar Aspose.Pdf vía NuGet

Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.Pdf
```

El comando agrega la última versión estable de Aspose.Pdf a tu proyecto, la cual proporciona las clases `Document`, `BatesNumbering` y otras de manipulación de PDF que usarás.

## Paso 2: Crear nuevo documento PDF – configuración inicial

Crear el archivo PDF es la base para cualquier operación posterior. La clase `Document` representa todo el contenedor PDF.

```csharp
using Aspose.Pdf;

// Step 2: Create a new PDF document
using var doc = new Document();
```

*Por qué es importante*: Instanciar `Document` asigna las estructuras internas necesarias para páginas, fuentes y gráficos. Usar `using var` garantiza que el archivo se libere correctamente después de guardarse.

## Paso 3: Añadir página en blanco al pdf

Un PDF debe contener al menos una página antes de que puedas colocar contenido en ella. Añadir una página en blanco te brinda un lienzo limpio para los números Bates.

```csharp
// Step 3: Add a blank page to the document
Page page = doc.Pages.Add();
```

El método `Pages.Add()` agrega una nueva página vacía al final de la colección de páginas del documento. Puedes repetir esta llamada para añadir más páginas si luego necesitas **añadir números de página personalizados** en varias páginas.

## Paso 4: Configurar la numeración Bates – cómo añadir Bates

La numeración Bates es un identificador secuencial usado comúnmente en documentos legales. La configuras mediante la clase `BatesNumbering`.

```csharp
// Step 4: Set up Bates numbering options
var bates = new BatesNumbering
{
    StartNumber = 1000,      // Starting number for the sequence
    Prefix = "CaseA-",       // Text to prepend to each number
    Increment = 1,           // Increment between consecutive numbers
    // Optional: Set the location, font size, etc.
};
```

*Por qué es importante*: `StartNumber` define el primer número, `Prefix` agrega una etiqueta legible, y `Increment` controla el tamaño del paso. También puedes ajustar `HorizontalAlignment`, `VerticalAlignment`, `FontSize` y `Margins` para controlar la apariencia del número en cada página.

## Paso 5: Aplicar la numeración Bates al pdf en la página

Ahora que las opciones de numeración están listas, aplícalas a la página (o a todo el documento).

```csharp
// Step 5: Apply the Bates numbering to the page
bates.Apply(page);
```

Llamar a `Apply` inserta el número formateado en el pie de página por defecto. Si necesitas el número en otro lugar, establece `bates.Position` antes de llamar a `Apply`.

## Paso 6: Guardar el PDF con los números Bates aplicados

Finalmente, escribe el documento en memoria en disco.

```csharp
// Step 6: Save the PDF with Bates numbers applied
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "BatesNumbered.pdf");

doc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

El archivo guardado ahora contiene una sola página con el número Bates **CaseA-1000** mostrado en la parte inferior. Abre el PDF en cualquier visor para verificar la numeración.

## Resultado esperado

Al abrir `BatesNumbered.pdf`, deberías ver:

* Una página en blanco (o más si añadiste páginas adicionales)  
* El texto **CaseA-1000** posicionado en la parte inferior de la página (ubicación predeterminada)  

Si añades más páginas y reutilizas la misma instancia de `BatesNumbering`, los números se incrementarán automáticamente (CaseA-1001, CaseA-1002, …).

## Consejo profesional: Añadir números de página personalizados además de los números Bates

A veces necesitas tanto números Bates como números de página tradicionales. Puedes combinarlos añadiendo un `TextFragment` después de aplicar la numeración Bates:

```csharp
// Add a traditional page number in the header
var pageNumber = new TextFragment($"Page {page.Number}")
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment = VerticalAlignment.Top,
    FontSize = 12,
    Font = FontRepository.FindFont("Arial")
};
page.Paragraphs.Add(pageNumber);
```

Este fragmento demuestra **añadir números de página personalizados** mientras se conserva la etiqueta Bates.

## Caso límite: Aplicar numeración Bates a varias páginas

Si tu documento contiene varias páginas, puedes aplicar la misma instancia de `BatesNumbering` a cada página dentro de un bucle:

```csharp
for (int i = 1; i <= doc.Pages.Count; i++)
{
    bates.Apply(doc.Pages[i]);
}
```

El bucle asegura que cada página reciba un número secuencial basado en el `StartNumber` y `Increment` que definiste.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Los números aparecen descentrados | La alineación predeterminada puede no coincidir con tu diseño | Establece `bates.HorizontalAlignment` y `bates.VerticalAlignment` explícitamente |
| Los números se superponen al contenido existente | No se definió margen | Ajusta `bates.Margin` o usa `bates.Position` para mover el número |
| Excepción de licencia en tiempo de ejecución | La versión de evaluación limita la salida | Aplica una licencia válida de Aspose.Pdf antes de crear el documento (`License license = new License(); license.SetLicense("Aspose.Pdf.lic");`) |

## Ejemplo completo funcional

A continuación tienes un programa autónomo que puedes copiar, pegar y ejecutar.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1. Create a new PDF document
        using var doc = new Document();

        // 2. Add a blank page pdf
        Page page = doc.Pages.Add();

        // 3. Configure Bates numbering – how to add bates
        var bates = new BatesNumbering
        {
            StartNumber = 1000,
            Prefix = "CaseA-",
            Increment = 1,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(20, 20, 20, 20),
            FontSize =


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo añadir y personalizar números de página en PDFs usando Aspose.PDF para .NET | Guía de manipulación de documentos](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [Aspose.PDF .NET: Añadir números de página a PDFs usando FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Crear documento PDF con Aspose.PDF – Añadir página, forma y guardar](/pdf/english/net/document-creation/create-pdf-document-with-aspose-pdf-add-page-shape-save/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}