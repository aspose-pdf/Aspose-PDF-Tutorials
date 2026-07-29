---
category: general
date: 2026-07-03
description: Tutorial de numeración Bates que muestra cómo agregar numeración Bates
  a archivos PDF usando Aspose.PDF. Incluye configuración del prefijo del número Bates
  y un ejemplo completo de numeración Bates.
draft: false
keywords:
- bates numbering tutorial
- add bates numbering pdf
- bates numbering example
- prefix bates number
language: es
og_description: Tutorial de numeración Bates que le guía paso a paso para agregar
  numeración Bates a archivos PDF, establecer un prefijo de número Bates y ofrecer
  un ejemplo completo y funcional.
og_title: 'Tutorial de numeración Bates: Añadir números a PDF con Aspose'
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  headline: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  type: TechArticle
- description: Bates numbering tutorial showing how to add bates numbering pdf files
    using Aspose.PDF. Includes prefix bates number setup and a complete bates numbering
    example.
  name: 'Bates Numbering Tutorial: Add Numbers to PDF with Aspose'
  steps:
  - name: What if I need to reset the counter for each section?
    text: You can call `pdfDocument.BatesNumbering.Reset()` before processing a new
      range of pages. Combine it with a loop over `pdfDocument.Pages` and set `Start`
      again for each section.
  - name: How do I apply different prefixes to different page ranges?
    text: 'Create multiple `BatesNumbering` objects—one per range—by cloning the document
      or by using the `Add` method (available in newer Aspose versions). Here’s a
      quick sketch:'
  - name: Does the library support Unicode prefixes?
    text: Absolutely. Pass any Unicode string (e.g., `"案件‑"`). Aspose.PDF handles
      right‑to‑left scripts and special symbols without extra configuration.
  - name: What about PDF security—will Bates numbering break encryption?
    text: If the source PDF is encrypted, you must provide the password before accessing
      `BatesNumbering`. The numbering process respects the original encryption settings—your
      output will stay encrypted unless you explicitly change it.
  type: HowTo
tags:
- Aspose.PDF
- PDF processing
- Bates numbering
title: 'Tutorial de numeración Bates: Añadir números a PDF con Aspose'
url: /es/net/programming-with-stamps-and-watermarks/bates-numbering-tutorial-add-numbers-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial de Numeración Bates – Añadiendo Números Bates a PDFs con Aspose

¿Alguna vez necesitaste un **bates numbering tutorial** porque tenías que etiquetar miles de páginas para un litigio? No estás solo. En muchos flujos de trabajo legales y de cumplimiento, una forma fiable de *add bates numbering pdf* archivos es un requisito innegociable. Afortunadamente, Aspose.PDF hace que todo el proceso sea pan comido, y en esta guía recorreremos un **bates numbering example** completo que puedes incorporar directamente en tu proyecto.

> **Lo que obtendrás:** un fragmento de código ejecutable que establece el número inicial, aplica un **prefix bates number**, y guarda el resultado — todo en menos de 30 líneas de C#.

## Prerequisites

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior (la API funciona igual en .NET Framework 4.6+)
- Una licencia válida de Aspose.PDF for .NET (o puedes usar el modo de evaluación gratuito)
- Un PDF de entrada llamado `input.pdf` ubicado en una carpeta que controles
- Visual Studio 2022 o cualquier editor que entienda proyectos C#

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf`.

## Step 1: Install Aspose.PDF for .NET

Abre tu terminal (o la Consola del Administrador de paquetes) y ejecuta:

```bash
dotnet add package Aspose.Pdf
```

O, si prefieres la interfaz gráfica, haz clic derecho en **Dependencies → Manage NuGet Packages**, busca *Aspose.Pdf* y pulsa **Install**. Esto descarga la última versión estable (a julio 2026, versión 23.12).

## Step 2: Open the Source PDF Document

La primera línea de cualquier flujo de trabajo *add bates numbering pdf* es cargar el archivo que deseas marcar. Envolvemos la operación en un bloque `using` para que el documento se libere automáticamente.

```csharp
using Aspose.Pdf;

// Step 2: Load the PDF you want to number
using (var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf"))
{
    // Subsequent steps go here...
}
```

> **Pro tip:** Si tu PDF está en un bucket en la nube, puedes proporcionar un `Stream` en lugar de una ruta de archivo — Aspose.PDF maneja ambos sin problemas.

## Step 3: Set the Starting Number and Prefix

Ahora llega el corazón del **bates numbering example**: indicar a Aspose dónde comenzar y qué texto debe preceder a cada número. La propiedad `BatesNumbering` expone tanto `Start` como `Prefix`.

```csharp
    // Step 3a: Define where the numbering begins
    pdfDocument.BatesNumbering.Start = 1000;   // you can start anywhere

    // Step 3b: Add a custom prefix – this is the prefix bates number you asked for
    pdfDocument.BatesNumbering.Prefix = "ABC-";
```

¿Por qué usar un prefijo? En muchos casos legales el prefijo identifica el expediente, el departamento o el lote de producción. Usando `"ABC-"` como marcador de posición, podrías cambiarlo a `"CASE42-"` o cualquier cadena que se ajuste a tu convención de nombres.

## Step 4: Choose Where the Numbers Appear (Optional)

Aspose coloca por defecto el número en la esquina inferior derecha, pero puedes moverlo a cualquier parte ajustando la propiedad `Location`. Este paso no es obligatorio para una operación básica *add bates numbering pdf*, pero es útil conocerlo.

```csharp
    // Optional: Move the number to the top‑left corner
    pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);
