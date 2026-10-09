---
category: general
date: 2026-06-21
description: Añade numeración Bates en Word rápidamente. Aprende cómo agregar Bates,
  aplicar numeración Bates a documentos legales y automatizar la numeración con C#.
draft: false
keywords:
- add bates numbering
- how to add bates
- bates numbering in word
- bates numbering for legal
- apply bates numbering
language: es
og_description: Agregar numeración Bates en Word usando C#. Esta guía muestra cómo
  agregar Bates, aplicar numeración Bates a documentos legales y automatizar el proceso.
og_title: Agregar numeración Bates en Word – Guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  headline: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add Bates numbering in Word quickly. Learn how to add Bates, apply
    Bates numbering for legal docs, and automate numbering with C#.
  name: Add Bates Numbering in Word – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| Page | Bates Number | |------|--------------| | 1 | ABC-1000 | | 2 |
      ABC-1001 | | … | … | | N | ABC‑(1000 + N‑1) |'
  - name: What if the document already contains page numbers?
    text: The `AddBatesNumbering` method will **not** overwrite existing page number
      fields; it simply adds a new field. If you want to replace the existing numbers,
      remove them first or set `batesOptions.Position` to the same location as the
      current page numbers.
  - name: Can I skip pages (e.g., exclude a cover page)?
    text: 'Yes. Use the overload that accepts a `PageRange`:'
  - name: How do I change the numbering format (Roman numerals, letters)?
    text: 'The `BatesNumberingOptions` class supports a `NumberFormat` property:'
  - name: What about performance on huge files?
    text: Loading a 2‑GB Word file can consume a lot of RAM. To mitigate, process
      the document in chunks using the `DocumentSplitter` utility, apply Bates numbering
      to each chunk, then merge the parts back together. This pattern keeps memory
      usage under control while still letting you **apply bates numbering*
  type: HowTo
tags:
- document‑automation
- csharp
- legal‑tech
title: Agregar numeración Bates en Word – Guía completa paso a paso
url: /es/net/programming-with-document/add-bates-numbering-in-word-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates en Word – Guía completa paso a paso

¿Alguna vez te has preguntado cómo añadir numeración Bates a un archivo de Word sin escribir manualmente cada número? No estás solo. Muchos abogados, asistentes legales y especialistas en e‑discovery necesitan una forma fiable de **añadir numeración Bates** a cientos de páginas, y hacerlo a mano es una pesadilla.

En este tutorial recorreremos una solución limpia en C# que **aplica numeración Bates** a un archivo `.docx`, explica por qué cada línea es importante y te muestra cómo ajustar el código para necesidades legales específicas. Al final podrás generar un documento perfectamente numerado en segundos—sin plugins adicionales.

## Lo que aprenderás

- El código exacto necesario para **añadir numeración Bates** a un documento Word.
- Cómo funciona la clase `BatesNumberingOptions` y por qué podrías ajustar el prefijo o el valor inicial.
- Consejos para usar este enfoque en archivos de casos grandes, incluyendo consideraciones de memoria.
- Una breve descripción de los requisitos previos para que puedas copiar‑pegar la solución y ejecutarla hoy.

**Requisitos previos**  
- .NET 6+ (or .NET Framework 4.7.2+ if you prefer the older runtime).  
- Una referencia a la biblioteca Aspose.Words for .NET (o cualquier API similar que exponga `AddBatesNumbering`).  
- Familiaridad básica con C# y Visual Studio (or your favourite IDE).

Si te sientes cómodo con eso, vamos a sumergirnos.

## Paso 1: Configurar el proyecto e importar la biblioteca

Primero, crea una nueva aplicación de consola (o intégrala en un servicio existente). Luego agrega el paquete NuGet de Aspose.Words:

```bash
dotnet add package Aspose.Words
```

> **Consejo profesional:** Usa la licencia de evaluación gratuita para pruebas; agrega una pequeña marca de agua pero funciona exactamente como la versión completa.

