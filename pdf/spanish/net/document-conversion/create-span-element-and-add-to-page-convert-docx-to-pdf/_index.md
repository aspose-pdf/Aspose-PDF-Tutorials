---
category: general
date: 2026-03-27
description: Crear elemento span en C# y aprender cómo agregar el span a una página
  mientras se convierte un DOCX a PDF y se guarda como PDF. Guía paso a paso para
  desarrolladores.
draft: false
keywords:
- create span element
- how to add span
- convert docx to pdf
- add element to page
- save as pdf
language: es
og_description: Crea un elemento span en C# y aprende cómo agregar el span a una página
  mientras conviertes DOCX a PDF, luego guárdalo como PDF. Se incluye un ejemplo de
  código completo.
og_title: Crear elemento span y agregar a la página – Convertir DOCX a PDF
tags:
- C#
- DocumentProcessing
- PDFConversion
title: Crear elemento span y añadir a la página – Convertir DOCX a PDF
url: /es/net/document-conversion/create-span-element-and-add-to-page-convert-docx-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear elemento span y agregar a la página – Convertir DOCX a PDF

Crear **span element** en un archivo DOCX es una tarea común cuando necesitas un control preciso del diseño. En este tutorial te mostraremos **cómo agregar span** a una página, **convertir DOCX a PDF**, y **guardar como PDF**—todo en unos pocos pasos ordenados.  

Si alguna vez has mirado un documento de Word y pensado, “Ojalá pudiera colocar una pequeña caja de texto en una coordenada exacta”, estás en el lugar correcto. Te guiaremos a través de todo el flujo de trabajo, desde cargar el archivo fuente hasta obtener un PDF pulido.

## Lo que lograrás

Al final de esta guía podrás:

* Cargar un archivo `.docx` usando la clase `Document` de la biblioteca de documentos.  
* **Crear span element** con la API `TaggedContent`.  
* Posicionar ese span en coordenadas X/Y exactas en una página elegida.  
* **Agregar elemento a la página** de forma fiable, incluso cuando la página no es la primera.  
* **Convertir DOCX a PDF** y **guardar como PDF** con una única llamada a `Save`.

Sin herramientas externas, sin configuraciones misteriosas—solo código C# sencillo que puedes copiar‑pegar en tu proyecto.

## Requisitos previos

* .NET 6+ (o cualquier runtime .NET reciente que soporte tu biblioteca).  
* El SDK de procesamiento de documentos que proporciona `Document`, `TaggedContent`, `Position`, etc.  
* Un entendimiento básico de la sintaxis de C#—si puedes escribir un `Console.WriteLine`, estás listo.

> **Consejo profesional:** Mantén tu versión del SDK actualizada; la última versión (v3.2 a partir de marzo 2026) incluye mejoras de rendimiento para operaciones a nivel de página.

---

