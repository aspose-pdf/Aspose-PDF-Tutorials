---
category: general
date: 2026-10-07
description: Aprende cómo agregar numeración Bates a un PDF usando C#. Esta guía paso
  a paso también cubre la numeración de páginas de PDF y otros trucos de numeración.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add bates numbering
- pdf page numbering
- number pdf pages
- how to add bates
- bates numbering pdf
language: es
lastmod: 2026-10-07
og_description: Añade numeración Bates a un PDF rápidamente. Sigue este tutorial para
  dominar la numeración de páginas PDF, numerar páginas PDF y automatizar el seguimiento
  de documentos.
og_image_alt: Screenshot of a PDF with Bates numbers added using Aspose.Pdf
og_title: Agregar numeración Bates a PDFs en C# – guía completa de Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  headline: How to add bates numbering to a PDF with Aspose.Pdf
  type: TechArticle
- description: Learn how to add bates numbering to a PDF using C#. This step‑by‑step
    guide also covers pdf page numbering and other numbering tricks.
  name: How to add bates numbering to a PDF with Aspose.Pdf
  steps:
  - name: 1. Can I change the location of the numbers?
    text: Yes. Set `batesOptions.Position = new Position(10, 10, 10, 10);` where the
      four values represent margins from the top, bottom, left, and right edges. Aspose
      also provides predefined enums such as `BatesNumberingPosition.BottomCenter`.
  - name: 2. What if my PDF already contains page numbers?
    text: Adding Bates numbers will **stack** on top of existing numbers. To avoid
      visual clutter, either hide the original numbers (if they are part of a text
      layer) or adjust the `batesOptions` font size and position.
  - name: 3. Does this work with encrypted PDFs?
    text: 'Aspose can open password‑protected PDFs if you supply the password:'
  - name: 4. How do I **number pdf pages** with a simple sequential counter (no prefix/suffix)?
    text: 'Just set `Prefix = string.Empty` and `Suffix = string.Empty`:'
  - name: 5. Can I use this approach in ASP.NET Core to serve PDFs on‑the‑fly?
    text: 'Absolutely. Load the document, apply the numbering, then write the stream
      to the HTTP response:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cómo agregar numeración Bates a un PDF con Aspose.Pdf
url: /es/net/programming-with-pdf-pages/how-to-add-bates-numbering-to-a-pdf-with-aspose-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar numeración Bates a un PDF con Aspose.Pdf

Si necesita **agregar numeración bates** a un PDF, esta guía le muestra exactamente cómo hacerlo en C#. Ya sea que esté preparando paquetes legales, gestionando expedientes de casos, o simplemente quiera una **numeración de páginas pdf** confiable, los pasos a continuación le brindan una solución completa y ejecutable.

En este tutorial aprenderá a:

* Cargar un archivo PDF existente.
* Configurar opciones de numeración Bates como prefijo, número inicial, relleno de dígitos, separador y sufijo.
* Aplicar la numeración a cada página.
* Guardar el documento actualizado.

No se requieren herramientas externas más allá de la biblioteca Aspose.Pdf for .NET, y el código funciona con .NET 6+ así como con .NET Framework 4.7.2+.  

---

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| **Aspose.Pdf for .NET** (NuGet package `Aspose.Pdf`) | Proporciona las clases `Document` y `BatesNumberingOptions` utilizadas en el código. |
| **.NET SDK** (6.0 o posterior recomendado) | Le permite compilar y ejecutar la aplicación de consola C#. |
| **A source PDF** you want to number | El tutorial usa `source.pdf` como ejemplo; reemplace la ruta con su propio archivo. |
| **Write permission** to the output folder | La llamada `Save` necesita escribir el nuevo archivo. |

Puede instalar la biblioteca con el siguiente comando CLI:

```bash
dotnet add package Aspose.Pdf
```

---

## Paso 1: Crear un nuevo proyecto de consola

Abra una terminal y ejecute:

```bash
dotnet new console -n BatesNumberingDemo
cd BatesNumberingDemo
```

Esto crea un proyecto C# mínimo que completaremos con el código necesario para **agregar numeración bates**.

---

## Paso 2: Agregar las directivas `using` requeridas

Abra `Program.cs` y agregue los espacios de nombres al inicio del archivo:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

* `Aspose.Pdf` le brinda acceso a la clase `Document` para cargar y guardar PDFs.  
* `Aspose.Pdf.Text` contiene `BatesNumberingOptions`, el objeto que define cómo aparecen los números.

---

