---
category: general
date: 2026-03-06
description: Crea un documento PDF en C# y agrega números de Bates fácilmente. Aprende
  cómo añadir una página en blanco al PDF, colocar un sello en la página e implementar
  la numeración Bates.
draft: false
keywords:
- create pdf document
- add bates number
- add blank page pdf
- how to add bates numbering
- place stamp on page
language: es
og_description: Crear documento PDF en C# y agregar número de Bates. Esta guía muestra
  cómo añadir una página en blanco al PDF, colocar un sello en la página y aplicar
  numeración de Bates.
og_title: Crear documento PDF con numeración Bates – Tutorial de C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Crear documento PDF con numeración Bates en C# – Guía completa
url: /es/net/programming-with-stamps-and-watermarks/create-pdf-document-with-bates-numbering-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF con numeración Bates en C#

¿Alguna vez necesitaste **crear un documento PDF** en C# y te preguntaste cómo añadir un número Bates sin volverte loco? No eres el único: despachos de abogados, tribunales e incluso algunos equipos de cumplimiento corporativo se enfrentan a este mismo reto a diario. ¿La buena noticia? Con unas pocas líneas de código de Aspose.Pdf puedes generar un PDF nuevo, añadir una página en blanco y estampar un número Bates correcto en un flujo continuo.

En este tutorial recorreremos todo el proceso: desde la configuración del proyecto, pasando por la adición de una página en blanco al PDF, hasta descubrir **cómo añadir numeración Bates**, y finalmente **colocar el sello en la página** y guardar el resultado. Al final tendrás un fragmento listo para usar que podrás insertar en cualquier aplicación .NET. Sin referencias vagas, solo un ejemplo completo y ejecutable.

## Lo que necesitarás

