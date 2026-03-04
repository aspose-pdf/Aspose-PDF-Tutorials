---
category: general
date: 2026-03-03
description: Crear documento PDF en C# con numeración Bates – aprende cómo agregar
  Bates, añadir números de página secuenciales y generar Bates en solo unos pocos
  pasos.
draft: false
keywords:
- create pdf document c#
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- how to generate bates
language: es
og_description: Crear documento PDF en C# con numeración Bates. Esta guía muestra
  cómo agregar Bates, añadir números de página secuenciales y generar Bates rápidamente.
og_title: Crear documento PDF en C# – Añadir numeración Bates
tags:
- C#
- PDF
- Bates numbering
title: Crear documento PDF en C# – Añadir numeración Bates
url: /es/net/programming-with-pdf-pages/create-pdf-document-c-add-bates-numbering/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF C# – Añadir numeración Bates

¿Alguna vez necesitaste **crear documento PDF C#** y luego etiquetar cada página con un identificador único para fines legales o de archivo? No eres el único: bufetes de abogados, tribunales e incluso grandes corporaciones preguntan constantemente, “¿Cómo añado números Bates a mis PDFs automáticamente?” La buena noticia es que con unas pocas líneas de código puedes generar un PDF, esparcir números Bates en cada página y guardar el resultado sin abrir nunca un editor.

En este tutorial recorreremos un ejemplo práctico, de extremo a extremo, que muestra **cómo añadir Bates**, cómo **añadir números de página secuenciales**, e incluso cómo **generar Bates** con prefijos personalizados. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET.

## Lo que necesitarás

- **.NET 6+** (el código también funciona en .NET Framework 4.6+).
- **Aspose.Pdf for .NET** – una biblioteca comercial que ofrece una API limpia para la manipulación de PDFs. Una evaluación gratuita funciona bien para pruebas.
- Una comprensión básica de C# (probablemente ya estés familiarizado con las sentencias `using` y los objetos).

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`. Si aún no lo has instalado, ejecuta:

```bash
dotnet add package Aspose.Pdf
```

> **Consejo profesional:** Mantén tu versión de Aspose actualizada; la última versión 23.x añade mejoras de rendimiento para documentos grandes.

## Paso 1: Abrir (o crear) el documento PDF de origen

Primero necesitamos un PDF con el que trabajar. En muchos escenarios reales ya tienes un archivo de entrada —por ejemplo, un contrato escaneado. Para el ejemplo abriremos un archivo existente llamado `input.pdf`.

```csharp
using Aspose.Pdf;

// Step 1 – Load the PDF you want to number
var pdfPath = @"C:\Docs\input.pdf";
using var pdfDocument = new Document(pdfPath);
```

> **Por qué es importante:** Abrir el documento dentro de un bloque `using` garantiza que el manejador de archivo se libere rápidamente, evitando problemas de bloqueo de archivo cuando luego intentes sobrescribir el mismo archivo.

## Paso 2: Definir tus opciones de numeración Bates

Los números Bates constan de un **prefijo** (a menudo un identificador de caso) y un **número inicial**. También puedes controlar la cantidad de dígitos, la ubicación en la página y el estilo de fuente. Aquí usaremos la palabra clave secundaria **add bates numbering pdf** configurando un objeto `BatesNumberingOptions`.

```csharp
// Step 2 – Set up Bates numbering preferences
var batesOptions = new BatesNumberingOptions
{
    // Primary keyword in action: create pdf document c# with custom settings
    Prefix = "CASE-",
    Start = 1000,
    // Optional: set zero‑padding to 6 digits (e.g., CASE-001000)
    NumberOfDigits = 6,
    // Optional: define where the number appears (bottom‑right corner)
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Bottom,
    // Optional: choose a readable font
    Font = FontRepository.FindFont("Arial")
};
```

> **Cómo añadir Bates:** Ajustando `Prefix` y `Start` controlas la cadena exacta que aparecerá en cada página. La propiedad `NumberOfDigits` garantiza un ancho constante, lo cual es útil para presentaciones legales.

## Paso 3: Aplicar la numeración Bates a cada página

Ahora llega la operación principal —añadir los números. El método `AddBatesNumbering` recorre cada página, dibuja el texto y respeta las opciones que definimos.

```csharp
// Step 3 – Apply Bates numbering to all pages
pdfDocument.AddBatesNumbering(batesOptions);
```

En su interior, Aspose renderiza el texto como un elemento *content*, lo que significa que los números se convierten en parte del PDF y no pueden desactivarse en un visor. Esto es exactamente lo que necesitas cuando deseas **añadir números de página secuenciales** que sean inmutables.

### Casos límite y variaciones

- **Múltiples prefijos:** Si necesitas diferentes prefijos por sección, crea `BatesNumberingOptions` separados y llama a `AddBatesNumbering` en un rango de páginas (`pdfDocument.Pages[1..5]`).
- **Control de relleno con ceros:** Omite `NumberOfDigits` para un número de longitud variable, o establécelo a un valor mayor para ceros iniciales.
- **Posicionamiento personalizado:** Usa `Margin` para desplazar el número desde el borde, o cambia `HorizontalAlignment` a `Center` para un estilo de pie de página.

## Paso 4: Guardar el PDF modificado

Finalmente, escribe el documento actualizado en disco. Puedes sobrescribir el original o crear un archivo completamente nuevo.

```csharp
// Step 4 – Save the PDF with Bates numbers applied
var outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
```

Después de que esta línea se ejecute, `output.pdf` contiene el contenido original más una etiqueta Bates visible en cada página —exactamente lo que esperarías al **generar Bates** para un expediente.

## Ejemplo completo y ejecutable

Juntando todo, aquí tienes el fragmento completo que puedes copiar y pegar en una aplicación de consola:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Open the source PDF
        var inputFile = @"C:\Docs\input.pdf";
        using var pdf = new Document(inputFile);

        // 2️⃣ Configure Bates numbering (add bates numbering pdf)
        var options = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            Start = 1000,
            NumberOfDigits = 6,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = FontRepository.FindFont("Arial")
        };

        // 3️⃣ Apply the numbering (how to add bates)
        pdf.AddBatesNumbering(options);

        // 4️⃣ Save the result (add sequential page numbers)
        var outputFile = @"C:\Docs\output.pdf";
        pdf.Save(outputFile);

        Console.WriteLine("Bates numbering applied successfully!");
    }
}
```

