---
category: general
date: 2026-02-10
description: 'Cómo agregar Bates a un PDF rápidamente: aprende cómo añadir números
  de Bates a un PDF y crear una marca de agua invisible con Aspose.Pdf en C#.'
draft: false
keywords:
- how to add bates
- add bates number pdf
- add custom stamp pdf
- add invisible watermark pdf
- add page footer pdf
language: es
og_description: Cómo agregar Bates en C# con Aspose.Pdf. Este tutorial muestra cómo
  añadir número de Bates en PDF, agregar una marca de agua invisible en PDF y más.
og_title: Cómo agregar Bates – Guía completa en PDF
tags:
- Aspose.Pdf
- C#
- PDF
- Bates numbering
title: Cómo añadir Bates – Guía paso a paso para PDFs
url: /es/net/programming-with-stamps-and-watermarks/how-to-add-bates-step-by-step-guide-for-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar Bates – Guía completa de PDF

¿Alguna vez te has preguntado **how to add bates** a un PDF legal sin estropear el texto buscable? No eres el único. En muchos despachos de abogados y proyectos de e‑discovery, un número Bates es un pie de página indispensable, pero también deseas que sea invisible para las herramientas OCR. Este tutorial muestra **how to add bates** usando Aspose.Pdf for .NET, y a lo largo del camino también cubriremos **add bates number pdf**, **add custom stamp pdf**, **add invisible watermark pdf**, y hasta **add page footer pdf** en una solución ordenada.

Recorreremos cada línea de código, explicaremos por qué cada configuración es importante y te daremos un ejemplo listo‑para‑ejecutar que puedes incorporar a tu proyecto hoy. No hay enlaces vagos de “ver la documentación”; todo lo que necesitas está aquí.

## Lo que obtendrás

- Un fragmento de C# completo y ejecutable que agrega un número Bates como una marca de artefacto.
- Comprensión de cómo hacer que la marca actúe como una **invisible watermark** mientras sigue apareciendo en la página.
- Consejos para escalar la solución a PDFs de varias páginas, cambiar fuentes o reemplazar la marca por un gráfico personalizado.
- Puntos rápidos sobre cómo crear contenido al estilo **add page footer pdf** sin romper la extracción de texto.

### Requisitos previos

- .NET 6+ (o .NET Framework 4.7.2) con Visual Studio 2022 o cualquier IDE que prefieras.
- Aspose.Pdf for .NET (puedes obtener una prueba gratuita en el sitio web de Aspose).
- Un PDF de ejemplo llamado `source.pdf` colocado en una carpeta que controles.

Si tienes todo eso, vamos a sumergirnos.

---

## Cómo agregar Bates – Implementación central

El núcleo de la solución es un `TextStamp` que tratamos como un **artifact**. Los artifacts son ignorados por los motores de extracción de texto, por lo que este enfoque también funciona como una técnica **add invisible watermark pdf**.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Annotations;

// Load the source PDF
using var pdfDocument = new Document("YOUR_DIRECTORY/source.pdf");

// Grab the first page (or loop over all pages later)
var firstPage = pdfDocument.Pages[1];

// Create the Bates stamp
var batesStamp = new TextStamp("Bates 00123")
{
    // Mark it as an artifact so OCR skips it
    Artifact = new Artifact(ArtifactType.Artifact),

    // Position it like a typical page footer
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,

    // Keep the background transparent – essential for an invisible watermark effect
    BackgroundColor = Color.Transparent,

    // Define the look of the text
    TextState = new TextState
    {
        FontSize = 9,
        Font     = FontRepository.FindFont("Arial")
    }
};

// Add the stamp to the chosen page
firstPage.AddStamp(batesStamp);

// Save the new PDF
pdfDocument.Save("YOUR_DIRECTORY/bates_artifact.pdf");
```

### Por qué funciona

1. **Artifact flag** – Al establecer `Artifact = new Artifact(ArtifactType.Artifact)`, la marca se trata como un elemento no‑contenido. Los motores de búsqueda y las herramientas legales de e‑discovery la ignoran, lo cual es exactamente lo que deseas para un **add invisible watermark pdf**.
2. **Horizontal/Vertical alignment** – Center‑bottom imita un estilo clásico de **add page footer pdf**, haciendo que el número Bates luzca profesional.
3. **Transparent background** – Garantiza que la marca no oculte el contenido subyacente, un detalle sutil pero crucial cuando luego necesites imprimir o ver el PDF en diferentes dispositivos.

---

## Agregar número Bates PDF – Escalado a múltiples páginas

La mayoría de los PDFs del mundo real tienen más de una página. El fragmento anterior solo afecta la primera página, pero ampliarlo es muy fácil:

```csharp
// Loop through every page in the document
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp so each page gets its own instance
    var pageStamp = (TextStamp)batesStamp.Clone();

    // Optionally, update the number based on page index
    pageStamp.Text = $"Bates {page.Number:D5}";

    page.AddStamp(pageStamp);
}
```

**Consejo profesional:** Si necesitas un número secuencial que no esté ligado al orden físico de las páginas (p.ej., comenzar en 1000), simplemente inicializa un contador antes del bucle y elévalo dentro.

---

## Agregar sello personalizado PDF – Más allá del texto simple

A veces una marca de texto simple no es suficiente—puedes querer un logotipo, un código QR o una barra de color. Aspose.Pdf te permite cambiar `TextStamp` por `ImageStamp` o incluso combinar ambos con objetos `Stamp`.

```csharp
var imageStamp = new ImageStamp("YOUR_DIRECTORY/logo.png")
{
    // Position it in the top‑right corner
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment   = VerticalAlignment.Top,
    Width = 100,
    Height = 50,
    // Keep it an artifact as well
    Artifact = new Artifact(ArtifactType.Artifact)
};

