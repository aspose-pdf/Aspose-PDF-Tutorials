---
category: general
date: 2026-03-27
description: Aprende cómo dibujar un rectángulo en PDF usando Aspose.Pdf para C#.
  Añade un rectángulo al PDF, agrega una forma al PDF y dibuja la forma en el PDF
  con ejemplos de código claros.
draft: false
keywords:
- how to draw rectangle
- add rectangle to pdf
- add shape to pdf
- draw shape on pdf
- draw rectangle in pdf
language: es
og_description: Domina cómo dibujar un rectángulo en PDF usando Aspose.Pdf. Este tutorial
  te muestra cómo agregar un rectángulo a PDF, agregar una forma a PDF y dibujar una
  forma en PDF paso a paso.
og_title: Cómo dibujar un rectángulo en PDF con C# – Guía completa
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cómo dibujar un rectángulo en PDF con C# – Guía paso a paso
url: /es/net/images-graphics/how-to-draw-rectangle-in-pdf-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo dibujar un rectángulo en PDF con C# – Guía paso a paso

¿Alguna vez te has preguntado **cómo dibujar un rectángulo** en un PDF sin tener que lidiar con la sintaxis de bajo nivel? No eres el único. Muchos desarrolladores se quedan atascados cuando necesitan visualizar un cuadro delimitador, un área resaltada o un simple elemento decorativo dentro de un documento generado. ¿La buena noticia? Con Aspose.Pdf para .NET el proceso es pan comido.

En este tutorial recorreremos todo lo que necesitas para **añadir un rectángulo a PDF**, **añadir forma a PDF**, y en última instancia **dibujar un rectángulo en PDF** usando C# limpio e idiomático. Al final tendrás un programa ejecutable que produce un archivo PDF con un rectángulo nítido, sin herramientas externas.

## Requisitos previos

- .NET 6.0 o posterior (el código funciona también con .NET Core y .NET Framework)
- Paquete NuGet Aspose.Pdf para .NET (`Install-Package Aspose.Pdf`)
- Un entorno básico de desarrollo C# (Visual Studio, VS Code, Rider, etc.)

No se necesitan otras librerías; todo lo demás lo gestiona Aspose.Pdf por sí mismo.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Primero, crea una nueva aplicación de consola y agrega el espacio de nombres Aspose.Pdf.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the rest of the code here.
        }
    }
}
```

**Por qué es importante:** Importar `Aspose.Pdf.Drawing` te da acceso a la clase de forma `Rectangle` que usaremos para **dibujar forma en PDF**. Mantener el punto de entrada ordenado facilita los pasos posteriores.

## Paso 2: Crear un nuevo documento PDF y una página

Un PDF sin páginas no tiene sentido, así que empezamos creando un objeto documento y añadiendo una única página.

```csharp
// Step 2: Initialize a new PDF document
Document pdfDoc = new Document();

// Add a blank page to the document (size defaults to A4)
Page page = pdfDoc.Pages.Add();
```

**Explicación:** La clase `Document` representa todo el archivo, mientras que `Pages.Add()` devuelve un nuevo objeto `Page` donde más adelante **añadiremos un rectángulo a PDF**. El tamaño A4 predeterminado funciona en la mayoría de los casos, pero puedes pasar ancho/alto si necesitas un lienzo personalizado.

## Paso 3: Definir la forma rectángulo

Ahora llega el núcleo de **cómo dibujar un rectángulo**: definir su posición y dimensiones.

```csharp
// Step 3: Define a rectangle shape (x, y, width, height)
// Coordinates are measured from the lower‑left corner of the page.
var rectangleShape = new Rectangle(100, 500, 300, 200)
{
    // Optional: set line color and fill color
    BorderColor = Color.Black,
    BorderWidth = 2,
    FillColor = Color.LightGray
};
```

**Por qué establecemos estas propiedades:**  
- `BorderColor` y `BorderWidth` controlan el contorno, haciendo visible el rectángulo.  
- `FillColor` le da un fondo sutil, útil cuando deseas resaltar una zona.  
- El constructor `(x, y, width, height)` te permite **dibujar un rectángulo en PDF** exactamente donde lo necesitas.

## Paso 4: Añadir el rectángulo a la página

Con la forma lista, ahora **añadimos la forma a PDF** adjuntándola a la colección `Annotations` de la página. Aspose.Pdf valida los límites automáticamente, por lo que no tienes que preocuparte por desbordamientos.

```csharp
// Step 4: Add the rectangle shape to the page
page.Annotations.Add(rectangleShape);
```

**Qué ocurre tras bambalinas:** La colección `Annotations` trata el rectángulo como un gráfico vectorial. Cuando el PDF se renderiza, la biblioteca traduce nuestras coordenadas al flujo de contenido del PDF.

## Paso 5: Guardar el documento

Finalmente, escribe el PDF en disco para que puedas abrirlo en cualquier visor.

```csharp
// Step 5: Save the PDF file
string outputPath = "RectangleDemo.pdf";
pdfDoc.Save(outputPath);
Console.WriteLine($"PDF saved to {outputPath}");
```

**Resultado:** Al abrir `RectangleDemo.pdf` se muestra un rectángulo gris claro con borde negro situado a 100 pts del borde izquierdo y 500 pts del borde inferior de la página. Esa es la solución completa para **cómo dibujar un rectángulo** en un PDF usando C#.

## Ejemplo completo y funcional

Juntando todas las piezas, aquí tienes el programa completo listo para ejecutar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Color;

namespace PdfRectangleDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize a new PDF document
            Document pdfDoc = new Document();

            // Add a blank page (A4 by default)
            Page page = pdfDoc.Pages.Add();

            // Define a rectangle shape (x, y, width, height)
            var rectangleShape = new Rectangle(100, 500, 300, 200)
            {
                BorderColor = Color.Black,
                BorderWidth = 2,
                FillColor = Color.LightGray
            };

            // Add the rectangle to the page
            page.Annotations.Add(rectangleShape);

            // Save the document
            string outputPath = "RectangleDemo.pdf";
            pdfDoc.Save(outputPath);
            Console.WriteLine($"PDF saved to {outputPath}");
        }
    }
}
```