### Resultado esperado

Abre `output.pdf` en cualquier visor (Adobe Reader, Edge, etc.). Verás cada página estampada con algo como **CASE-001000**, **CASE-001001**, … hasta la última página. Los números se sitúan cómodamente en la esquina inferior derecha, coincidiendo con las opciones que configuramos.

## Preguntas frecuentes y solución de problemas

- **“¿Qué pasa si mi PDF está protegido con contraseña?”**  
  Cárgalo con la contraseña: `new Document(inputFile, new LoadOptions { Password = "secret" })`.

- **“¿Puedo añadir números Bates a un PDF recién creado?”**  
  Por supuesto. Simplemente crea el documento primero (`var doc = new Document();`) y luego sigue los Pasos 2‑4 antes de guardar.

- **“¿La fuente siempre se incrusta?”**  
  Aspose incrusta automáticamente la fuente si no está ya en el PDF. Si necesitas una familia de fuentes específica, establece `options.Font` en consecuencia.

- **“¿Qué pasa con el rendimiento en archivos de 10 000 páginas?”**  
  La biblioteca transmite las páginas, por lo que el uso de memoria se mantiene modesto. Sin embargo, podrías querer aumentar `PdfSaveOptions.CompressionMode` para una I/O más rápida.

## Consejos profesionales para uso en producción

1. **Procesamiento por lotes:** Envuelve la lógica anterior en un bucle que itere sobre una carpeta de PDFs. Usa `Directory.GetFiles("*.pdf")` y procesa cada archivo individualmente.
2. **Registro (logging):** Emite los primeros y últimos números Bates a un archivo de registro —ayuda a los auditores a verificar que la numeración fue continua.
3. **Manejo de errores:** Envuelve todo el bloque en un `try/catch` y muestra un mensaje claro si el PDF de origen falta o está corrupto.
4. **Flexibilidad de relleno con ceros:** Si necesitas un recuento de dígitos dinámico basado en el total de páginas, calcula `NumberOfDigits = (pdf.Pages.Count + options.Start).ToString().Length`.

## Conclusión

Acabamos de mostrar cómo **crear documento PDF C#** y añadir de forma fluida la **numeración Bates** —cubriendo todo desde la carga inicial hasta el guardado final. El breve ejemplo demuestra **cómo añadir Bates**, **añadir números de página secuenciales**, y **cómo generar Bates** con prefijos personalizados y relleno con ceros. Con unos pocos ajustes puedes adaptar este patrón a trabajos por lotes, diferentes diseños, o incluso integrarlo en una API web que devuelva un PDF recién numerado bajo demanda.

¿Listo para el siguiente paso? Prueba combinar esto con la función de **marca de agua** de Aspose, o genera un índice resumido que liste cada número Bates junto con una breve descripción del contenido de la página. Las posibilidades son infinitas, y el código que ahora tienes es una base sólida para cualquier flujo de trabajo de automatización de documentos.

¡Feliz codificación, y que tus PDFs siempre estén perfectamente numerados!

![Captura de pantalla de un visor de PDF mostrando crear documento pdf c# con números Bates aplicados](image-placeholder.png "crear documento pdf c# con números Bates")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}