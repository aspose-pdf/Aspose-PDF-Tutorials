---
category: general
date: 2026-08-14
description: Crear un diccionario PDF vacío en C# usando Aspose.Pdf – aprende cómo
  agregar un estado gráfico a la colección ExtGState y modificar PDFs programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- Aspose.Pdf Document
- PDF graphics state
- ExtGState dictionary
- CosPdfDictionary usage
language: es
lastmod: 2026-08-14
og_description: Crear un diccionario PDF vacío en C# con Aspose.Pdf. Sigue esta guía
  completa para añadir un estado gráfico personalizado a la colección ExtGState de
  un PDF.
og_image_alt: Screenshot showing C# code that creates an empty PDF dictionary with
  Aspose.Pdf
og_title: Crear un diccionario PDF vacío en C# – Guía paso a paso de Aspose.Pdf
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  headline: Create empty PDF dictionary in C# with Aspose.Pdf
  type: TechArticle
- description: Create empty PDF dictionary in C# using Aspose.Pdf – learn how to add
    a graphics state to the ExtGState collection and modify PDFs programmatically.
  name: Create empty PDF dictionary in C# with Aspose.Pdf
  steps:
  - name: Create a new **Console App** project in Visual Studio.
    text: Create a new **Console App** project in Visual Studio.
  - name: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
    text: 'Open the **NuGet Package Manager** and install `Aspose.Pdf`:'
  - name: 'Add the following `using` directives at the top of `Program.cs`:'
    text: 'Add the following `using` directives at the top of `Program.cs`:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Crear un diccionario PDF vacío en C# con Aspose.Pdf
url: /es/net/programming-with-operators/create-empty-pdf-dictionary-in-c-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear un diccionario PDF vacío en C# con Aspose.Pdf

Si necesitas **crear objetos de diccionario PDF vacío** mientras trabajas con archivos PDF, esta guía te muestra exactamente cómo hacerlo en C# usando la biblioteca Aspose.Pdf. Ya sea que estés construyendo un estado gráfico personalizado, añadiendo un nuevo recurso o preparando una plantilla para uso posterior, los pasos a continuación te ofrecen una solución completa y ejecutable.

Aprenderás a cargar un PDF, acceder al diccionario de recursos de la primera página, crear un `CosPdfDictionary` totalmente nuevo y insertarlo en la colección `ExtGState`. Al final del tutorial tendrás un `output.pdf` que contiene el diccionario recién creado.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)
- Visual Studio 2022 o cualquier IDE de C# que prefieras
- Una licencia de Aspose.Pdf para .NET (o una clave de evaluación temporal)
- Un PDF de ejemplo llamado **input.pdf** colocado en una carpeta que controles (la ruta de la carpeta se usará como `dataDir`)

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`.

## Paso 1: Configurar el proyecto y referenciar Aspose.Pdf

1. Crea un nuevo proyecto **Console App** en Visual Studio.  
2. Abre el **Administrador de paquetes NuGet** e instala `Aspose.Pdf`:

   ```bash
   dotnet add package Aspose.Pdf
   ```

3. Añade las siguientes directivas `using` al inicio de `Program.cs`:

   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Text;
   using Aspose.Pdf.Operators;
   using Aspose.Pdf.Facades;
   using Aspose.Pdf.InteractiveFeatures;
   using Aspose.Pdf.Xmp;
   using Aspose.Pdf.Operators.Filters;
   using Aspose.Pdf.Operators.Gfx;
   ```

   *¿Por qué estos espacios de nombres?* `Aspose.Pdf` contiene la clase central `Document`, mientras que `Aspose.Pdf.Operators.Gfx` proporciona `CosPdfDictionary`, `CosPdfNumber` y otros objetos PDF de bajo nivel necesarios para **crear estructuras de diccionario PDF vacío**.

## Paso 2: Cargar el PDF de origen

La primera operación es cargar el archivo PDF existente en una instancia de `Document`. Esto te brinda acceso a todas las páginas, recursos y diccionarios de bajo nivel.

