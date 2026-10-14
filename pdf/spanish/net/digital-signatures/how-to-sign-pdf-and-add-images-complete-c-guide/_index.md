---
category: general
date: 2026-03-29
description: Cómo firmar un PDF con una firma digital y añadir una imagen recortada
  en C#. Aprende a agregar una firma digital al PDF, recortar una imagen para el PDF
  y añadir una imagen al PDF fácilmente.
draft: false
keywords:
- how to sign pdf
- add digital signature pdf
- crop image for pdf
- add image to pdf
- digital signature pdf page
language: es
og_description: Cómo firmar un PDF con una firma digital e incrustar una imagen recortada
  usando Aspose.Pdf en C#. Sigue esta guía para una solución completa.
og_title: Cómo firmar PDF y agregar imágenes – Tutorial paso a paso en C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Cómo firmar PDF y agregar imágenes – Guía completa de C#
url: /es/net/digital-signatures/how-to-sign-pdf-and-add-images-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo firmar PDF y agregar imágenes – Guía completa en C#

¿Alguna vez te has preguntado **cómo firmar PDF** de forma programática mientras insertas una imagen personalizada? Tal vez estés construyendo un flujo de aprobación y necesites una firma legalmente vinculante *y* una miniatura de la foto del firmante en la misma página. En resumen, quieres **agregar firma digital pdf** al contenido, recortar esa foto y luego **agregar imagen a pdf** sin complicaciones.  

Este tutorial te guía paso a paso—desde cargar un certificado ECDSA PKCS#7 hasta recortar un JPEG y estamparlo en la página firmada. Al final tendrás un único archivo C# ejecutable que firma la página 1, recorta una foto a 400 × 400 px y la coloca en una ubicación precisa. Sin scripts externos, sin trucos, solo código claro y explicaciones.

## Requisitos previos

- .NET 6.0 o superior (el código también funciona con .NET Framework 4.7+)
- Paquete NuGet **Aspose.Pdf for .NET** (versión 23.9 o más reciente)
- Un certificado ECDSA P‑256 en formato PKCS#7 (`.pfx`) y su contraseña
- Una imagen JPEG que desees incrustar (p. ej., `photo.jpg`)

> **Consejo profesional:** Mantén tu archivo de certificado fuera del control de versiones y protege la contraseña con un gestor de secretos.

---

## Paso 1: Configurar el proyecto e importaciones

Primero, crea una aplicación de consola (o intégrala en cualquier servicio existente). Añade la referencia a Aspose.Pdf:

```bash
dotnet add package Aspose.Pdf
```

Luego incluye los espacios de nombres requeridos:

```csharp
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;
```

Estas sentencias `using` te dan acceso a las clases `Document`, `Signature` y `Rectangle` que necesitaremos más adelante.

## Paso 2: Cargar el PDF y preparar la firma

Abriremos un PDF existente (`source.pdf`) y crearemos un objeto **digital signature pdf** que usa una firma PKCS#7 separada. El certificado es una clave ECDSA P‑256, ampliamente aceptada para cumplimiento.

```csharp
// Load the PDF you want to sign
var doc = new Document("YOUR_DIRECTORY/source.pdf");

// Initialize the signature appearance (optional but recommended)
var signature = new Signature(doc);
signature.Contact = "John Doe";
signature.Location = "New York, USA";
signature.Reason = "Document approval";

// Load the PKCS#7 certificate (ECDSA P‑256) for signing
var pkcsSignature = new PKCS7Detached(
    "YOUR_DIRECTORY/ecdsa.pfx",   // certificate file
    "YOUR_PASSWORD");             // certificate password
```

**Por qué es importante:** Usar una firma PKCS#7 separada mantiene intacto el contenido original del PDF mientras se incrusta un hash criptográfico. Este es el enfoque estándar de la industria para PDFs legalmente vinculantes.

## Paso 3: Aplicar la firma digital a una página específica

Ahora colocaremos el campo de firma visible en **la página 1**. El rectángulo define dónde aparece el cuadro de firma (las coordenadas están en puntos, donde 1 pulgada = 72 puntos).

```csharp
// Apply the digital signature to page 1, covering a rectangular area
signature.Sign(
    pageNumber: 1,
    isVisible: true,
    signatureRect: new Rectangle(100, 100, 300, 300),
    pkcsSignature);
```

Si no necesitas un cuadro visible, establece `isVisible` a `false`. El `signatureRect` puede ajustarse para que coincida con el diseño de tu documento.

## Paso 4: Abrir el flujo de imagen y definir áreas de recorte

Leemos el archivo JPEG en un flujo y especificamos un **rectángulo de origen** que selecciona los 400 × 400 píxeles superiores‑izquierdos. Esta es la operación **crop image for pdf**.

```csharp
// Open the image file that will be added to the PDF
using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

// Define the source rectangle that selects the portion to crop (0‑400 pixels)
var sourceRect = new Rectangle(0, 0, 400, 400);
```

> **Caso límite:** Si tu imagen es más pequeña que 400 × 400, el recorte se ajustará automáticamente a las dimensiones reales de la imagen—no se lanzará ninguna excepción.

## Paso 5: Definir dónde debe aparecer la imagen recortada

A continuación, establecemos el **rectángulo de destino** en la página PDF. En este ejemplo colocamos la imagen en (50, 50) con un tamaño de 200 × 200 puntos (≈2.78 pulgadas cuadradas).

```csharp
// Define the destination rectangle where the cropped image will be placed on the page
var destinationRect = new Rectangle(50, 50, 200, 200);
```

