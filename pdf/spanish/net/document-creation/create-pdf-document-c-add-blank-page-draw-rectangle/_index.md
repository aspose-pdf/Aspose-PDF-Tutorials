---
category: general
date: 2026-02-12
description: Crea un documento PDF en C# rápidamente añadiendo una página en blanco,
  verificando el tamaño de la página, dibujando un rectángulo y guardando el archivo.
  Guía paso a paso con Aspose.Pdf.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- save pdf file c#
- check pdf page size
language: es
og_description: Crea rápidamente un documento PDF en C# añadiendo una página en blanco,
  verificando el tamaño de la página, dibujando un rectángulo y guardando el archivo.
  Tutorial completo con código.
og_title: Crear documento PDF en C# – Añadir página en blanco y dibujar rectángulo
tags:
- PDF
- C#
- Aspose.Pdf
- Document Generation
title: Crear documento PDF en C# – Añadir página en blanco y dibujar rectángulo
url: /es/net/document-creation/create-pdf-document-c-add-blank-page-draw-rectangle/
---

none besides image.

Check for any other code blocks placeholders: CODE_BLOCK_0 to CODE_BLOCK_8. Keep them unchanged.

Now produce final content with translated text.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF C# – Añadir página en blanco y dibujar rectángulo

¿Alguna vez necesitaste **create PDF document C#** desde cero y te preguntaste cómo añadir una página en blanco, verificar las dimensiones de la página, dibujar una forma y, finalmente, guardarlo? No estás solo. Muchos desarrolladores se encuentran con este mismo obstáculo al automatizar informes, facturas o cualquier tipo de salida imprimible.

En este tutorial recorreremos un ejemplo completo y ejecutable que te muestra exactamente cómo **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, y **save PDF file C#** usando la biblioteca Aspose.Pdf. Al final tendrás un archivo PDF listo para usar con un rectángulo con borde azul situado perfectamente en una página de tamaño A4.

## Requisitos previos

- **.NET 6.0** o posterior (el código también funciona en .NET Framework 4.6+).  
- **Aspose.Pdf for .NET** instalado vía NuGet (`Install-Package Aspose.Pdf`).  
- Un conocimiento básico de la sintaxis de C#—no se requiere nada sofisticado.  
- Un IDE de tu elección (Visual Studio, Rider, VS Code, etc.).

> **Consejo profesional:** Si estás usando Visual Studio, la interfaz del Administrador de paquetes NuGet facilita la incorporación de Aspose.Pdf—simplemente busca “Aspose.Pdf” y haz clic en Instalar.

## Paso 1: Crear documento PDF C# – Inicializar el documento

Lo primero que necesitas es un objeto `Document` nuevo. Piensa en él como un lienzo en blanco donde cada operación posterior pintará su contenido.

```csharp
using Aspose.Pdf;
using System;

// Step 1: Create a new PDF document
var pdfDocument = new Document();
```

> **Por qué es importante:** La clase `Document` es el punto de entrada para cualquier operación con PDF. Instanciarla asigna las estructuras internas necesarias para gestionar páginas, recursos y metadatos.

## Paso 2: Añadir página en blanco PDF – Añadir una nueva página

Un PDF sin páginas es como un libro sin hojas—inútil. Añadir una página en blanco nos da algo sobre lo que dibujar.

```csharp
// Step 2: Add a blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Qué ocurre internamente:** `Pages.Add()` crea una página que hereda el tamaño predeterminado (A4 para la mayoría de configuraciones). Puedes cambiar sus dimensiones más adelante si necesitas un tamaño personalizado.

## Paso 3: Definir el rectángulo y comprobar el tamaño de la página PDF

Antes de dibujar, debemos definir dónde se ubicará el rectángulo y asegurarnos de que cabe dentro de la página. Aquí es donde entra en juego la palabra clave **check PDF page size**.

```csharp
// Step 3: Define rectangle position and size (fits within a standard A4 page)
var rectangle = new Rectangle(50, 50, 550, 750);

// Step 3b: Verify that the rectangle fits inside the page boundaries
bool fitsWidth = page.PageInfo.Width >= rectangle.Width;
bool fitsHeight = page.PageInfo.Height >= rectangle.Height;