```csharp
using Aspose.Words;
using Aspose.Words.BatesNumbering;
```

Estas sentencias `using` traen las clases `Document` y `BatesNumberingOptions` al alcance, lo cual es esencial para el paso de **aplicar numeración Bates** más adelante.

## Paso 2: Cargar el documento fuente

Necesitarás un archivo Word para trabajar. El código a continuación carga `input.docx` desde una carpeta que especifiques. Reemplaza `"YOUR_DIRECTORY"` con la ruta real en tu máquina.

```csharp
// Step 1: Load the source document
var document = new Document("YOUR_DIRECTORY/input.docx");
```

¿Por qué cargar el archivo primero? El objeto `Document` analiza todo el paquete Word en memoria, permitiéndonos manipular encabezados, pies de página y diseños de página antes de guardarlo. Si el archivo es enorme (por ejemplo, 10,000 páginas), considera usar `LoadOptions` con `LoadFormat.Docx` para transmitir secciones en lugar de cargar todo de una vez.

## Paso 3: Configurar las opciones de numeración Bates

Aquí es donde ocurre la magia. Le indicas a la biblioteca qué prefijo usar (`"ABC-"` en el ejemplo) y dónde comenzar a contar (`1000`). Ambos valores son totalmente personalizables.

```csharp
// Step 2: Define Bates numbering options (prefix and starting number)
var batesOptions = new BatesNumberingOptions
{
    Prefix = "ABC-",
    Start = 1000,
    // Optional: set the position, alignment, and font if you need legal‑specific styling
    // Position = BatesNumberingPosition.Footer,
    // Alignment = BatesNumberingAlignment.Right,
    // Font = new Font("Times New Roman", 10, FontStyle.Bold)
};
```

**¿Por qué un prefijo?** En la práctica legal, los prefijos a menudo identifican el caso o la parte productora (`"ABC-"` podría representar *Acme Bank Corp.*). Comenzar en `1000` es común porque muchas firmas reservan los primeros 999 números para borradores internos.

Si estás trabajando con **numeración Bates para documentos legales**, también podrías querer establecer `batesOptions.Position` a `Header` o `Footer` y ajustar la alineación para cumplir con las reglas del tribunal. La biblioteca soporta estos ajustes de forma nativa.

## Paso 4: Aplicar numeración Bates a todo el documento

Ahora realmente inyectamos los números. El método `AddBatesNumbering` recorre cada página, inserta la cadena formateada y actualiza el recuento interno de páginas del documento.

```csharp
// Step 3: Apply Bates numbering to the entire document
document.AddBatesNumbering(batesOptions);
```

Detrás de escena, Aspose.Words crea un campo oculto en cada página que se muestra como `ABC-1000`, `ABC-1001`, etc. Como es un campo, puedes editar más tarde el prefijo o el número inicial sin volver a generar todo el archivo—útil para **cómo añadir bates** después de que cambie una solicitud de descubrimiento.

## Paso 5: Guardar el documento modificado

Finalmente, escribe la salida a un nuevo archivo. Mantener el original intacto es una buena práctica, especialmente al manejar evidencia que debe permanecer impecable.

```csharp
// Step 4: Save the modified document
document.Save("YOUR_DIRECTORY/output.docx");
```

Ahora tienes `output.docx` con números Bates secuenciales añadidos a cada página. Ábrelo en Word y verás los números exactamente donde los especificaste (pie de página por defecto). El tamaño del archivo puede aumentar ligeramente debido a los campos adicionales, pero es insignificante comparado con los beneficios.

### Salida esperada

| Página | Número Bates |
|--------|--------------|
| 1      | ABC-1000     |
| 2      | ABC-1001     |
| …      | …            |
| N      | ABC‑(1000 + N‑1) |

Si abres la vista de “Códigos de campo” del documento (`Alt+F9` en Word), verás algo como `{ BATES \* MERGEFORMAT ABC-1000 }` en cada página.

## Casos límite y preguntas frecuentes

