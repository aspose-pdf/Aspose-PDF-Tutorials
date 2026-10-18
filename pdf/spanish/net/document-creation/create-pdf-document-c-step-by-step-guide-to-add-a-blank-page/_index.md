---
category: general
date: 2026-04-10
description: Crear documento PDF en C# rápidamente. Aprende cómo añadir una página
  en blanco al PDF, dibujar un rectángulo en el PDF, agregar una forma de rectángulo
  y añadir el rectángulo al PDF con código claro.
draft: false
keywords:
- create pdf document c#
- add blank page pdf
- draw rectangle pdf
- add rectangle shape
- add rectangle to pdf
language: es
og_description: Crea documentos PDF en C# en minutos. Esta guía muestra cómo agregar
  una página PDF en blanco, dibujar un rectángulo en PDF y añadir una forma de rectángulo
  con código sencillo.
og_title: Crear documento PDF en C# – Tutorial completo
tags:
- C#
- PDF
- Aspose.PDF
- Document Generation
title: Crear documento PDF en C# – Guía paso a paso para agregar una página en blanco
  y dibujar un rectángulo
url: /es/net/document-creation/create-pdf-document-c-step-by-step-guide-to-add-a-blank-page/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF C# – Guía completa

¿Alguna vez necesitaste **crear documento PDF C#** para una función de informes pero no sabías por dónde empezar? No estás solo. En muchos proyectos el primer obstáculo es obtener un PDF con una página en blanco y luego dibujar gráficos simples como un rectángulo.  

En este tutorial resolveremos ese problema de inmediato: verás cómo añadir un PDF con página en blanco, dibujar un rectángulo en PDF y, finalmente, agregar la forma de rectángulo al archivo, todo con unas pocas líneas de C#. Al final tendrás un `shapes.pdf` listo para usar que podrás abrir en cualquier visor.

## Qué aprenderás

- Cómo inicializar un documento PDF usando Aspose.PDF for .NET.  
- Los pasos exactos para **add blank page pdf** y posicionar un rectángulo dentro de él.  
- Por qué la clase `Rectangle` es la elección correcta para dibujar formas.  
- Trampas comunes como desajustes de tamaño de página y cómo evitarlos.  

Sin herramientas externas, sin trucos—solo código C# puro que puedes copiar y pegar en una aplicación de consola.

## Requisitos previos

- .NET 6.0 o superior (el código también funciona con .NET Framework 4.6+).  
- El paquete NuGet **Aspose.PDF for .NET** (`Install-Package Aspose.PDF`).  
- Un entendimiento básico de la sintaxis de C# (variables, sentencias `using`, etc.).  

> **Consejo profesional:** Si usas Visual Studio, el Administrador de paquetes NuGet permite instalar Aspose.PDF con un solo clic.

## Paso 1: Inicializar el documento PDF

Crear un PDF comienza con un objeto `Document`. Piensa en él como el lienzo que contendrá cada página, imagen o forma que añadas después.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Drawing;

