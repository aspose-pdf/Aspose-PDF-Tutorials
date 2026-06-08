---
category: general
date: 2026-01-02
description: Añade números de página a PDF rápidamente usando Aspose.Pdf en C#. Aprende
  a agregar numeración Bates, texto de pie de página, marca de agua personalizada
  y a recorrer las páginas del PDF en un solo script.
draft: false
keywords:
- add page numbers pdf
- add bates numbering
- add footer text
- add custom watermark
- loop through pdf pages
language: es
og_description: Añade números de página a PDF al instante con Aspose.Pdf. Esta guía
  también cubre la incorporación de numeración Bates, texto de pie de página, marca
  de agua personalizada y el recorrido de las páginas del PDF.
og_title: Agregar números de página a PDF con C# – Tutorial completo de programación
tags:
- C#
- Aspose.Pdf
- PDF manipulation
title: Agregar números de página a PDF con C# – Guía completa paso a paso
url: /es/net/programming-with-pdf-pages/add-page-numbers-pdf-with-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir números de página pdf con C# – Tutorial de programación completo

¿Alguna vez necesitaste **añadir números de página pdf** a archivos pero no sabías por dónde empezar? No eres el único—los desarrolladores preguntan constantemente cómo estampar números, pies de página o incluso un identificador al estilo Bates en cada página de un PDF.  

En este tutorial verás un ejemplo listo‑para‑ejecutar en C# que **recorre páginas pdf**, estampa un pie de página con número de página y (si lo deseas) añade una marca de agua personalizada. También te mostraremos cómo cambiar el sello a un número Bates, que es simplemente una forma elegante de decir “añadir numeración Bates” para documentos legales o forenses. Al final, tendrás un único método reutilizable que maneja todas estas tareas sin sudar.

## Añadir números de página pdf – Visión general

Antes de sumergirnos en el código, aclaremos qué significa realmente “añadir números de página pdf” en el mundo de Aspose.Pdf. La biblioteca trata cualquier fragmento de texto que coloques en una página como un **TextStamp**. Al crear un sello con un marcador de posición de página (`{page}`) y aplicarlo a cada página, obtienes automáticamente una numeración secuencial. El mismo sello puede llevar texto adicional, de modo que puedes **añadir texto de pie de página** como “Confidencial” o un identificador específico del caso.

> **¿Por qué usar un sello en lugar de editar el flujo de contenido del PDF?**  
> Los sellos son objetos de alto nivel que respetan los márgenes de la página, la rotación y los gráficos existentes. Además, son mucho más fáciles de mantener—solo cambia unas pocas propiedades y vuelve a ejecutar el script.

## Recorrer páginas PDF para aplicar sellos

El primer paso práctico es abrir el PDF de origen e iterar sobre sus páginas. Este es el patrón clásico de **recorrer páginas pdf** que la mayoría de los ejemplos de Aspose utilizan.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Paths – change these to match your environment
string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // The loop – every Page object lives in pdfDocument.Pages
    foreach (Page page in pdfDocument.Pages)
    {
        // We'll attach a stamp later (see next section)
    }

    // Save the modified document
    pdfDocument.Save(outputPdfPath);
}
```

> **Consejo profesional:** Si tu PDF es enorme (cientos de páginas), considera procesarlo en lotes para mantener bajo el uso de memoria. Aspose.Pdf transmite páginas de forma perezosa, por lo que el bucle ya es bastante eficiente.

## Añadir numeración Bates y texto de pie de página

Ahora que podemos caminar por cada página, creemos un **TextStamp reutilizable** que lleve tanto el número de página como el texto de pie de página opcional. El marcador `{page}` se reemplaza automáticamente por el índice de página actual.

```csharp
// Create a stamp that will be reused for every page
var batesStamp = new TextStamp("Bates-{page} – Confidential")
{
    // Position the stamp 20 points from the left and bottom edges
    XIndent = 20,
    YIndent = 20,
    // Align left‑bottom so it behaves like a traditional footer
    HorizontalAlignment = HorizontalAlignment.Left,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Font styling – Times New Roman, 10pt, bold, gray
    Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Gray }
};

// Attach the stamp to every page
foreach (Page page in pdfDocument.Pages)
    page.AddStamp(batesStamp);
```

### Por qué funciona esto

* **`Bates-{page}`** – Aspose sustituye `{page}` por el número de página real, dándote automáticamente un número Bates clásico.  
* **`Confidential`** – Esta es la parte de **añadir texto de pie de página**. Puedes reemplazarla por cualquier cadena, incluso obtener datos de una base de datos.  
* **Estilizado** – Usar `TextState` te permite ajustar color, opacidad e incluso rotación sin tocar los flujos internos del PDF.

Si solo necesitas números simples, elimina el prefijo “Bates‑” y el texto adicional:

```csharp
var simpleStamp = new TextStamp("{page}")
{
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    Font = new Font(FontFamily.Helvetica, 12, FontStyle.Regular),
    TextState = { ForegroundColor = Color.Black }
};
```

## Añadir una marca de agua personalizada (opcional)

A veces quieres más que un pie de página—necesitas un logo semitransparente o una superposición “BORRADOR” en toda la página. Ahí es donde entra **añadir marca de agua personalizada**. La misma clase `TextStamp` puede reutilizarse, solo cambia su alineación y opacidad.

```csharp
var watermark = new TextStamp("DRAFT")
{
    // Center it both horizontally and vertically
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Center,
    // Make it big and light
    Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
    TextState = { ForegroundColor = Color.Red, FontSize = 72, FontStyle = FontStyle.Bold, 
                  Transparency = 0.5f }   // 50% transparent
};