### ¿Qué pasa si el documento ya contiene números de página?

El método `AddBatesNumbering` **no** sobrescribirá los campos de número de página existentes; simplemente añade un nuevo campo. Si deseas reemplazar los números existentes, elimínalos primero o establece `batesOptions.Position` en la misma ubicación que los números de página actuales.

### ¿Puedo omitir páginas (p.ej., excluir una portada)?

Sí. Usa la sobrecarga que acepta un `PageRange`:

```csharp
var range = new PageRange(2, document.PageCount); // start at page 2
document.AddBatesNumbering(batesOptions, range);
```

Esto es útil cuando necesitas **numeración Bates para documentos legales** que comienzan después de una página de título.

### ¿Cómo cambio el formato de numeración (números romanos, letras)?

La clase `BatesNumberingOptions` soporta una propiedad `NumberFormat`:

```csharp
batesOptions.NumberFormat = BatesNumberFormat.RomanUpper;
```

Establécela antes de llamar a `AddBatesNumbering`. Esta flexibilidad ayuda cuando un tribunal exige un estilo específico.

### ¿Qué pasa con el rendimiento en archivos enormes?

Cargar un archivo Word de 2 GB puede consumir mucha RAM. Para mitigarlo, procesa el documento en fragmentos usando la utilidad `DocumentSplitter`, aplica numeración Bates a cada fragmento y luego une las partes nuevamente. Este patrón mantiene el uso de memoria bajo control mientras te permite **aplicar numeración Bates** de manera eficiente.

## Ejemplo completo funcionando

Juntando todo, aquí tienes un programa de consola listo para ejecutar:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.BatesNumbering;

namespace BatesNumberingDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document
            var inputPath = @"C:\Docs\input.docx";
            var document = new Document(inputPath);

            // 2️⃣ Define Bates numbering options
            var batesOptions = new BatesNumberingOptions
            {
                Prefix = "ABC-",
                Start = 1000,
                // Optional styling for legal compliance
                Position = BatesNumberingPosition.Footer,
                Alignment = BatesNumberingAlignment.Right,
                Font = new Font("Times New Roman", 9, FontStyle.Bold)
            };

            // 3️⃣ Apply Bates numbering across all pages
            document.AddBatesNumbering(batesOptions);

            // 4️⃣ Save the result
            var outputPath = @"C:\Docs\output.docx";
            document.Save(outputPath);

            Console.WriteLine($"✅ Bates numbering applied! Saved to {outputPath}");
        }
    }
}
```

Ejecuta el programa, abre `output.docx` y verás una serie limpia de números listos para presentar, descubrimiento o presentación ante el tribunal.

## Conclusión

Ahora sabes exactamente **cómo añadir Bates** a un documento Word usando C#. Los pasos—cargar, configurar, aplicar y guardar—son sencillos, pero lo suficientemente flexibles para satisfacer los flujos de trabajo de **numeración Bates para legal**, prefijos personalizados e incluso procesamiento por lotes a gran escala.

Si estás listo para llevar esto más allá, considera:

- Integrar el código en una API web para que los colegas puedan subir archivos y recibir PDFs numerados al instante.  
- Agregar manejo de errores para archivos faltantes o problemas de permisos (un rápido `try/catch` alrededor de `Document.Load`).  
- Explorar otras características de Aspose.Words como marcas de agua o redacción para una suite completa de herramientas de e‑discovery.

Siéntete libre de experimentar con diferentes prefijos, números iniciales, o incluso combinar varios esquemas de numeración en el mismo documento. El mundo de **aplicar numeración Bates** es sorprendentemente versátil una vez que tienes la lógica central bajo control.

¿Tienes preguntas o un escenario complicado? Deja un comentario abajo y lo resolveremos juntos. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Aplicar estilo de numeración en encabezado de PDF usando Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aplicar estilo de numeración en encabezado de PDF usando Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aplicar estilo de numeración en encabezado de PDF usando Java](/pdf/french/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}