## Paso 3: Cargar el PDF de origen

La primera línea ejecutable carga el PDF que desea numerar. Reemplace `"YOUR_DIRECTORY/source.pdf"` con la ruta real a su archivo.

```csharp
// Load the source PDF
Document pdf = new Document("YOUR_DIRECTORY/source.pdf");
```

Si el archivo no se encuentra, Aspose lanza una `FileNotFoundException`. Para evitarlo, puede validar la ruta previamente:

```csharp
if (!System.IO.File.Exists("YOUR_DIRECTORY/source.pdf"))
{
    Console.WriteLine("Source PDF not found.");
    return;
}
```

---

## Paso 4: Definir las opciones de numeración Bates

`BatesNumberingOptions` le permite controlar cada elemento visual de la numeración. El ejemplo a continuación muestra una configuración típica para expedientes legales:

```csharp
// Define Bates numbering options
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    Prefix = "CASE-",          // Text before the numeric part
    StartNumber = 1000,       // First number to use
    Digits = 6,               // Pad with leading zeros (e.g., 001000)
    Separator = "-",          // Character between prefix, number, and suffix
    Suffix = "-2025"          // Text after the numeric part
};
```

**Por qué cada propiedad es importante**

| Propiedad | Propósito |
|----------|-----------|
| `Prefix` | Le ayuda a agrupar documentos por proyecto, cliente o caso. |
| `StartNumber` | Establece el contador inicial; útil cuando ya tiene archivos numerados existentes. |
| `Digits` | Garantiza un ancho uniforme, facilitando la ordenación. |
| `Separator` | Mejora la legibilidad, especialmente al combinar prefijo y sufijo. |
| `Suffix` | Le permite agregar un año, versión o cualquier identificador final. |

También puede controlar la ubicación (superior, inferior, izquierda, derecha) y el estilo de fuente accediendo a `batesOptions.Position` y `batesOptions.Font`. Para la mayoría de los escenarios, los valores predeterminados (abajo‑derecha, Times New Roman de 12 pt) funcionan bien.

---

## Paso 5: Aplicar la numeración a cada página

Llamar a `pdf.BatesNumbering.Add` inserta los números en cada página en el orden en que aparecen.

```csharp
// Apply Bates numbering to every page
pdf.BatesNumbering.Add(batesOptions);
```

Si necesita **numerar páginas pdf** solo en un subconjunto (p. ej., omitir la página de portada), puede pasar un `PageCollection` en su lugar:

```csharp
// Example: skip the first page
pdf.BatesNumbering.Add(batesOptions, pdf.Pages.Skip(1));
```

---

## Paso 6: Guardar el PDF actualizado

Finalmente, escriba el documento modificado en disco. El nombre del archivo suele reflejar que el PDF ahora contiene números Bates.

```csharp
// Save the PDF with Bates numbers applied
pdf.Save("YOUR_DIRECTORY/bates_numbered.pdf");
Console.WriteLine("Bates numbering added successfully.");
```

Si la carpeta de salida no existe, Aspose la crea automáticamente. Sin embargo, debe asegurarse de tener permisos de escritura para evitar una `UnauthorizedAccessException`.

---

## Ejemplo completo y ejecutable

