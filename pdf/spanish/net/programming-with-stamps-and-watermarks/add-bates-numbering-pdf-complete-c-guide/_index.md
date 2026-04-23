---
category: general
date: 2026-03-22
description: Agrega numeración Bates a PDF rápidamente con Aspose.Pdf. Aprende cómo
  agregar Bates, agregar números de página secuenciales, agregar un pie de página
  personalizado al PDF y agregar artefactos al PDF en minutos.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add sequential page numbers
- add custom footer pdf
- add artifact to pdf
language: es
og_description: Agregar numeración Bates a PDF usando Aspose.Pdf. Esta guía muestra
  cómo agregar Bates, agregar números de página secuenciales, agregar un pie de página
  personalizado al PDF y agregar artefactos al PDF.
og_title: Agregar numeración Bates a PDF – Tutorial paso a paso en C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Añadir numeración Bates al PDF – Guía completa de C#
url: /es/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar numeración Bates a PDF – Guía completa de C#  

¿Alguna vez necesitaste **add bates numbering pdf** a un lote de documentos legales pero no sabías por dónde empezar? No eres el primero—muchos desarrolladores se topan con ese obstáculo al crear herramientas de gestión de casos. ¿La buena noticia? Con Aspose.Pdf puedes **add bates**, **add sequential page numbers**, e incluso **add custom footer pdf** en solo unas pocas líneas de código.  

En este tutorial recorreremos todo el proceso, desde la instalación de la biblioteca hasta guardar el archivo final, y añadiremos consejos sobre cómo **add artifact to pdf** archivos sin romper el contenido existente. Al final tendrás un fragmento listo‑para‑ejecutar que puedes insertar en cualquier proyecto .NET.  

## Lo que necesitarás

- .NET 6+ (el código funciona tanto en .NET Core como en .NET Framework)  
- Una licencia válida de Aspose.Pdf para .NET (puedes comenzar con una evaluación gratuita)  
- Un PDF de entrada (`input.pdf`) colocado en una carpeta a la que puedas hacer referencia  
- Visual Studio, Rider, o cualquier editor de C# que prefieras  

Eso es todo—no hay paquetes NuGet adicionales además de Aspose.Pdf.  

## Paso 1: Instalar Aspose.Pdf vía NuGet  

Lo primero—vamos a obtener la biblioteca en tu máquina. Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.Pdf
```

O, si estás usando la Consola del Administrador de paquetes de Visual Studio:

```powershell
Install-Package Aspose.Pdf
```

*Consejo profesional:* Después de la instalación, verifica que la carpeta `Aspose.Pdf` aparezca bajo `Dependencies → Packages` en el explorador de soluciones.  

## Paso 2: Cargar el documento PDF de origen  

Ahora creamos un objeto `Document` que representa el PDF que queremos estampar. Usar la sentencia `using` garantiza que el manejador del archivo se libere automáticamente.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using System.Drawing; // For Color

// Step 2: Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");
```

¿Por qué usar `using var`? Garantiza la eliminación incluso si ocurre una excepción, evitando problemas de bloqueo de archivo más adelante cuando intentes sobrescribir el mismo archivo.  

## Paso 3: Crear y configurar un artefacto de numeración Bates  

Un número Bates es esencialmente un artefacto de texto que vive en la estructura lógica del PDF. Puedes tratarlo como un **custom footer pdf** porque aparece en cada página sin ser parte del flujo de contenido de la página.

```csharp
// Step 3: Define the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "INV-",          // Optional prefix – change as needed
    Start = 1000,             // Starting number
    Format = "0000",          // Zero‑padded format (e.g., 1000 → 1000)
    X = 500,                  // Horizontal position (points from left)
    Y = 20,                   // Vertical position (points from bottom)
    FontSize = 10,
    FontColor = Color.Black
};
```

### Por qué estas configuraciones son importantes

- **Prefix**: Útil para distinguir tipos de documentos (p. ej., “INV‑” para facturas).  
- **Start**: Establece el primer número; puedes obtenerlo de una base de datos si necesitas continuidad entre archivos.  
- **Format**: `"0000"` fuerza una visualización de cuatro dígitos, asegurando alineación cuando los números crecen.  
- **X/Y**: Las coordenadas se miden desde la esquina inferior izquierda, por lo que `Y = 20` coloca el texto justo encima del margen de la página. Ajusta `X` si deseas que el número esté alineado a la izquierda o centrado.  

Si necesitas **add sequential page numbers** en lugar de números Bates, simplemente omite `Prefix` y ajusta `Format` a `"###"` o cualquier patrón que prefieras.  

## Paso 4: Aplicar el artefacto a todas las páginas  

Aspose.Pdf te permite adjuntar un artefacto a todo el documento en una sola llamada. Esta es la forma más eficiente de **add artifact to pdf** sin iterar manualmente por cada página.