```csharp
// Step 2: Load the PDF document
string dataDir = @"C:\MyPdfFolder\";               // Change to your folder
using var pdfDocument = new Document(dataDir + "input.pdf");
```

*Explicación*: `Document` lee el archivo en memoria y prepara las estructuras internas. La sentencia `using` garantiza que el manejador del archivo se libere después de que terminemos el procesamiento.

## Paso 3: Acceder al diccionario de recursos de la primera página

Cada página PDF tiene un diccionario **Resources** que agrupa fuentes, imágenes, objetos ExtGState y otros recursos compartidos. Para insertar un nuevo estado gráfico necesitamos editar este diccionario.

```csharp
// Step 3: Get the first page and its Resources dictionary
Page firstPage = pdfDocument.Pages[1];                     // PDF pages are 1‑based
DictionaryEditor resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor` es una clase auxiliar que te permite tratar un diccionario PDF como un `Dictionary<string, object>` de C#.

## Paso 4: Recuperar (o crear) la colección ExtGState

`ExtGState` contiene objetos de estado gráfico como opacidad, modo de fusión y ancho de línea. Si el PDF de origen ya contiene una entrada `ExtGState`, la reutilizamos; de lo contrario creamos un nuevo diccionario vacío.

```csharp
// Step 4: Ensure an ExtGState dictionary exists
CosPdfDictionary extGStateDict;
if (resourcesEditor.ContainsKey("ExtGState"))
{
    extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
}
else
{
    // Create a brand‑new ExtGState dictionary and add it to Resources
    extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
    resourcesEditor["ExtGState"] = extGStateDict;
}
```

*¿Por qué esta comprobación?* Algunos PDFs omiten la entrada `ExtGState` por completo. Al manejar ambos casos, el tutorial se mantiene robusto para cualquier archivo de entrada.

## Paso 5: **Crear diccionario PDF vacío** para un nuevo estado gráfico

Ahora realmente **creamos objetos de diccionario PDF vacío** que definen los parámetros del estado gráfico. El diccionario comienza vacío y añadimos las claves requeridas:

```csharp
// Step 5: Build a new graphics state dictionary (empty PDF dictionary + entries)
CosPdfDictionary newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);

// Stroke opacity (CA) – 1 means fully opaque strokes
newGraphicsState.Add("CA", new CosPdfNumber(1));

// Fill opacity (ca) – 0.5 makes semi‑transparent fills
newGraphicsState.Add("ca", new CosPdfNumber(0.5));

// Blend mode (BM) – "Normal" is the default compositing mode
newGraphicsState.Add("BM", new CosPdfName("Normal"));
```

### Qué hace cada entrada

| Clave | Tipo | Significado |
|-------|------|-------------|
| **CA** | `CosPdfNumber` | Opacidad del trazo (rango 0‑1). |
| **ca** | `CosPdfNumber` | Opacidad del relleno (rango 0‑1). |
| **BM** | `CosPdfName`   | Modo de fusión; `"Normal"` es el más común. |

Como partimos de un **diccionario PDF vacío**, tienes control total sobre qué entradas se añaden. Puedes ampliar este diccionario con parámetros adicionales de estado gráfico como `LW` (ancho de línea) o `LC` (cap de línea) cuando lo necesites.

## Paso 6: Insertar el nuevo estado gráfico en ExtGState

El diccionario `ExtGState` funciona como un mapa donde cada entrada se identifica por un nombre (p. ej., `GS0`, `GS1`). Añadimos nuestro diccionario recién creado bajo una clave única.

```csharp
// Step 6: Add the graphics state to the ExtGState collection
extGStateDict.Add("GS0", newGraphicsState);
```

Si planeas añadir varios estados, incrementa el sufijo (`GS1`, `GS2`, …) para evitar colisiones de nombres.

## Paso 7: Guardar el PDF modificado

Finalmente, escribe los cambios en disco. El método `Save` serializa automáticamente los diccionarios actualizados.

```csharp
// Step 7: Persist the changes
pdfDocument.Save(dataDir + "output.pdf");
```

