---
category: general
date: 2026-02-12
description: Agregue números Bates a archivos PDF rápidamente. Aprenda cómo agregar
  un campo de texto PDF, un campo de formulario PDF y números de página PDF usando
  Aspose.PDF.
draft: false
keywords:
- add bates numbers
- add text field pdf
- add form field pdf
- add page numbers pdf
- how to add bates
language: es
og_description: Agregar números Bates a documentos PDF en C#. Esta guía muestra cómo
  agregar un campo de texto PDF, agregar un campo de formulario PDF y agregar números
  de página PDF con Aspose.PDF.
og_title: Agregar números Bates a PDFs – Tutorial completo de C#
tags:
- PDF
- C#
- Aspose.PDF
title: Agregar números Bates a PDFs – Guía paso a paso en C#
url: /es/net/programming-with-forms/add-bates-numbers-to-pdfs-step-by-step-c-guide/
---



{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar números Bates a PDFs – Guía completa en C#

¿Alguna vez necesitaste **agregar números bates** a un conjunto de PDFs legales pero no sabías por dónde empezar? No estás solo. En muchos despachos de abogados y proyectos de e‑discovery, estampar cada página con un identificador único es una tarea diaria, y hacerlo manualmente es una pesadilla.  

¿La buena noticia? Con unas pocas líneas de C# y Aspose.PDF puedes automatizar todo. En este tutorial recorreremos **cómo agregar números bates**, añadiremos un campo de texto en cada página y guardaremos un PDF limpio y buscable, sin sudar.

> **Lo que obtendrás:** un ejemplo de código completamente ejecutable, explicaciones de por qué cada línea es importante, consejos para casos límite y una lista de verificación rápida para verificar tu salida.  

También abordaremos tareas relacionadas como **add text field pdf**, **add form field pdf** y **add page numbers pdf**, para que tengas una caja de herramientas lista para cualquier desafío de automatización de documentos.

---

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)
- Visual Studio 2022 (o cualquier IDE que prefieras)
- Una licencia válida de Aspose.PDF para .NET (la prueba gratuita sirve para pruebas)
- Un PDF de origen llamado `source.pdf` colocado en una carpeta a la que puedas referenciar  

Si alguno de estos te resulta desconocido, simplemente detente e instala la pieza faltante antes de continuar. Los pasos a continuación asumen que ya has añadido el paquete NuGet de Aspose.PDF:

```bash
dotnet add package Aspose.Pdf
```

---

## Cómo agregar números bates a un PDF con Aspose.PDF

A continuación se muestra el programa completo, listo para copiar y pegar. Carga un PDF, crea un **campo de cuadro de texto** en cada página, escribe un número Bates formateado y, finalmente, guarda el archivo modificado.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;