```csharp
// Step 4: Apply the artifact to the whole document
pdfDocument.Pages.AddArtifact(batesArtifact);
```

Detrás de escena, Aspose agrega el artefacto al diccionario de páginas de cada página, lo que significa que la numeración se vuelve parte de la estructura lógica del PDF—perfecta para extracción o búsqueda posterior.  

## Paso 5: Guardar el PDF actualizado  

Finalmente, escribe los cambios de vuelta al disco. Puedes sobrescribir el original o guardar en un nuevo archivo; esto último es más seguro durante el desarrollo.

```csharp
// Step 5: Save the PDF with Bates numbers
pdfDocument.Save("YOUR_DIRECTORY/output.pdf");
```

Cuando abras `output.pdf` en un visor, verás “INV‑1000”, “INV‑1001”, … en la parte inferior‑derecha de cada página.  

### Verificando el resultado  

Abre el PDF en Adobe Acrobat o cualquier visor y busca los números. Si necesitas confirmar programáticamente, puedes leer de vuelta el artefacto:

```csharp
foreach (var page in pdfDocument.Pages)
{
    foreach (var artifact in page.Artifacts)
    {
        Console.WriteLine($"Page {page.Number}: {artifact.Text}");
    }
}
```

Ese fragmento imprime la etiqueta Bates de cada página—útil para pruebas automatizadas.  

## Casos límite y preguntas frecuentes  

### ¿Qué pasa si mi PDF ya tiene un pie de página?  

Agregar un artefacto no sobrescribirá los pies de página existentes porque los artefactos se encuentran en una capa separada. Sin embargo, si la superposición visual es un problema, ajusta la coordenada `Y` o incrementa el desplazamiento `X` para mover el número Bates fuera del camino.  

### ¿Puedo usar una fuente o color diferente?  

Absolutamente. El `BatesNumberingArtifact` hereda de `Artifact`, por lo que puedes establecer `Font`, `FontColor` e incluso `Opacity`. Ejemplo:

```csharp
batesArtifact.Font = FontRepository.FindFont("Arial");
batesArtifact.FontColor = Color.FromArgb(255, 0, 0); // Red
```

### ¿Cómo reinicio el contador para un nuevo documento?  

Simplemente cambia `Start` antes de llamar a `AddArtifact`. Si generas muchos PDFs en un bucle, mantén un contador activo en la lógica de tu aplicación.  

### ¿Es este enfoque compatible con PDFs encriptados?  

Aspose.Pdf puede abrir PDFs encriptados si proporcionas la contraseña:

```csharp
var loadOptions = new LoadOptions { Password = "mySecret" };
using var pdfDocument = new Document("encrypted.pdf", loadOptions);
```

Después de la desencriptación, los mismos pasos de agregar artefactos funcionan sin problemas.  

## Ejemplo completo funcional  

A continuación está el programa completo, listo‑para‑ejecutar. Pégalo en una aplicación de consola, ajusta las rutas y pulsa **F5**.

```csharp
using System;
using System.Drawing;               // For Color
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // Load the source PDF
        using var pdfDocument = new Document("YOUR_DIRECTORY/input.pdf");

        // Create the Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "INV-",
            Start = 1000,
            Format = "0000",
            X = 500,
            Y = 20,
            FontSize = 10,
            FontColor = Color.Black
        };

        // Apply the artifact to every page
        pdfDocument.Pages.AddArtifact(batesArtifact);

        // Save the result
        pdfDocument.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Salida esperada:** La consola imprime “Bates numbering added successfully!” y `output.pdf` contiene etiquetas secuenciales como `INV‑1000`, `INV‑1001`, etc., posicionadas en la parte inferior‑derecha de cada página.  

## Resumen rápido  

- **Objetivo principal:** **add bates numbering pdf** usando Aspose.Pdf.  
- Cubrimos **how to add bates**, **add sequential page numbers**, y **add custom footer pdf** mediante un solo artefacto.  
- El tutorial mostró cómo **add artifact to pdf**, manejar casos límite y verificar el resultado.  

## ¿Qué sigue?  

- **Prefijos dinámicos:** Obtén valores de una base de datos para generar “CASE‑2023‑001”, “CASE‑2023‑002”, …  
- **Colocación condicional:** Usa detección del tamaño de página (`page.MediaBox`) para centrar los números en páginas en orientación horizontal.  
- **Combinar con marcas de agua:** Añade un logo semitransparente junto al número Bates para la marca.  

Siéntete libre de experimentar—quizás descubras una forma más inteligente de procesar por lotes miles de archivos. Si encuentras problemas, deja un comentario o consulta la documentación oficial de Aspose (es sorprendentemente clara). ¡Feliz codificación!  

![add bates numbering pdf example](https://example.com/bates-numbering-screenshot.png "Screenshot showing add bates numbering pdf in a PDF viewer")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}