Siéntete libre de experimentar: cambia las coordenadas X/Y para mover la foto, o ajusta ancho/alto para escalarla.

## Paso 6: Insertar la imagen recortada en la página firmada

Finalmente, añadimos la imagen a **la página 1** (la misma página que ahora lleva la firma). La sobrecarga `AddImage` que usamos acepta los rectángulos de origen y destino, realizando el recorte y la colocación en una sola llamada.

```csharp
// Insert the cropped image onto page 1 at the specified location
doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);
```

Detrás de escena, Aspose.Pdf extrae la región de 400 × 400 píxeles, la reescala a 200 × 200 puntos y la escribe en el flujo de contenido del PDF.

## Paso 7: Guardar el PDF firmado y con la imagen añadida

Después de todas las modificaciones, persiste el documento. Puedes sobrescribir el archivo original o escribir a uno nuevo.

```csharp
// Save the final document
doc.Save("YOUR_DIRECTORY/output_signed.pdf");
Console.WriteLine("PDF signed and image added successfully!");
```

Al abrir `output_signed.pdf` en Adobe Acrobat o cualquier visor de PDF, verás:

- Un campo de firma visible en las coordenadas que especificaste.
- La foto recortada colocada en (50, 50) en la página 1.
- La firma digital validada (si el visor confía en tu certificado).

---

## Preguntas frecuentes (FAQ)

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo firmar una página diferente?** | Cambia el argumento `pageNumber` en `signature.Sign` a cualquier índice de página válido (basado en 1). |
| **¿Qué pasa si necesito varias firmas?** | Crea una nueva instancia de `Signature` para cada página o ubicación, reutilizando el mismo `pkcsSignature` si se aplica el mismo certificado. |
| **¿El recorte de imagen está limitado a rectángulos?** | Sí, `AddImage` de Aspose.Pdf funciona con regiones rectangulares. Para formas complejas deberás pre‑procesar la imagen (p. ej., con System.Drawing) antes de incrustarla. |
| **¿Cómo hago que la firma sea invisible?** | Establece `isVisible` a `false` y omite `signatureRect`. La firma seguirá siendo criptográficamente válida. |
| **¿Qué formatos puedo incrustar además de JPEG?** | PNG, BMP, GIF y TIFF son compatibles. Simplemente cambia la ruta del archivo y asegura que el flujo lea los bytes correctos. |

---

## Ejemplo completo y funcional

A continuación tienes el programa completo, autocontenido. Copia‑pega en `Program.cs`, ajusta las rutas y ejecútalo.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using Aspose.Pdf.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        var doc = new Document("YOUR_DIRECTORY/source.pdf");

        // 2️⃣ Prepare the digital signature appearance
        var signature = new Signature(doc)
        {
            Contact = "John Doe",
            Location = "New York, USA",
            Reason = "Document approval"
        };

        // 3️⃣ Load the PKCS#7 ECDSA P‑256 certificate
        var pkcsSignature = new PKCS7Detached(
            "YOUR_DIRECTORY/ecdsa.pfx",
            "YOUR_PASSWORD");

        // 4️⃣ Apply a visible signature on page 1
        signature.Sign(
            pageNumber: 1,
            isVisible: true,
            signatureRect: new Rectangle(100, 100, 300, 300),
            pkcsSignature);

        // 5️⃣ Open the image to be added
        using var imageStream = File.OpenRead("YOUR_DIRECTORY/photo.jpg");

        // 6️⃣ Define crop (source) and placement (destination) rectangles
        var sourceRect = new Rectangle(0, 0, 400, 400);      // crop 400×400 px from top‑left
        var destinationRect = new Rectangle(50, 50, 200, 200); // place at (50,50) with 200×200 pt size

        // 7️⃣ Insert the cropped image onto the same page
        doc.Pages[1].AddImage(imageStream, sourceRect, destinationRect);

        // 8️⃣ Save the final PDF
        doc.Save("YOUR_DIRECTORY/output_signed.pdf");
        Console.WriteLine("PDF signed and image added successfully!");
    }
}
```

**Resultado esperado:** Al abrir `output_signed.pdf` se muestra un campo de firma (100 × 100 → 300 × 300 puntos) y una imagen de 200 × 200 puntos derivada de la esquina superior‑izquierda de `photo.jpg`. La firma se valida contra el certificado ECDSA suministrado.

---

## Conclusión

Hemos cubierto **cómo firmar PDF**, cómo **agregar digital signature pdf** a una página específica, cómo **crop image for pdf**, y finalmente cómo **add image to pdf** usando Aspose.Pdf en C#. Todo el flujo—desde cargar el certificado hasta guardar el documento final—cabe en un solo archivo fuente fácil de leer.

Si estás listo para el siguiente reto, considera:

- Añadir **múltiples firmas** en diferentes páginas (usa el concepto “digital signature pdf page”).
- Incrustar **códigos QR** que enlacen a servicios de verificación.
- Automatizar el proceso en una API ASP.NET Core para generación de PDF bajo demanda.

Recuerda, la clave para una automatización robusta de PDFs es la separación clara de responsabilidades: manejo de firmas, procesamiento de imágenes y ensamblado final del documento. Juega con las coordenadas, cambia el formato de la imagen o experimenta con sellos de tiempo—tu flujo de trabajo ahora es totalmente extensible.

¿Tienes preguntas, casos límite o un uso interesante que compartir? ¡Deja un comentario abajo y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}