Juntando todas las piezas, aquí hay un programa completo que puede copiar, pegar y ejecutar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source PDF
        // -------------------------------------------------
        const string inputPath = "YOUR_DIRECTORY/source.pdf";
        if (!System.IO.File.Exists(inputPath))
        {
            Console.WriteLine($"Input file not found: {inputPath}");
            return;
        }

        Document pdf = new Document(inputPath);

        // -------------------------------------------------
        // 2️⃣ Configure Bates numbering
        // -------------------------------------------------
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            Digits = 6,
            Separator = "-",
            Suffix = "-2025"
        };

        // -------------------------------------------------
        // 3️⃣ Apply the numbering to every page
        // -------------------------------------------------
        pdf.BatesNumbering.Add(batesOptions);

        // -------------------------------------------------
        // 4️⃣ Save the result
        // -------------------------------------------------
        const string outputPath = "YOUR_DIRECTORY/bates_numbered.pdf";
        pdf.Save(outputPath);
        Console.WriteLine($"Bates numbering added. Saved to {outputPath}");
    }
}
```

**Salida esperada** (consola):

```
Bates numbering added. Saved to YOUR_DIRECTORY/bates_numbered.pdf
```

Abra `bates_numbered.pdf` y verá cada página etiquetada con algo como `CASE-001000-2025`, `CASE-001001-2025`, etc., posicionada en la esquina inferior‑derecha predeterminada.

---

## Preguntas frecuentes (FAQ)

### 1. ¿Puedo cambiar la ubicación de los números?

Sí. Establezca `batesOptions.Position = new Position(10, 10, 10, 10);` donde los cuatro valores representan los márgenes desde los bordes superior, inferior, izquierdo y derecho. Aspose también ofrece enumeraciones predefinidas como `BatesNumberingPosition.BottomCenter`.

### 2. ¿Qué pasa si mi PDF ya contiene números de página?

Agregar números Bates **se superpondrá** a los números existentes. Para evitar desorden visual, oculte los números originales (si forman parte de una capa de texto) o ajuste el tamaño de fuente y la posición en `batesOptions`.

### 3. ¿Esto funciona con PDFs encriptados?

Aspose puede abrir PDFs protegidos con contraseña si proporciona la contraseña:

```csharp
Document pdf = new Document("source.pdf", new LoadOptions { Password = "mySecret" });
```

### 4. ¿Cómo **numerar páginas pdf** con un contador secuencial simple (sin prefijo/sufijo)?

Simplemente establezca `Prefix = string.Empty` y `Suffix = string.Empty`:

```csharp
BatesNumberingOptions simple = new BatesNumberingOptions
{
    StartNumber = 1,
    Digits = 4   // 0001, 0002, …
};
pdf.BatesNumbering.Add(simple);
```

### 5. ¿Puedo usar este enfoque en ASP.NET Core para servir PDFs al vuelo?

Absolutamente. Cargue el documento, aplique la numeración y luego escriba el flujo en la respuesta HTTP:

```csharp
using (var ms = new MemoryStream())
{
    pdf.Save(ms);
    ms.Position = 0;
    return File(ms, "application/pdf", "bates_numbered.pdf");
}
```

---

## Casos límite y consejos de mejores prácticas

| Situación | Enfoque recomendado |
|-----------|----------------------|
| **Large PDFs (hundreds of pages)** | Llame a `pdf.BatesNumbering.Add` **después** de haber realizado cualquier transformación a nivel de página para evitar volver a procesar las mismas páginas varias veces. |
| **Custom fonts** | Establezca `batesOptions.Font = FontRepository.FindFont("Arial")` y ajuste `batesOptions.FontSize` para una mejor legibilidad en documentos escaneados. |
| **Performance‑critical batch jobs** | Reutilice una única instancia de `Document` al procesar muchos archivos en un bucle; dispóngala después de cada iteración para liberar memoria. |
| **International characters** | Utilice fuentes compatibles con Unicode (p. ej., `Times New Roman Unicode`) para garantizar que el prefijo o sufijo se muestre correctamente. |
| **Version compatibility** | El código funciona con Aspose.Pdf 23.10 y versiones posteriores. Si apunta a una versión anterior, revise la referencia de la API para cualquier cambio en los nombres de propiedades. |

---

## Conclusión

Ahora sabe cómo **agregar numeración bates** a un PDF usando Aspose.Pdf para .NET. El tutorial cubrió la carga de un PDF, la configuración de `BatesNumberingOptions`, la aplicación de los números a cada página y el guardado del resultado. Con estos bloques de construcción también puede implementar la **numeración de páginas pdf** genérica, **numerar páginas pdf** con formatos personalizados e integrar el proceso en pipelines de automatización más grandes.

**Próximos pasos**

* Explore la API de **bates numbering pdf** más a fondo para personalizar la fuente, el color y la ubicación.  
* Combine esta técnica con **firmas digitales** para crear paquetes legales a prueba de manipulaciones.  
* Investigue las capacidades de **fusión de PDF** de Aspose si necesita concatenar varios expedientes antes de numerar.

Siéntase libre de experimentar con diferentes prefijos, sufijos y longitudes de dígitos para que coincidan con los estándares de archivo de su organización. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Crear documento PDF C# – Guía para agregar numeración Bates](/pdf/english/net/document-creation/create-pdf-document-c-add-bates-numbering-guide/)
- [Cómo agregar numeración Bates en PDF con C# – Guía completa](/pdf/english/net/programming-with-stamps-and-watermarks/how-to-add-bates-numbering-in-pdf-with-c-complete-guide/)
- [Tutorial de Aspose PDF – Insertar una página en blanco y actualizar la numeración Bates](/pdf/english/net/programming-with-pdf-pages/aspose-pdf-tutorial-insert-a-blank-page-and-update-bates-num/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}