```

`Location` recibe coordenadas X e Y medidas en puntos (1 pt ≈ 1/72 in). Ajusta según necesites para el diseño de tu página.

## Step 5: Save the Updated PDF

Finalmente, persiste los cambios. El método `Save` de `BatesNumbering` escribe un nuevo archivo manteniendo el original intacto.

```csharp
    // Step 5: Write the output file with numbering applied
    pdfDocument.BatesNumbering.Save("YOUR_DIRECTORY/output.pdf");
}
```

Al abrir `output.pdf`, cada página mostrará algo como `ABC-1000`, `ABC-1001`, … hasta la última página.

## Full Working Example

Juntándolo todo, aquí tienes el **bates numbering example** que puedes copiar‑pegar en el método `Main` de una aplicación de consola:

```csharp
using System;
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // Path configuration – adjust to your environment
        string inputPath = @"YOUR_DIRECTORY\input.pdf";
        string outputPath = @"YOUR_DIRECTORY\output.pdf";

        // Load the PDF
        using (var pdfDocument = new Document(inputPath))
        {
            // Set start number and prefix
            pdfDocument.BatesNumbering.Start = 1000;
            pdfDocument.BatesNumbering.Prefix = "ABC-";

            // (Optional) Change location – comment out if default is fine
            // pdfDocument.BatesNumbering.Location = new Location(10, pdfDocument.Pages[1].PageInfo.Height - 30);

            // Save the numbered PDF
            pdfDocument.BatesNumbering.Save(outputPath);
        }

        Console.WriteLine($"Bates numbering applied! Check: {outputPath}");
    }
}
```

**Salida esperada** (en la consola):

```
Bates numbering applied! Check: YOUR_DIRECTORY\output.pdf
```

Abre el PDF generado y verás números secuenciales con el prefijo `ABC-` comenzando en `1000`.

## Common Questions & Edge Cases

### What if I need to reset the counter for each section?

Puedes llamar a `pdfDocument.BatesNumbering.Reset()` antes de procesar un nuevo rango de páginas. Combínalo con un bucle sobre `pdfDocument.Pages` y vuelve a establecer `Start` para cada sección.

### How do I apply different prefixes to different page ranges?

Crea varios objetos `BatesNumbering` —uno por rango— clonando el documento o usando el método `Add` (disponible en versiones más recientes de Aspose). Aquí tienes un bosquejo rápido:

```csharp
// Number first 10 pages with "PRE‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "PRE-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(1, 10));

// Number the rest with "POST‑"
pdfDocument.BatesNumbering.Start = 1;
pdfDocument.BatesNumbering.Prefix = "POST-";
pdfDocument.BatesNumbering.Save(outputPath, new PageRange(11, pdfDocument.Pages.Count));
```

### Does the library support Unicode prefixes?

Absolutamente. Pasa cualquier cadena Unicode (p. ej., `"案件‑"`). Aspose.PDF maneja scripts de derecha a izquierda y símbolos especiales sin configuración adicional.

### What about PDF security—will Bates numbering break encryption?

Si el PDF de origen está encriptado, debes proporcionar la contraseña antes de acceder a `BatesNumbering`. El proceso de numeración respeta la configuración de cifrado original — tu salida permanecerá encriptada a menos que la cambies explícitamente.

```csharp
pdfDocument.Encrypt(new DocumentEncryption("ownerPwd", "userPwd"));
```

## Tips & Best Practices

- **Batch processing:** Envuelve toda la rutina en un bucle `foreach` para manejar decenas de archivos automáticamente.
- **Logging:** Registra el número inicial, el prefijo y la ruta de salida en un archivo de log; esto facilita las auditorías para los equipos legales.
- **Performance:** Para PDFs muy grandes (500 + páginas), considera habilitar **memory optimization** mediante `pdfDocument.OptimizeMemory = true;`.
- **Testing:** Siempre conserva una copia del PDF original; la numeración Bates es irreversible una vez guardada.

## Conclusion

En este **bates numbering tutorial** hemos cubierto todo lo que necesitas para **add bates numbering pdf** archivos con Aspose.PDF:

1. Instala la biblioteca.
2. Carga tu documento de origen.
3. Establece el número inicial y un **prefix bates number**.
4. (Opcional) ajusta la ubicación.
5. Guarda el resultado.

Ahora dispones de un sólido **bates numbering example** que puedes adaptar a cualquier flujo de trabajo legal, archivístico o de cumplimiento. ¿Quieres ir más allá? Prueba combinar los números Bates con marcas de agua, o genera un manifiesto CSV que asocie cada página con su identificador. El cielo es el límite, y Aspose te brinda las herramientas para llegar allí.

---

*¿Listo para poner esto en producción? Deja un comentario si encuentras algún inconveniente, ¡y feliz codificación!*

## What Should You Learn Next?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Apply Numbering Style in Heading of PDF using Java](/pdf/english/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)
- [Aspose Pdf Net Floatingbox Page Numbering](/pdf/german/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)
- [Apply Numbering Style In Heading Of Pdf Using Java](/pdf/german/java/pdf-images/apply-numbering-style-in-heading-of-pdf-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}