// Apply the watermark on top of the page‑number stamp
foreach (Page page in pdfDocument.Pages)
{
    page.AddStamp(watermark);   // watermark on top
    page.AddStamp(batesStamp);  // then the footer
}
```

> **Nota:** El orden importa. Añadir la marca de agua primero garantiza que los números de página permanezcan legibles sobre el texto semitransparente.

## Guardar el PDF y verificar resultados

Después de estampar, el paso final es escribir los cambios de vuelta al disco. La llamada `Save` que colocamos antes hace el trabajo pesado, pero añadamos un fragmento rápido de verificación que abra el nuevo archivo e imprima cuántas páginas fueron procesadas.

```csharp
pdfDocument.Save(outputPdfPath);

// Quick verification
using (var resultDoc = new Document(outputPdfPath))
{
    Console.WriteLine($"✅ Successfully added page numbers to {resultDoc.Pages.Count} pages.");
}
```

Cuando ejecutes el programa completo, deberías ver un PDF donde cada página termina con algo como **“Bates‑3 – Confidential”** (o simplemente “3” si usaste el sello simple) y, si activaste la marca de agua, un tenue “BORRADOR” en el centro.

### Salida esperada

| Página | Pie de página (ejemplo) |
|--------|--------------------------|
| 1      | Bates‑1 – Confidential |
| 2      | Bates‑2 – Confidential |
| …      | … |
| N      | Bates‑N – Confidential |

Si abres el archivo en un visor, los números estarán a 20 pts de los márgenes izquierdo e inferior, coincidiendo con las convenciones típicas de documentos legales.

## Ejemplo completo funcional (listo para copiar y pegar)

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

string sourcePdfPath = @"C:\Docs\input.pdf";
string outputPdfPath = @"C:\Docs\PageNumbered.pdf";

using (var pdfDocument = new Document(sourcePdfPath))
{
    // ---------- Create the page‑number/footer stamp ----------
    var batesStamp = new TextStamp("Bates-{page} – Confidential")
    {
        XIndent = 20,
        YIndent = 20,
        HorizontalAlignment = HorizontalAlignment.Left,
        VerticalAlignment   = VerticalAlignment.Bottom,
        Font = new Font(FontFamily.TimesRoman, 10, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Gray }
    };

    // ---------- Optional watermark ----------
    var watermark = new TextStamp("DRAFT")
    {
        HorizontalAlignment = HorizontalAlignment.Center,
        VerticalAlignment   = VerticalAlignment.Center,
        Font = new Font(FontFamily.Helvetica, 72, FontStyle.Bold),
        TextState = { ForegroundColor = Color.Red, Transparency = 0.5f }
    };

    // ---------- Apply stamps to every page ----------
    foreach (Page page in pdfDocument.Pages)
    {
        page.AddStamp(watermark);   // comment out if you don't need a watermark
        page.AddStamp(batesStamp);
    }

    // ---------- Save and verify ----------
    pdfDocument.Save(outputPdfPath);
    Console.WriteLine($"✅ Added page numbers and watermark to {pdfDocument.Pages.Count} pages.");
}
```

Guarda esto como `AddPageNumbers.cs`, restaura el paquete NuGet Aspose.Pdf (`Install-Package Aspose.Pdf`) y ejecútalo. Obtendrás un archivo **añadir números de página pdf** que también demuestra **añadir numeración Bates**, **añadir texto de pie de página**, **añadir marca de agua personalizada**, y el clásico patrón de **recorrer páginas pdf**, todo en un script ordenado.

![añadir números de página pdf ejemplo](https://example.com/images/add-page-numbers-pdf.png "Captura de pantalla que muestra páginas PDF numeradas con pie de página y marca de agua")

## Conclusión

Hemos cubierto todo lo que necesitas para **añadir números de página pdf** usando Aspose.Pdf en C#. Desde recorrer cada página, estampar números Bates, añadir texto de pie de página personalizado y hasta superponer una marca de agua semitransparente, el código es lo suficientemente compacto como para insertarlo en cualquier proyecto existente.  

A continuación, podrías explorar escenarios más avanzados—como obtener el texto del pie de página de una base de datos, aplicar fuentes diferentes por sección, o generar un PDF índice separado que liste todos los números Bates. Todas esas extensiones se basan en las mismas ideas centrales que hemos mostrado aquí, por lo que estás bien posicionado para ampliar la solución a medida que crezcan tus requerimientos.  

Pruébalo, ajusta el estilo y cuéntanos en los comentarios cómo te funcionó. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}