![Diagrama que ilustra cómo crear un elemento span y colocarlo en una página PDF](https://example.com/images/create-span-element.png "Create span element placement diagram")

## Crear elemento span – Posicionar y agregar a la página

A continuación tienes el código completo y ejecutable que hace todo, desde cargar el DOCX fuente hasta escribir el PDF final. Siéntete libre de insertarlo en una aplicación de consola, ajustar las rutas y ejecutarlo.

```csharp
using DocumentProcessing;   // Replace with the actual namespace of your SDK
using DocumentProcessing.Models;

class Program
{
    static void Main()
    {
        // Step 1: Load the DOCX you want to modify
        // -------------------------------------------------
        // The constructor takes a file path; make sure the file exists.
        Document doc = new Document(@"C:\Docs\input.docx");

        // Step 2: Create a new span element using the TaggedContent API
        // -------------------------------------------------
        // A span is a lightweight container for inline content.
        var span = doc.TaggedContent.CreateSpanElement();
        // Optional: add some text inside the span
        span.Text = "Hello, world!";

        // Step 3: Position the span at the desired coordinates (X = 50, Y = 750)
        // -------------------------------------------------
        // Position uses points (1/72 inch). Adjust as needed.
        span.Position = new Position(50, 750);

        // Step 4: Add the span to the target page (page index 1 = second page)
        // -------------------------------------------------
        // Pages are zero‑based; index 1 means the second page in the document.
        doc.Pages[1].Add(span);

        // Step 5: Convert the modified DOCX to PDF and save the result
        // -------------------------------------------------
        // The Save method automatically detects the output format from the extension.
        doc.Save(@"C:\Docs\output.pdf");

        // Confirmation output
        Console.WriteLine("Span added, document converted, and PDF saved successfully.");
    }
}
```

### Explicación paso a paso

#### Paso 1 – Cargar el documento DOCX  
Instanciamos un objeto `Document` apuntando a `input.docx`. Este objeto representa todo el archivo Word en memoria, dándonos acceso a páginas, contenido y metadatos.  

#### Paso 2 – Crear un elemento span  
La llamada `TaggedContent.CreateSpanElement()` devuelve un contenedor inline ligero. Piensa en él como una pequeña caja invisible que puede contener texto, imágenes u otros elementos inline. Agregar texto (`span.Text`) es opcional pero útil para depuración.

#### Paso 3 – Posicionar el span  
`new Position(50, 750)` establece la esquina superior izquierda del span a 50 pts del margen izquierdo y 750 pts del borde superior de la página. Estos valores son absolutos, por lo que puedes colocar el span en cualquier lugar—ideal para diseños precisos.

#### Paso 4 – Agregar el span a la página objetivo  
`doc.Pages[1].Add(span)` inserta el span en la segunda página. La API usa indexación basada en cero, por lo que la página 0 es la primera. Si necesitas agregarlo a la primera página, simplemente usa `doc.Pages[0]`.

#### Paso 5 – Convertir DOCX a PDF y guardar como PDF  
Llamar a `doc.Save("output.pdf")` hace dos cosas: escribe el documento modificado en disco **y** convierte el contenido a PDF debido a la extensión `.pdf`. No se requiere un paso de conversión adicional—esta es la forma más sencilla de **guardar como PDF**.

---

## Cómo agregar span en una página diferente (avanzado)

A veces no conoces el índice de la página de antemano. Puedes localizar una página por su número (amigable para el usuario) o buscando una palabra clave específica.

```csharp
// Find the page that contains the word "Summary"
int targetIndex = doc.Pages
    .Select((p, i) => new { Page = p, Index = i })
    .FirstOrDefault(x => x.Page.Text.Contains("Summary"))?.Index ?? 0;

// Fallback to first page if not found
targetIndex = Math.Max(targetIndex, 0);

// Add the span to the discovered page
doc.Pages[targetIndex].Add(span);
```

**Por qué es importante:** En informes donde el número de páginas varía, codificar `Pages[1]` puede romper el diseño. Este fragmento muestra un patrón robusto para **cómo agregar span** dinámicamente.

---

## Errores comunes y cómo evitarlos

| Problema | Qué ocurre | Solución |
|----------|------------|----------|
| **Span no visible** | Las coordenadas están fuera de la página o el span tiene ancho/alto cero. | Verifica los valores de `Position`; usa una regla en tu visor de PDF. |
| **Índice de página incorrecto** | Agregas a la página 0 pero esperas que esté en la página 2. | Recuerda que la API usa indexación cero; suma 1 al número de página humano. |
| **Guardar sobrescribe el origen** | `doc.Save("input.docx")` reemplaza el archivo original. | Siempre guarda en una ruta nueva (`output.pdf`) al convertir. |
| **Referencia al SDK faltante** | Error de compilación en la clase `Document`. | Instala el paquete NuGet: `dotnet add package DocumentProcessing.SDK`. |

---

## Verificando el resultado

Después de ejecutar el programa, abre `output.pdf` en cualquier visor de PDF. Deberías ver el texto “Hello, world!” posicionado exactamente en (50, 750) en la segunda página. Si el texto aparece en otro lugar, ajusta los valores de `Position` y vuelve a ejecutar.  

Para pruebas automatizadas, puedes usar un parser de PDF (p.ej., iTextSharp) para validar programáticamente las coordenadas del texto.

```csharp
// Example using iTextSharp to verify position (pseudo‑code)
var pdfReader = new PdfReader(@"C:\Docs\output.pdf");
var page = pdfReader.GetPageContent(2);
Debug.Assert(page.Contains("Hello, world!"));
```

---

## Próximos pasos

* **Estilizar el span** – explora `span.Font`, `span.Color` y otras propiedades de estilo.  
* **Agregar imágenes** – usa `CreateImageElement()` en lugar de un span para gráficos.  
* **Procesamiento por lotes** – recorrer una carpeta de archivos DOCX

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}