class Program
{
    static void Main()
    {
        // 👉 Step 1: Load the source PDF document
        using (var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf"))
        {
            // 👉 Step 2: Add a Bates number text field to each page
            for (int pageNumber = 1; pageNumber <= pdfDocument.Pages.Count; pageNumber++)
            {
                // Define the rectangle where the field will appear (10,10) = lower‑left corner
                var fieldRect = new Rectangle(10, 10, 150, 30);

                // Create the TextBoxField – this is the “add text field pdf” part
                var batesField = new TextBoxField(pdfDocument.Pages[pageNumber], fieldRect)
                {
                    // Format the number: BATES-00001, BATES-00002, …
                    Value = $"BATES-{pageNumber:D5}"
                };

                // Register the field with the form collection – “add form field pdf”
                pdfDocument.Form.Add(batesField, $"Bates_{pageNumber}", pageNumber);
            }

            // 👉 Step 3: Save the modified PDF with Bates numbers
            pdfDocument.Save(@"YOUR_DIRECTORY\bates.pdf");
        }

        Console.WriteLine("✅ Bates numbers added successfully!");
    }
}
```

### Por qué funciona esto

- **`Document`** es el punto de entrada; representa todo el archivo PDF.  
- **`Rectangle`** define dónde vive el campo en la página. Los números están en puntos (1 pt ≈ 1/72 in). Ajusta las coordenadas si necesitas el número en una esquina diferente.  
- **`TextBoxField`** es un *form field* que puede contener cualquier cadena. Al asignar `Value` efectivamente **add page numbers pdf** con un prefijo personalizado.  
- **`pdfDocument.Form.Add`** registra el campo en el AcroForm del PDF, haciéndolo visible en visores como Adobe Acrobat.  

Si alguna vez necesitas cambiar la apariencia (fuente, color, tamaño) puedes ajustar las propiedades de `TextBoxField`; consulta la documentación de Aspose para `DefaultAppearance` y `Border`.

---

## Añadiendo un campo de texto a cada página PDF (el paso “add text field pdf”)

A veces solo deseas una etiqueta visible, no un campo de formulario interactivo. En ese caso puedes reemplazar `TextBoxField` por un `TextFragment` y añadirlo directamente a la colección `Paragraphs` de la página. Aquí tienes una alternativa rápida:

```csharp
var fragment = new TextFragment($"BATES-{pageNumber:D5}")
{
    // Position the text using a TextState (font, size, color)
    TextState = new TextState
    {
        Font = FontRepository.FindFont("Arial"),
        FontSize = 12,
        ForegroundColor = Color.Black
    }
};

// Set the fragment’s rectangle (same coordinates as before)
fragment.Position = new Position(10, 10);
pdfDocument.Pages[pageNumber].Paragraphs.Add(fragment);
```

El enfoque **add text field pdf** es útil cuando el documento final será de solo lectura, mientras que el método **add form field pdf** mantiene los números editables posteriormente.

---

## Guardando el PDF con números Bates (el momento “add page numbers pdf”)

Después de que el bucle termina, llamar a `pdfDocument.Save` escribe todo en disco. Si necesitas preservar el archivo original, simplemente cambia la ruta de salida o usa sobrecargas de `pdfDocument.Save` para transmitir el resultado directamente a una respuesta en una API web.

```csharp
// Example: stream to HTTP response (ASP.NET Core)
Response.ContentType = "application/pdf";
pdfDocument.Save(Response.Body);
```

Esa es la parte elegante: sin archivos temporales, sin bibliotecas adicionales, solo Aspose manejando el trabajo pesado.

---

## Resultado esperado y verificación rápida

Abre `bates.pdf` en cualquier visor de PDF. Deberías ver una pequeña caja en la esquina inferior izquierda de cada página que dice:

```
BATES-00001
BATES-00002
…
```

Si inspeccionas las propiedades del documento, notarás un AcroForm que contiene campos llamados `Bates_1`, `Bates_2`, etc. Eso confirma que el paso **add form field pdf** se completó con éxito.

---

## Errores comunes y consejos profesionales

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Los números aparecen descentrados | Las coordenadas del Rectangle son relativas a la esquina inferior izquierda de la página. | Invierte el valor Y (`pageHeight - marginTop`) o usa `page.PageInfo.Height` para calcular una posición con margen superior. |
| Los campos son invisibles en Adobe Reader | El borde predeterminado está configurado como “No”. | Establece `batesField.Border = new Border { Width = 0.5f, Color = Color.Black };` |
| Los PDFs grandes generan presión de memoria | `using` elimina el documento solo después de que el bucle termina. | Procesa las páginas en bloques o usa `pdfDocument.Save` con `SaveOptions` que habilitan streaming. |
| La licencia no se aplica | Aspose imprime una marca de agua en la primera página. | Registra tu licencia temprano: `License lic = new License(); lic.SetLicense("Aspose.Pdf.lic");` |

---

## Extender la solución

- **Prefijos personalizados:** Reemplaza `"BATES-"` por cualquier cadena (`"DOC-"`, `"CASE-"`, …).  
- **Longitud de relleno con ceros:** Cambia `{pageNumber:D5}` a `{pageNumber:D3}` para tres dígitos.  
- **Posicionamiento dinámico:** Usa `pdfDocument.Pages[pageNumber].PageInfo.Width` para colocar el campo en el lado derecho.  
- **Numeración condicional:** Omite páginas en blanco verificando `pdfDocument.Pages[pageNumber].IsBlank`.  

Todas estas variaciones mantienen intacto el patrón central de **add bates numbers**, **add text field pdf** y **add form field pdf**.

---

## Ejemplo completo (Todo en uno)

A continuación se muestra el programa final, listo para ejecutar, que incorpora los consejos anteriores. Cópialo en una nueva aplicación de consola y pulsa F5.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;

class AddBatesNumbers
{
    static void Main()
    {
        // Register your license here (optional for trial)
        // var license = new License();
        // license.SetLicense("Aspose.Pdf.lic");

        string inputPath = @"YOUR_DIRECTORY\source.pdf";
        string outputPath = @"YOUR_DIRECTORY\bates.pdf";

        using (var pdfDocument = new Document(inputPath))
        {
            int totalPages = pdfDocument.Pages.Count;

            for (int i = 1; i <= totalPages; i++)
            {
                // Position the field 10 pts from left and 10 pts from bottom
                var rect = new Rectangle(10, 10, 150, 30);

                var batesField = new TextBoxField(pdfDocument.Pages[i], rect)
                {
                    Value = $"BATES-{i:D5}"
                };

                // Optional: make the field look nicer
                batesField.Border = new Border
                {
                    Width = 0.5f,
                    Color = Color.Gray
                };
                batesField.DefaultAppearance = new DefaultAppearance
                {
                    Font = FontRepository.FindFont("Arial"),
                    FontSize = 10,
                    ForegroundColor = Color.DarkBlue
                };

                pdfDocument.Form.Add(batesField, $"Bates_{i}", i);
            }

            pdfDocument.Save(outputPath);
        }

        Console.WriteLine($"✅ Finished! Bates numbers saved to: {outputPath}");
    }
}
```

Ejecuta el programa, abre el resultado y verás un identificador de aspecto profesional en cada página, exactamente lo que un especialista en soporte de litigios esperaría.

---

## Conclusión

Acabamos de demostrar **cómo agregar números bates** a cualquier PDF usando C# y Aspose.PDF. Al crear un **campo de cuadro de texto** en cada página, simultáneamente **add text field pdf**, **add form field pdf** y **add page numbers pdf** en una sola pasada. El enfoque es rápido, escalable y fácil de ajustar para prefijos personalizados, diferentes diseños o lógica condicional.

¿Listo para el próximo desafío? Intenta incrustar un código QR que enlace al archivo original del caso, o genera una página de índice separada que enumere todos los números Bates con sus títulos de página correspondientes. La misma API te permite combinar PDFs, extraer páginas e incluso redactar datos sensibles, así que el cielo es el límite.

Si encuentras algún problema, deja un comentario abajo o consulta la documentación oficial de Aspose para profundizar. ¡Feliz codificación, y que tus PDFs siempre estén perfectamente numerados!  

---  

![add bates numbers screenshot](https://example.com/images/add-bates-numbers.png "add bates numbers example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}