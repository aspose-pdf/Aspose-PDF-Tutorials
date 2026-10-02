---
category: general
date: 2026-02-14
description: 'Crear documento PDF en C# rápidamente: agregar una página al PDF, dibujar
  una forma rectangular y guardar el PDF en un archivo usando Aspose.Pdf en unas pocas
  líneas de código.'
draft: false
keywords:
- create pdf document c#
- add page to pdf
- how to draw rectangle
- add shape to pdf
- save pdf to file
language: es
og_description: Crea documentos PDF en C# en minutos. Aprende cómo agregar una página
  al PDF, dibujar un rectángulo, añadir una forma al PDF y guardar el PDF en un archivo
  con ejemplos de código claros.
og_title: Crear documento PDF en C# – Guía paso a paso
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Crear documento PDF en C# – Añadir página, dibujar rectángulo y guardar
url: /es/net/document-creation/create-pdf-document-c-add-page-draw-rectangle-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF C# – Añadir página, dibujar rectángulo y guardar

¿Alguna vez necesitaste **crear documento PDF C#** desde cero y te preguntaste por dónde empezar? No eres el único: muchos desarrolladores se topan con ese mismo obstáculo al abordar por primera vez la generación programática de PDFs. ¿La buena noticia? Con unas pocas líneas de código de Aspose.Pdf puedes añadir una página al PDF, dibujar un rectángulo y **guardar el PDF en un archivo** sin sudar.

En este tutorial recorreremos todo lo que necesitas: inicializar el PDF, insertar una nueva página, dibujar una forma de rectángulo y, finalmente, persistir el archivo en disco. Al final tendrás una aplicación de consola ejecutable que produce un rectángulo con borde azul dentro de una página PDF recién creada.

## Qué necesitarás

- **.NET 6 o posterior** (el ejemplo usa declaraciones de nivel superior, pero cualquier versión reciente de .NET funciona)
- **Aspose.Pdf for .NET** paquete NuGet  
  ```bash
  dotnet add package Aspose.Pdf
  ```
- Una carpeta donde tengas permiso de escritura – el tutorial guardará el archivo en `YOUR_DIRECTORY/shapes.pdf`.

Sin configuración extra, sin XML, solo C# puro.

## Crear documento PDF C# – Visión general

El primer paso es crear un objeto `Document`. Piensa en él como tu lienzo en blanco; todo lo que añadas después—páginas, texto, formas—se adjunta a esta única instancia.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Step 1: Create a new PDF document (the canvas)
using var pdfDocument = new Document();
```

> **¿Por qué `using var`?**  
> La clase `Document` implementa `IDisposable`. Envolverla en una sentencia `using` garantiza que todos los recursos no administrados (manejadores de archivo, buffers nativos) se liberen tan pronto como terminemos, lo cual es especialmente importante en servicios de larga duración.

## Añadir página al PDF

Un PDF sin páginas es como un libro sin hojas—bastante inútil. Añadir una página es una única llamada a método, pero también te devuelve un objeto `Page` que podrás manipular después.

```csharp
// Step 2: Add a fresh page to the document
var pdfPage = pdfDocument.Pages.Add();
```

> **Consejo:** La página recién añadida adopta automáticamente el tamaño predeterminado (A4). Si necesitas un tamaño personalizado, puedes establecer `pdfPage.PageInfo.Width` y `Height` antes de añadir cualquier contenido.

## Cómo dibujar un rectángulo

Ahora viene la parte divertida: dibujar un rectángulo. Aspose.Pdf usa la clase `RectangleShape`, que espera un `Rectangle` (x, y, ancho, alto) que define los límites. Las coordenadas comienzan en la esquina inferior‑izquierda de la página.

```csharp
// Step 3: Define the rectangle bounds (x, y, width, height)
// This will be validated – an exception is thrown if the rectangle is out of bounds
var rectangleBounds = new Rectangle(50, 50, 200, 150);
```

> **Caso límite:** Si `x + width` supera el ancho de la página o `y + height` supera el alto de la página, Aspose lanza una `ArgumentException`. Verifica siempre tus dimensiones, especialmente al generar PDFs para diferentes tamaños de página.

## Añadir forma al PDF

Con los límites listos, creamos la forma, le damos un trazo azul y la insertamos en la colección de párrafos de la página.

```csharp
// Step 4: Create a rectangle shape with a blue stroke and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue,   // Outline color
    // FillColor = Color.LightGray, // Uncomment to add a fill
    // LineWidth = 2                // Adjust border thickness if needed
};
pdfPage.Paragraphs.Add(rectangleShape);
```

> **¿Por qué añadirla a `Paragraphs`?**  
> En Aspose.Pdf, los elementos visuales como las formas se tratan como “párrafos” porque ocupan un área rectangular en la página. Este diseño mantiene coherente el motor de maquetación entre texto y gráficos.

## Guardar PDF en archivo

El acto final es persistir el documento. Proporciona una ruta completa y Aspose se encarga del trabajo pesado—compresión, flujos de objetos y tablas de referencias cruzadas se gestionan automáticamente.

```csharp
// Step 5: Save the PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");
```

> **Consejo profesional:** Usa `Path.Combine(Environment.CurrentDirectory, "shapes.pdf")` si deseas el archivo junto a tu ejecutable, o crea la carpeta previamente con `Directory.CreateDirectory` para evitar una `DirectoryNotFoundException`.

### Resultado esperado

Abre `shapes.pdf` con cualquier visor de PDF. Deberías ver una única página tamaño A4 con un **rectángulo con borde azul** ubicado a 50 puntos del borde izquierdo y del borde inferior, con dimensiones de 200 × 150 puntos. Sin texto, solo la forma—perfecta para marcas de agua, campos de formulario o marcadores visuales.

![PDF document with a blue rectangle created using create pdf document c#](https://example.com/images/pdf-rectangle.png "PDF document with a blue rectangle created using create pdf document c#")

*Texto alternativo:* *PDF document with a blue rectangle created using create pdf document c#.*

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar y pegar. Compila como una aplicación de consola (`dotnet new console`) y se ejecuta sin ninguna configuración adicional más allá del paquete NuGet.

```csharp
// Program.cs
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