// Initialise a new PDF document – this is the core of create pdf document c#
var pdfDocument = new Document();
```

La clase `Document` te da acceso a la colección `Pages`, que es donde más adelante **add blank page pdf**.

## Paso 2: Añadir una página en blanco al documento

Un PDF sin páginas está esencialmente vacío. Añadir una página es tan simple como llamar a `pdfDocument.Pages.Add()`. La nueva página hereda el tamaño predeterminado (A4) a menos que especifiques lo contrario.

```csharp
// Add a fresh, blank page – this satisfies the add blank page pdf requirement
Page page = pdfDocument.Pages.Add();
```

> **Por qué es importante:** Añadir una página primero garantiza que cualquier comando de dibujo posterior tenga una superficie donde renderizar. Omitir este paso provocará un error en tiempo de ejecución cuando intentes dibujar un rectángulo.

## Paso 3: Definir los límites del rectángulo

Ahora **draw rectangle pdf** creando un objeto `Rectangle`. El constructor recibe las coordenadas X/Y de la esquina inferior izquierda, seguidas del ancho y la altura. En nuestro ejemplo queremos un rectángulo que encaje bien dentro de la página, dejando un pequeño margen.

```csharp
// Rectangle coordinates: (0,0) is the lower‑left corner of the page
// Width = 500, Height = 700 – fits comfortably on an A4 page
var rectangle = new Rectangle(0, 0, 500, 700);
```

Si necesitas un tamaño diferente, simplemente ajusta los valores de ancho/altura. El origen del rectángulo (0,0) se alinea con la esquina inferior izquierda de la página, lo cual es una fuente común de confusión para los recién llegados.

## Paso 4: Añadir la forma de rectángulo a la página

Con el objeto rectángulo listo, podemos **add rectangle shape** a la página. El método `AddRectangle` dibuja el contorno usando el estado gráfico actual (por defecto una línea negra delgada).

```csharp
// Add the rectangle shape – this completes the add rectangle to pdf step
page.AddRectangle(rectangle);
```

Puedes personalizar la apariencia modificando el objeto `Graphics` antes de llamar a `AddRectangle`, por ejemplo, estableciendo `LineWidth` o `Color`. Para un relleno sólido usarías `page.AddAnnotation(new SquareAnnotation(...))`, pero eso está fuera del alcance de esta guía sencilla.

## Paso 5: Guardar el archivo PDF

Finalmente, persiste el documento en disco. Elige una carpeta donde tengas permiso de escritura y dale al archivo un nombre significativo como `shapes.pdf`.

```csharp
// Save the PDF – you’ll find shapes.pdf in the specified directory
pdfDocument.Save(@"C:\Temp\shapes.pdf");
```

> **Nota:** La sentencia `using` del fragmento original no es necesaria aquí porque `Document` implementa `IDisposable`. Sin embargo, envolverlo en `using` es una buena práctica para la limpieza de recursos, especialmente en aplicaciones más grandes.

## Ejemplo completo funcional

Juntándolo todo, aquí tienes un programa de consola autocontenido que puedes ejecutar al instante:

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
            // Step 1: Create a new PDF document
            using (var pdfDocument = new Document())
            {
                // Step 2: Add a blank page to the document
                Page page = pdfDocument.Pages.Add();

                // Step 3: Define a rectangle that fits inside the page bounds (0,0 to 500,700)
                var rectangle = new Rectangle(0, 0, 500, 700);

                // Step 4: Add the rectangle shape to the page
                page.AddRectangle(rectangle);

                // Step 5: Save the PDF file
                string outputPath = @"C:\Temp\shapes.pdf";
                pdfDocument.Save(outputPath);

                Console.WriteLine($"PDF created successfully at {outputPath}");
            }
        }
    }
}
```

**Salida esperada:** Después de ejecutar el programa, abre `C:\Temp\shapes.pdf`. Verás una sola página con un rectángulo contorneado en negro posicionado en la esquina inferior izquierda, con un tamaño exacto de 500 × 700 puntos.

## Preguntas frecuentes y casos especiales

| Pregunta | Respuesta |
|----------|-----------|
| *¿Puedo cambiar el tamaño de la página antes de añadir el rectángulo?* | Sí. Crea una `Page` con dimensiones personalizadas: `var page = pdfDocument.Pages.Add(); page.PageInfo.Width = 600; page.PageInfo.Height = 800;` |
| *¿Qué pasa si necesito un rectángulo relleno?* | Usa un objeto `Graphics`: `page.Canvas.Rectangle(rectangle, Color.Blue, Color.LightBlue);` |
| *¿Aspose.PDF es gratuito?* | Ofrece una **prueba gratuita** con funcionalidad completa; se requiere una licencia comercial para uso en producción. |
| *¿Cómo añado varios rectángulos?* | Simplemente repite los pasos 3‑4 con diferentes instancias de `Rectangle` o ajusta las coordenadas. |

## Próximos pasos

Ahora que sabes cómo **create pdf document c#**, **add blank page pdf**, y **draw rectangle pdf**, podrías explorar:

- Añadir texto dentro del rectángulo (`TextFragment`, `page.Paragraphs.Add`).  
- Insertar imágenes (`page.Resources.Images.Add`) para crear informes más ricos.  
- Exportar el PDF a otros formatos como PNG o DOCX usando las APIs de conversión de Aspose.  

Todos estos temas se derivan naturalmente de la base **add rectangle to pdf** que hemos construido aquí.

---

*¡Feliz codificación!* Si encuentras algún inconveniente, no dudes en dejar un comentario abajo. Y recuerda—una vez que domines lo básico, generar PDFs complejos será pan comido.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}