- **.NET 6+** (o .NET Framework 4.6+ – Aspose.Pdf funciona con ambos)
- **Aspose.Pdf for .NET** paquete NuGet (`Install-Package Aspose.Pdf`)
- Un IDE decente (Visual Studio, Rider o VS Code con la extensión C#)

Eso es todo. Sin DLLs extra, sin servicios externos. Vamos al grano.

## Paso 1: Crear documento PDF – Configuración inicial

Lo primero es obtener un objeto `Document` nuevo. Piensa en él como el lienzo vacío donde vivirá todo lo demás.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Initialize a new PDF document
Document pdfDocument = new Document();
```

> **Por qué importa:** La clase `Document` es el punto de entrada para cada operación de Aspose. Instanciarla te da acceso a la colección `Pages`, a los metadatos y a la configuración de seguridad, todos los bloques de construcción para un PDF profesional.

## Paso 2: Añadir página en blanco al PDF

Un PDF sin páginas es como un libro sin hojas: bastante inútil. Añadir una página en blanco es sencillo y nos brinda una superficie donde estampar el número Bates.

```csharp
// Add a single blank page to the document
Page page = pdfDocument.Pages.Add();
```

> **Consejo profesional:** Si necesitas varias páginas, simplemente llama a `pdfDocument.Pages.Add()` dentro de un bucle. Cada llamada devuelve un objeto `Page` nuevo que puedes personalizar de forma independiente.

## Paso 3: Cómo añadir numeración Bates – Crear el TextStamp

Ahora llega la parte esencial: el **número Bates**. En Aspose.Pdf es simplemente un `TextStamp` con una bandera de artefacto especial.

```csharp
// Create a text stamp that will serve as a Bates number
TextStamp batesStamp = new TextStamp("Bates-001")
{
    // Mark the stamp as a Bates‑numbering artifact (helps PDF viewers treat it specially)
    Artifact = ArtifactType.BatesNumbering,
    // Align the stamp to the bottom‑right corner of the page
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Add a small margin so the number isn’t glued to the edge
    Margin = new Margin { Bottom = 10, Right = 10 }
};
```

> **Por qué establecemos `Artifact`:** Algunos lectores de PDF exponen los números Bates como metadatos buscables. Marcar el sello como artefacto `BatesNumbering` garantiza que las herramientas posteriores lo reconozcan automáticamente.

## Paso 4: Colocar el sello en la página

Con el sello listo, ahora **colocamos el sello en la página**. Este es el paso donde el número visual aparece realmente en el PDF.

```csharp
// Add the Bates number stamp to the previously created page
page.AddStamp(batesStamp);
```

> **Caso límite:** Si necesitas que el número se incremente en cada página, deberías iterar sobre `pdfDocument.Pages` y actualizar `batesStamp.Value` antes de llamar a `AddStamp`. El ejemplo aquí se mantiene simple con un “Bates‑001” estático.

## Paso 5: Guardar y verificar el resultado

Finalmente, persistimos el PDF en disco. Elige una carpeta donde tengas permisos de escritura; de lo contrario, obtendrás una `UnauthorizedAccessException`.

```csharp
// Save the stamped PDF to a file
pdfDocument.Save("YOUR_DIRECTORY/BatesStamped.pdf");
```

Al abrir `BatesStamped.pdf` en cualquier visor deberías ver un pequeño “Bates‑001” ubicado discretamente en la esquina inferior derecha de la página en blanco.

> **Salida esperada:**  
> ![PDF con sello de número Bates](image-placeholder.png "PDF con sello de número Bates")  
> *Texto alternativo: PDF con sello de número Bates en la esquina inferior‑derecha.*

Si el número no aparece, verifica los valores de margen y asegúrate de que el tamaño de página no sea demasiado pequeño (el A4 predeterminado funciona bien). También confirma que la bandera `Artifact` no esté siendo eliminada por herramientas de post‑procesamiento.

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar y pegar. Incluye todas las directivas `using` y comentarios para que no te pierdas.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize a new PDF document
        Document pdfDocument = new Document();

        // 2️⃣ Add a blank page – this is where we’ll put the Bates number
        Page page = pdfDocument.Pages.Add();

        // 3️⃣ Create a TextStamp for the Bates number
        TextStamp batesStamp = new TextStamp("Bates-001")
        {
            Artifact = ArtifactType.BatesNumbering,          // Marks it as a Bates‑numbering artifact
            HorizontalAlignment = HorizontalAlignment.Right, // Align right
            VerticalAlignment = VerticalAlignment.Bottom,    // Align bottom
            Margin = new Margin { Bottom = 10, Right = 10 }  // Small margin from edges
        };

        // 4️⃣ Place the stamp on the page
        page.AddStamp(batesStamp);

        // 5️⃣ Save the PDF to disk
        string outputPath = @"C:\Temp\BatesStamped.pdf";
        pdfDocument.Save(outputPath);

        Console.WriteLine($"PDF created successfully: {outputPath}");
    }
}
```

Ejecuta el programa, abre el PDF y verás el número Bates exactamente donde le indicamos. 🎉

## Variaciones comunes y trampas

| Escenario | Qué cambiar | Por qué |
|----------|----------------|-----|
| **Múltiples páginas, números incrementales** | Recorrer `pdfDocument.Pages`, establecer `batesStamp.Value = $"Bates-{i:D3}"` antes de `AddStamp` | Asigna a cada página un identificador único, típico en paquetes legales |
| **Ubicación diferente (arriba‑izquierda)** | Cambiar `HorizontalAlignment = HorizontalAlignment.Left` y `VerticalAlignment = VerticalAlignment.Top` | Algunas organizaciones prefieren el número en el encabezado en lugar del pie de página |
| **Fuente o color personalizados** | Establecer `batesStamp.TextState.Font = FontRepository.FindFont("Arial"); batesStamp.TextState.FontSize = 12; batesStamp.TextState.ForegroundColor = Color.Red;` | Mejora la legibilidad o cumple con directrices de marca |
| **Añadir un PDF existente como fondo** | Cargar el PDF origen con `Document src = new Document("source.pdf"); pdfDocument.Pages.Add(src.Pages[1]);` | Útil cuando necesitas estampar sobre un formulario ya generado |

## Conclusión

Acabamos de mostrar cómo **crear documento PDF**, **añadir página en blanco al PDF** y **añadir número Bates** usando Aspose.Pdf para .NET, luego **colocar el sello en la página** y guardar el archivo. El código está deliberadamente compacto para que puedas adaptarlo a flujos de trabajo más amplios, ya sea procesando docenas de archivos o integrándolo en un servicio web.

Si estás listo para llevar esto más lejos, considera:

- Automatizar la lógica de incremento para archivos de casos extensos.
- Incrustar la generación de PDF en una API ASP.NET Core.
- Añadir seguridad (protección con contraseña) mediante `pdfDocument.Encrypt(...)`.

Siéntete libre de experimentar, romper cosas y hacer preguntas en los comentarios. ¡Feliz codificación, y que tus PDFs siempre estén perfectamente sellados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}