**Salida esperada:** Un archivo llamado `RectangleDemo.pdf` que contiene una sola página con un rectángulo gris claro centrado y delineado en negro. Puedes abrirlo con Adobe Reader, Chrome o cualquier visor de PDF.

## Variaciones comunes y casos límite

### 1. Dibujar varios rectángulos

Si necesitas **añadir un rectángulo a PDF** más de una vez, simplemente crea objetos `Rectangle` adicionales y añádelos a `page.Annotations`. Recorrer una colección de coordenadas hace esto trivial.

```csharp
foreach (var rectInfo in rectangles)
{
    var rect = new Rectangle(rectInfo.X, rectInfo.Y, rectInfo.Width, rectInfo.Height)
    {
        BorderColor = Color.Blue,
        BorderWidth = 1,
        FillColor = Color.Transparent
    };
    page.Annotations.Add(rect);
}
```

### 2. Usar diferentes unidades

Aspose.Pdf trabaja en puntos (1 pt = 1/72 pulgada). Si prefieres milímetros, conviértelos primero:

```csharp
double mmToPt = 72.0 / 25.4;
float x = (float)(20 * mmToPt); // 20 mm from left
float y = (float)(150 * mmToPt);
```

### 3. Añadir un rectángulo como campo de formulario

Cuando necesitas un rectángulo interactivo (p. ej., un área clicable), usa un `LinkAnnotation` en lugar de un `Rectangle` simple. El código es similar pero agrega una URL o una acción JavaScript.

### 4. Consideraciones de compatibilidad

Aspose.Pdf versión 23.9 (lanzada a principios de 2026) soporta totalmente las API mostradas arriba. Las versiones anteriores pueden requerir `page.AddAnnotation(rectangleShape)` en lugar de `page.Annotations.Add`. Siempre revisa las notas de la versión si encuentras errores de compilación.

## Consejos profesionales y trampas comunes

- **Consejo pro:** Establece `FillColor = Color.Transparent` si solo necesitas el contorno. Esto reduce ligeramente el tamaño del archivo.  
- **Cuidado con:** Usar coordenadas que excedan las dimensiones de la página. Aspose.Pdf recortará silenciosamente la forma, lo que puede resultar confuso al depurar.  
- **Nota de rendimiento:** Añadir miles de rectángulos está bien, pero si generas informes muy extensos considera agrupar formas en un solo objeto `Graphics` para reducir la sobrecarga.

## Referencia visual

A continuación una captura de pantalla rápida del PDF generado (el rectángulo está resaltado en gris claro). El texto alternativo incluye la palabra clave principal para SEO.

![how to draw rectangle in PDF example](https://example.com/images/rectangle-demo.png "how to draw rectangle in PDF example")

## Conclusión

Hemos cubierto **cómo dibujar un rectángulo** en un PDF usando Aspose.Pdf para C#. Creando un `Document`, añadiendo una `Page`, definiendo una forma `Rectangle` y finalmente **añadiendo la forma a PDF**, puedes generar gráficos vectoriales con solo unas cuantas líneas. Ya sea que necesites **añadir un rectángulo a pdf** para resaltar, depurar diseños o superponer UI, el enfoque escala sin problemas.

A continuación, podrías explorar **dibujar forma en pdf** más allá de los rectángulos—piensa en círculos, polilíneas o incluso rutas SVG personalizadas. O sumergirte en la renderización de texto, inserción de imágenes y manipulación de formularios PDF para crear informes completos. La biblioteca Aspose.Pdf ofrece una API rica, y con los fundamentos cubiertos aquí estás listo para experimentar.

¡Feliz codificación, y que tus PDFs siempre luzcan exactamente como los imaginas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}