Abre `output.pdf` en cualquier visor de PDF e inspecciona la entrada **Resources → ExtGState** (la mayoría de los visores la ocultan, pero herramientas como Adobe Acrobat Preflight o PDF‑Tron pueden revelarla). Deberías ver una entrada `GS0` que contiene los valores de opacidad y modo de fusión que definiste.

## Ejemplo completo y funcional

Juntando todas las piezas, aquí tienes el programa completo que puedes copiar‑pegar en `Program.cs` y ejecutar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Operators.Gfx;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Load the PDF document
        // -----------------------------------------------------------------
        string dataDir = @"C:\MyPdfFolder\"; // <-- change to your folder
        using var pdfDocument = new Document(dataDir + "input.pdf");

        // -----------------------------------------------------------------
        // 2️⃣ Access the first page’s Resources dictionary
        // -----------------------------------------------------------------
        Page firstPage = pdfDocument.Pages[1];
        var resourcesEditor = new DictionaryEditor(firstPage.Resources);

        // -----------------------------------------------------------------
        // 3️⃣ Retrieve or create the ExtGState dictionary
        // -----------------------------------------------------------------
        CosPdfDictionary extGStateDict;
        if (resourcesEditor.ContainsKey("ExtGState"))
        {
            extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();
        }
        else
        {
            extGStateDict = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            resourcesEditor["ExtGState"] = extGStateDict;
        }

        // -----------------------------------------------------------------
        // 4️⃣ **Create empty PDF dictionary** for a new graphics state
        // -----------------------------------------------------------------
        var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
        newGraphicsState.Add("CA", new CosPdfNumber(1));          // Stroke opacity
        newGraphicsState.Add("ca", new CosPdfNumber(0.5));        // Fill opacity
        newGraphicsState.Add("BM", new CosPdfName("Normal"));    // Blend mode

        // -----------------------------------------------------------------
        // 5️⃣ Add the graphics state to ExtGState
        // -----------------------------------------------------------------
        extGStateDict.Add("GS0", newGraphicsState);

        // -----------------------------------------------------------------
        // 6️⃣ Save the modified PDF
        // -----------------------------------------------------------------
        pdfDocument.Save(dataDir + "output.pdf");

        Console.WriteLine("PDF saved with new empty dictionary at: " + dataDir + "output.pdf");
    }
}
```

**Salida esperada** – La consola muestra una línea de confirmación, y `output.pdf` contiene la nueva entrada `GS0` bajo `ExtGState`. Cuando renderices una página que haga referencia a `GS0` (p. ej., mediante el operador de flujo de contenido `gs`), los trazos serán totalmente opacos mientras que los rellenos tendrán un 50 % de transparencia.

## Preguntas frecuentes y manejo de casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si el PDF tiene varias páginas?* | El ejemplo se dirige a la primera página (`Pages[1]`). Para afectar a todas las páginas, recorre `pdfDocument.Pages` y repite los pasos 3‑5 para los recursos de cada página. |
| *¿Puedo añadir el diccionario a una página que ya tiene una entrada ExtGState llamada “GS0”?* | Sí, pero debes usar una clave diferente (`GS1`, `GS2`, …) para no sobrescribir la entrada existente. |
| *¿Es seguro modificar el diccionario después de guardar?* | Una vez que llamas a `Save`, la representación en memoria se separa del archivo. Puedes seguir editando el objeto `Document` y volver a llamar a `Save` si lo necesitas. |
| *¿Necesito una licencia para Aspose.Pdf para usar ` | 

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear líneas discontinuas en PDFs usando Aspose.PDF para .NET&#58; Guía paso a paso](/pdf/english/net/images-graphics/create-dashed-lines-aspose-pdf-net/)
- [Cómo eliminar gráficos de PDFs usando Aspose.PDF .NET&#58; Guía completa](/pdf/english/net/images-graphics/remove-graphics-aspose-pdf-net/)
- [Cómo crear PDFs multilayer usando Aspose.PDF para .NET&#58; Guía exhaustiva](/pdf/english/net/advanced-features/create-multi-layer-pdfs-aspose-pdf-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}