using var pdfDocument = new Document();               // Create PDF document
var pdfPage = pdfDocument.Pages.Add();                // Add a page

// Define rectangle bounds (x, y, width, height)
// Aspose validates the rectangle – out‑of‑bounds throws an exception
var rectangleBounds = new Rectangle(50, 50, 200, 150);

// Create the rectangle shape (blue stroke) and add it to the page
var rectangleShape = new RectangleShape(rectangleBounds)
{
    StrokeColor = Color.Blue
};
pdfPage.Paragraphs.Add(rectangleShape);

// Save the document to disk
pdfDocument.Save("YOUR_DIRECTORY/shapes.pdf");

// Inform the user
Console.WriteLine("PDF created successfully at YOUR_DIRECTORY/shapes.pdf");
```

Ejecuta el programa, abre el archivo generado y verás la forma exactamente donde la definimos.

## Preguntas frecuentes y trucos

- **P:** *¿Qué pasa si necesito un rectángulo relleno?*  
  **R:** Descomenta la línea `FillColor` en el inicializador de `RectangleShape`. Aspose admite colores sólidos, degradados e incluso rellenos con imágenes.

- **P:** *¿Puedo dibujar varias formas en la misma página?*  
  **R:** Por supuesto. Simplemente crea más objetos `RectangleShape`, `Ellipse` o `Polygon` y añádelos a `pdfPage.Paragraphs`.

- **P:** *¿El sistema de coordenadas siempre es inferior‑izquierda?*  
  **R:** Sí, Aspose sigue la especificación PDF donde el origen (0,0) está en la esquina inferior‑izquierda. Si prefieres un origen superior‑izquierda, deberás calcular `y = pageHeight - desiredY`.

- **P:** *¿Qué ocurre si la carpeta de destino no existe?*  
  **R:** `pdfDocument.Save` lanzará una `DirectoryNotFoundException`. Precrea la carpeta con `Directory.CreateDirectory`.

## Próximos pasos

Ahora que sabes cómo **añadir página al PDF**, **dibujar un rectángulo**, **añadir forma al PDF** y **guardar el PDF en un archivo**, puedes ampliar esta base:

- Insertar texto, imágenes o tablas junto a las formas.  
- Usar `Graphics` para dibujo libre (líneas, arcos, rutas personalizadas).  
- Explorar encriptación de PDF o firmas digitales si la seguridad es una preocupación.  

Cada uno de esos temas se construye directamente sobre el código que acabamos de cubrir, así que siéntete seguro al experimentar.

---

**En conclusión:** Acabas de aprender el flujo completo para **crear documento PDF C#** con Aspose.Pdf—inicializar, añadir una página, dibujar una forma de rectángulo y persistir el archivo. Es un bloque de construcción sólido para facturas, informes, certificados o cualquier documento automatizado que necesites generar al vuelo. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}