if (!fitsWidth || !fitsHeight)
{
    throw new InvalidOperationException(
        $"Rectangle (W:{rectangle.Width}, H:{rectangle.Height}) exceeds page size (W:{page.PageInfo.Width}, H:{page.PageInfo.Height}).");
}
```

> **Por qué lo comprobamos:** Algunos PDFs pueden usar tamaños de página personalizados (Letter, Legal, etc.). Si el rectángulo es más grande que la página, la operación de dibujo se recorta o genera un error. Esta protección hace que el código sea robusto ante futuros cambios de tamaño de página.

## Paso 4: Dibujar rectángulo PDF – Renderizar la forma

Ahora la parte divertida: dibujar realmente un rectángulo con un borde azul y un relleno transparente. Esto demuestra la capacidad de **draw rectangle PDF**.

```csharp
// Step 4: Draw the rectangle with a blue border and a transparent fill
page.AddRectangle(
    rectangle,
    Color.Blue,          // Border color
    Color.Transparent    // Fill color (transparent)
);
```

> **Cómo funciona:** `AddRectangle` recibe tres argumentos—la geometría del rectángulo, el color del trazo (borde) y el color de relleno. Usar `Color.Transparent` garantiza que el interior permanezca vacío, permitiendo que cualquier contenido subyacente se muestre.

## Paso 5: Guardar archivo PDF C# – Persistir el documento en disco

Finalmente, escribimos el documento a un archivo. Este es el paso de **save pdf file c#** que sella el proceso.

```csharp
// Step 5: Save the PDF to a file
string outputPath = @"C:\Temp\shape.pdf"; // Adjust the path as needed
pdfDocument.Save(outputPath);
Console.WriteLine($"PDF saved successfully to {outputPath}");
```

> **Consejo:** Envuelve todo el proceso en un bloque `using` (o llama a `pdfDocument.Dispose()`) para liberar los recursos nativos rápidamente, especialmente al generar muchos PDFs en un bucle.

## Ejemplo completo y ejecutable

Juntando todas las piezas, aquí tienes el programa completo que puedes copiar y pegar en una aplicación de consola:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Create a new PDF document
        using (var pdfDocument = new Document())
        {
            // Add a blank page
            Page page = pdfDocument.Pages.Add();

            // Define rectangle (fits within a standard A4 page)
            var rectangle = new Rectangle(50, 50, 550, 750);

            // Ensure the rectangle fits inside the page boundaries
            if (page.PageInfo.Width >= rectangle.Width && page.PageInfo.Height >= rectangle.Height)
            {
                // Draw the rectangle with a blue border and a transparent fill
                page.AddRectangle(rectangle, Color.Blue, Color.Transparent);
            }
            else
            {
                Console.WriteLine("Rectangle does not fit on the page. Adjust dimensions.");
                return;
            }

            // Save the PDF to a file
            string outputPath = @"C:\Temp\shape.pdf"; // Change to your desired folder
            pdfDocument.Save(outputPath);
            Console.WriteLine($"PDF created at: {outputPath}");
        }
    }
}
```

### Resultado esperado

Abre `shape.pdf` y verás una única página de tamaño A4 con un rectángulo con borde azul ubicado a 50 pts del borde izquierdo y del inferior. El interior del rectángulo es transparente, por lo que el fondo de la página sigue visible.

![ejemplo de crear documento pdf c# mostrando rectángulo](https://example.com/placeholder.png "ejemplo de crear documento pdf c# mostrando rectángulo")

*(Texto alternativo de la imagen: **ejemplo de crear documento pdf c# mostrando rectángulo**)  

Si cambias `Color.Blue` a `Color.Red` o ajustas las coordenadas, el rectángulo reflejará esas modificaciones—siéntete libre de experimentar.

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito un tamaño de página diferente?

Puedes establecer las dimensiones de la página antes de añadir contenido:

```csharp
Page customPage = pdfDocument.Pages.Add();
customPage.SetPageSize(PageSize.Letter.Width, PageSize.Letter.Height);
```

Recuerda volver a ejecutar la lógica de **check PDF page size** después de cambiar las dimensiones.

### ¿Puedo dibujar otras formas?

Absolutamente. Aspose.Pdf ofrece objetos `AddCircle`, `AddEllipse`, `AddLine` e incluso `Path` de forma libre. El mismo patrón—definir la geometría, verificar los límites y luego llamar al método `Add*` correspondiente—se aplica.

### ¿Cómo lleno el rectángulo con un color?

Reemplaza `Color.Transparent` con cualquier color sólido:

```csharp
page.AddRectangle(rectangle, Color.Blue, Color.LightGray);
```

### ¿Hay una forma de añadir texto dentro del rectángulo?

Claro. Después de dibujar el rectángulo, añade un `TextFragment` posicionado dentro de las coordenadas del rectángulo:

```csharp
var tf = new TextFragment("Hello, world!");
tf.Rect = new Rectangle(60, 60, 540, 730); // Slightly inset
page.Paragraphs.Add(tf);
```

## Conclusión

Acabamos de mostrarte cómo **create PDF document C#**, **add blank page PDF**, **check PDF page size**, **draw rectangle PDF**, y finalmente **save PDF file C#**—todo en un ejemplo conciso de principio a fin. El código está listo para ejecutarse, las explicaciones cubren el *por qué* detrás de cada paso, y ahora tienes una base sólida para tareas de generación de PDFs más sofisticadas.

¿Listo para el próximo desafío? Prueba a superponer múltiples formas, insertar imágenes o generar tablas—todas siguen el mismo patrón que usamos aquí. Y si alguna vez necesitas ajustar las dimensiones de la página o cambiar a una biblioteca PDF diferente, los conceptos siguen siendo los mismos.

¡Feliz codificación, y que tus PDFs siempre se rendericen exactamente como deseas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}