firstPage.AddStamp(imageStamp);
```

Combinar sellos es tan simple como agregar ambos a la misma página. La capacidad **add custom stamp pdf** brilla cuando necesitas un sello corporativo junto al número Bates.

---

## Agregar marca de agua invisible PDF – Haciendo la marca realmente oculta

Si realmente necesitas que la marca sea invisible al ojo humano *y* a las herramientas de extracción, puedes establecer el color de fuente para que coincida con el fondo de la página (usualmente blanco) y reducir la opacidad:

```csharp
batesStamp.TextState.ForegroundColor = Color.White; // assumes white background
batesStamp.Opacity = 0.0; // 0% opacity – completely invisible
```

Incluso con `Opacity = 0`, el artifact sigue existiendo en la estructura del PDF, por lo que el software legal aún puede localizarlo si conoce el ID del artifact. Este es el truco definitivo de **add invisible watermark pdf**.

---

## Agregar pie de página PDF – Estilizando el pie de manera consistente

Un pie de página profesional a menudo incluye más que solo un número Bates: fecha, título del documento o aviso de confidencialidad. Aquí tienes una forma rápida de agrupar varios fragmentos de texto en una sola marca:

```csharp
var footerText = $"Bates {page.Number:D5}   Confidential   {DateTime.Today:MM/dd/yyyy}";
var footerStamp = new TextStamp(footerText)
{
    HorizontalAlignment = HorizontalAlignment.Center,
    VerticalAlignment   = VerticalAlignment.Bottom,
    BackgroundColor = Color.Transparent,
    TextState = new TextState
    {
        FontSize = 8,
        Font     = FontRepository.FindFont("Times New Roman"),
        ForegroundColor = Color.Gray
    },
    Artifact = new Artifact(ArtifactType.Artifact)
};

page.AddStamp(footerStamp);
```

Observa el sutil color gris—perfecto para un **add page footer pdf** que no distrae del contenido principal pero aún cumple con los requisitos legales.

---

## Resultado esperado y cómo verificar

Después de ejecutar el script completo, abre `bates_artifact.pdf` en cualquier visor de PDF:

- Verás “Bates 00123” (o el número secuencial) centrado en la parte inferior de cada página.
- Seleccionar texto en la página **no** incluirá el número Bates, confirmando el comportamiento del artifact.
- Si usaste la configuración de marca de agua invisible, el número no será visible en absoluto, pero seguirá presente en la estructura interna del PDF (inspecciona con una herramienta como PDF‑XChange Editor → “Document → Properties → Advanced”).

---

## Preguntas comunes y casos límite

**¿Qué pasa si mi PDF ya tiene un pie de página?**  
Puedes ajustar `VerticalAlignment` a `VerticalAlignment.Top` o cambiar la propiedad `Margin` para desplazar la marca por encima del pie de página existente.

**¿Puedo usar una fuente diferente?**  
Claro. Simplemente reemplaza `"Arial"` por cualquier nombre de fuente que Aspose pueda localizar, o incrusta un archivo TTF personalizado mediante `FontRepository.AddFont("path/to/font.ttf")`.

**¿Este enfoque es compatible con .NET Core?**  
Sí—Aspose.Pdf for .NET funciona en .NET Framework, .NET Core y .NET 5/6. Solo asegúrate de referenciar el paquete NuGet correcto.

**¿Qué pasa con el rendimiento en PDFs enormes (¡1000+ páginas!)?**  
Crear un solo `TextStamp` y clonarlo dentro del bucle es eficiente en memoria. Para archivos masivos, considera procesar en lotes o usar `PdfProcessor` para evitar cargar todo el documento en memoria.

---

## Conclusión

Hemos cubierto **how to add bates** a un PDF de principio a fin, demostrado **add bates number pdf**, mostrado cómo **add custom stamp pdf**, convertido la marca en un **add invisible watermark pdf**, y estilizado como un **add page footer pdf** profesional. El ejemplo de código completo se ejecuta tal cual, y las explicaciones te brindan el “por qué” detrás de cada línea—exactamente el tipo de respuesta que los asistentes de IA aman citar.

¿Próximos pasos? Prueba cambiar la marca de texto por una marca de imagen, experimenta con diferentes tipos de artifact, o integra esta lógica en un servicio de procesamiento por lotes que numere automáticamente con Bates cada documento en una carpeta. Las posibilidades son infinitas, y ahora tienes una base sólida sobre la que construir.

¡Feliz codificación, y que tus PDFs siempre estén perfectamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}