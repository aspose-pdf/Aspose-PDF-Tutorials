---
category: general
date: 2026-06-08
description: Recortar imagen en PDF usando Aspose.PDF en C#. Aprende cómo crear un
  PDF con imagen, guardar PDF con imagen y agregar imagen a PDF en solo unas pocas
  líneas.
draft: false
keywords:
- crop image in pdf
- create pdf with image
- save pdf with image
- how to add image to pdf
- how to crop image pdf
language: es
og_description: Recortar imagen en PDF usando Aspose.PDF en C#. Este tutorial muestra
  cómo crear un PDF con imagen, guardar un PDF con imagen y añadir una imagen al PDF
  rápidamente.
og_title: Recortar imagen en PDF con Aspose.PDF – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  headline: Crop Image in PDF with Aspose.PDF – Complete Guide
  type: TechArticle
- description: Crop image in PDF using Aspose.PDF in C#. Learn how to create PDF with
    image, save PDF with image, and add image to PDF in just a few lines.
  name: Crop Image in PDF with Aspose.PDF – Complete Guide
  steps:
  - name: '**Image stream** – the raw bytes of your picture.'
    text: '**Image stream** – the raw bytes of your picture.'
  - name: '**Placement rectangle** – where on the page the image lives.'
    text: '**Placement rectangle** – where on the page the image lives.'
  - name: '**Crop rectangle** – the portion of the image you actually want to render.'
    text: '**Crop rectangle** – the portion of the image you actually want to render.'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF manipulation
- Image processing
title: Recortar imagen en PDF con Aspose.PDF – Guía completa
url: /es/net/programming-with-images/crop-image-in-pdf-with-aspose-pdf-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recortar Imagen en PDF con Aspose.PDF – Guía Completa

¿Alguna vez te has preguntado cómo **recortar imagen en PDF** sin abrir un editor gráfico? No eres el único. En muchos informes, facturas o libros electrónicos necesitas solo una porción de una imagen—quizás la esquina del logotipo o un fragmento de un gráfico—y deseas que esté directamente dentro del PDF.  

Esta guía te muestra exactamente eso: **crearemos PDF con imagen**, **añadiremos imagen a PDF**, y luego **recortaremos imagen en PDF** usando la biblioteca Aspose.PDF para C#. Al final también sabrás cómo **guardar PDF con imagen** para que puedas enviar el archivo a cualquiera.

---

## Lo que Necesitarás

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)  
- Una copia con licencia o de prueba de **Aspose.PDF for .NET** (instalar vía NuGet `Install-Package Aspose.PDF`)  
- Un archivo de imagen (JPEG/PNG) en disco — lo llamaremos `image.jpg`  
- Cualquier IDE que prefieras (Visual Studio, Rider, VS Code)

Eso es todo. Sin servicios adicionales, sin herramientas externas.

---

## Paso 1: Configurar el Proyecto e Importaciones

Primero, crea una aplicación de consola y agrega los espacios de nombres que utilizaremos. Las sentencias `using` mantienen el código ordenado y facilitan la lectura de los pasos posteriores.

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;   // for text fragments if you want captions later
```

> **Consejo profesional:** Si estás usando Visual Studio, haz clic derecho en el proyecto → *Administrar paquetes NuGet* → busca “Aspose.PDF” e instala. La biblioteca maneja tanto la colocación de la imagen como el recorte internamente, por lo que no necesitarás bibliotecas de imágenes de terceros.

---

## Paso 2: Crear PDF con Imagen

Ahora realmente **creamos pdf con imagen**. El fragmento a continuación crea un nuevo `Document`, agrega una página en blanco y prepara un flujo de imagen.

```csharp
// Initialize a new PDF document
Document pdf = new Document();

// Add a blank page – think of it as a clean canvas
Page page = pdf.Pages.Add();

// Open the source image file
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // We'll place the whole image first; cropping comes next
    // Define where the image should sit on the page (in points; 1 point = 1/72 inch)
    Rectangle placement = new Rectangle(0, 0, 600, 800); // width=600pt, height=800pt

    // Add the image without cropping yet – just to see the full picture
    page.AddImage(imgStream, placement);
}
```

Ejecutar este código te generará un PDF con la imagen completa estirada a las dimensiones que especificaste. Es una buena verificación antes de comenzar a recortar.

---

## Paso 3: Cómo Añadir Imagen a PDF (y Preparar para Recortar)

Si ya conoces la región exacta que deseas, puedes omitir el paso de tamaño completo y pasar directamente a la parte de **cómo añadir imagen a pdf**. El método `AddImage` acepta tres parámetros:

1. **Flujo de imagen** – los bytes sin procesar de tu foto.  
2. **Rectángulo de colocación** – dónde en la página se ubica la imagen.  
3. **Rectángulo de recorte** – la porción de la imagen que realmente deseas renderizar.

A continuación se muestra la versión compacta que realiza tanto la colocación **como** el recorte en una sola llamada.

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Full‑size placement rectangle (you can adjust X/Y if you need margins)
    Rectangle placement = new Rectangle(0, 0, 600, 800);

    // Crop area: upper‑left quarter of the original image
    Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

    // This single line both adds the image and crops it
    page.AddImage(imgStream, placement, crop);
}
```

> **Por qué funciona:** Aspose.PDF asigna internamente el rectángulo de recorte a las dimensiones de píxel de la imagen, y luego renderiza solo esa porción dentro del área de `placement`. No se requiere procesamiento adicional de bitmap, lo que significa que mantienes el tamaño del PDF pequeño.

---

## Paso 4: Cómo Recortar Imagen en PDF – Opciones Avanzadas

A veces el recorte de un cuarto no es suficiente. Tal vez necesites un rectángulo personalizado o quieras preservar la relación de aspecto de la imagen. Aquí hay un enfoque más flexible:

```csharp
using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
{
    // Placement on the page (centered, 300pt wide, keep original height)
    Rectangle placement = new Rectangle(150, 400, 450, 1200);

    // Suppose you want a 200 × 150 pixel region starting at (50, 30) in the source image
    // First, convert pixel coordinates to points (assuming 72 DPI)
    float dpi = 72f;
    float left   = 50  / dpi * 72; // = 50 points
    float bottom = 30  / dpi * 72; // = 30 points
    float width  = 200 / dpi * 72; // = 200 points
    float height = 150 / dpi * 72; // = 150 points

    Rectangle crop = new Rectangle(left, bottom, left + width, bottom + height);

    page.AddImage(imgStream, placement, crop);
}
```

**Manejo de casos límite:**  
- **Flujos nulos** – siempre envuelve el `FileStream` en un bloque `using`, como se muestra, para evitar fugas.  
- **Imágenes grandes** – si la imagen de origen es enorme, considera reducir el rectángulo de `placement`; Aspose reducirá la muestra automáticamente.  
- **PNGs transparentes** – la biblioteca respeta los canales alfa, por lo que tu área recortada mantendrá la transparencia.

---

## Paso 5: Guardar PDF con Imagen (y Verificar)

Finalmente, **guardamos pdf con imagen**. El método `Save` escribe el documento en disco. También puedes enviarlo como stream a un cliente web si estás construyendo una API.

```csharp
// Save the final PDF to the output folder
pdf.Save("YOUR_DIRECTORY/output.pdf");

// Optional: Open the file automatically (only works on Windows)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/output.pdf",
    UseShellExecute = true
});
```

Al abrir `output.pdf`, deberías ver solo la porción recortada de `image.jpg` posicionada exactamente donde la definiste. Si la imagen se ve estirada, ajusta el ancho/alto del rectángulo de `placement` para que coincida con la relación de aspecto del rectángulo de recorte.

---

## Preguntas Frecuentes y Trucos

| Pregunta | Respuesta |
|----------|----------|
| **¿Puedo recortar varias imágenes en la misma página?** | Por supuesto. Llama a `page.AddImage` para cada imagen con sus propios rectángulos de colocación y recorte. |
| **¿Qué pasa si mi imagen está en otro formato (p. ej., BMP)?** | Aspose.PDF admite JPEG, PNG, BMP, GIF y TIFF de forma nativa. Simplemente cambia la extensión del archivo. |
| **¿Necesito una licencia para uso en producción?** | La versión de prueba funciona hasta 5 páginas. Para despliegues reales, compra una licencia para eliminar la marca de agua. |
| **¿Cómo rotar la imagen recortada?** | Después de añadir la imagen, obtén el objeto `Image` y establece su propiedad `Rotate` (`Rotate = RotationAngle.Rotate90`). |
| **¿Existe una forma de recortar usando porcentajes en lugar de puntos absolutos?** | Sí—calcula las dimensiones del rectángulo basándote en `image.Width * 0.25`, etc., y luego conviértelas a puntos como se muestra en el Paso 4. |

---

## Ejemplo Completo (Listo para Copiar‑Pegar)

```csharp
using System;
using System.IO;
using Aspose.Pdf;

namespace CropImageInPdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new PDF document and add a blank page
            Document pdf = new Document();
            Page page = pdf.Pages.Add();

            // 2️⃣ Open the image that will be placed on the page
            using (FileStream imgStream = new FileStream("YOUR_DIRECTORY/image.jpg", FileMode.Open))
            {
                // 3️⃣ Define where the image will sit on the page (points)
                Rectangle placement = new Rectangle(0, 0, 600, 800);

                // 4️⃣ Define the crop area – upper‑left quarter of the image
                Rectangle crop = new Rectangle(0, 0, placement.Width / 2, placement.Height / 2);

                // 5️⃣ Add the image using both placement and crop rectangles
                page.AddImage(imgStream, placement, crop);
            }

            // (Optional) Save the PDF to verify the result
            pdf.Save("YOUR_DIRECTORY/output.pdf");

            Console.WriteLine("PDF created and image cropped successfully!");
        }
    }
}
```

Ejecuta el programa, abre `output.pdf`, y verás solo el cuarto superior‑izquierdo de `image.jpg` renderizado en la esquina superior‑izquierda de la página. Cambia los valores del rectángulo `crop` para experimentar con diferentes porciones.

---

## Conclusión

Hemos recorrido todo el proceso de **recortar imagen en pdf** usando Aspose.PDF para C#. Partiendo de un documento nuevo, **creamos pdf con imagen**, demostramos el **cómo añadir imagen a pdf**, aplicamos un rectángulo personalizado de **cómo recortar imagen pdf**, y finalmente **guardamos pdf con imagen**.  

Ahora puedes incrustar imágenes recortadas con precisión en cualquier PDF que generes—perfecto para facturas, folletos de marketing o informes automatizados. A continuación, considera añadir subtítulos de texto (`TextFragment`) o dibujar formas alrededor de la imagen recortada para resaltarla aún más.  

¿Tienes más escenarios que te intrigan? Deja un comentario, ¡y feliz codificación!

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo establecer el tamaño de la imagen en un PDF usando Aspose.PDF para .NET](/pdf/english/net/images-graphics/set-image-size-pdf-aspose-dotnet/)
- [Cómo añadir una marca de imagen a un PDF usando Aspose.PDF para .NET: Guía completa](/pdf/english/net/images-graphics/add-image-stamp-pdf-aspose-dotnet/)
- [Cómo extraer información de imágenes de PDFs usando Aspose.PDF para .NET](/pdf/english/net/images-graphics/extract-image-info-pdf-aspose-pdf-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}