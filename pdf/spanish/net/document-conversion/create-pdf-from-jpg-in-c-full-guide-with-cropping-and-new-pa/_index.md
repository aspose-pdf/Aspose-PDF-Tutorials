---
category: general
date: 2026-04-06
description: Crea PDF a partir de JPG rápidamente y aprende cómo recortar la imagen
  en PDF, agregar una nueva página PDF y convertir JPG a PDF con recorte usando C#.
draft: false
keywords:
- create pdf from jpg
- crop image in pdf
- how to add new pdf page
- convert jpg to pdf with crop
- insert image into pdf c#
language: es
og_description: Crear PDF a partir de JPG y recortar la imagen en el PDF con C#. Aprende
  a agregar una nueva página PDF y convertir JPG a PDF con recorte.
og_title: Crear PDF a partir de JPG en C# – Guía paso a paso
tags:
- Aspose.Pdf
- C#
- PDF generation
title: Crear PDF a partir de JPG en C# – Guía completa con recorte y nuevas páginas
url: /es/net/document-conversion/create-pdf-from-jpg-in-c-full-guide-with-cropping-and-new-pa/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF a partir de JPG en C# – Guía completa con recorte y nuevas páginas

¿Alguna vez necesitaste **crear PDF a partir de JPG** pero no estabas seguro de cómo conservar solo la parte que realmente deseas? No estás solo. En muchas aplicaciones —piensa en facturas, recibos o libros de fotos— los desarrolladores deben convertir una imagen en un PDF descartando los bordes no deseados.  

En este tutorial recorreremos una solución completa y lista para ejecutar que **crea PDF a partir de JPG**, te muestra cómo **recortar una imagen en PDF**, y demuestra el **cómo agregar una nueva página PDF** cuando necesitas más de una foto. Al final también sabrás cómo **convertir JPG a PDF con recorte** y **insertar imagen en PDF C#** usando la biblioteca Aspose.Pdf.

## Qué aprenderás

- Configurar Aspose.Pdf en un proyecto .NET (sin configuración pesada).  
- Cargar un JPEG, definir el área que deseas conservar y recortarla al insertarla en una página PDF.  
- Añadir páginas adicionales al mismo documento, permitiéndote crear PDFs de varias páginas a partir de muchas imágenes.  
- Guardar el archivo final y verificar el resultado.  

**Requisitos previos:** .NET 6+ (o .NET Framework 4.6+), Visual Studio 2022 o cualquier editor que prefieras, y una referencia NuGet a `Aspose.Pdf`. No se necesitan otros servicios externos.

![Ejemplo de crear PDF a partir de JPG](image.jpg){: .align-center alt="Ejemplo de crear PDF a partir de JPG que muestra una imagen recortada colocada en una página PDF"}

---

## Paso 1: Instalar Aspose.Pdf y preparar tu proyecto

Lo primero, agrega el paquete Aspose.Pdf. Abre una terminal en la carpeta de tu solución y ejecuta:

```bash
dotnet add package Aspose.Pdf
```

Esa única línea descarga todo lo que necesitas: las clases `Document`, `Rectangle` y `Page` que usaremos más adelante. En mi experiencia, la vía NuGet es la forma más limpia de mantenerse actualizado sin manipular DLLs.

> **Consejo profesional:** Si estás apuntando a .NET Framework, usa el paquete `Aspose.Pdf.NET` en su lugar; la superficie de la API es idéntica.

---

## Paso 2: Cargar el JPEG y definir el tamaño de la página

Necesitamos un lienzo que coincida con las dimensiones que queremos para la página PDF final. El código a continuación crea un nuevo `Document` y abre la imagen de origen como un flujo.

```csharp
using Aspose.Pdf;
using System.IO;

// Create a new PDF document – this will hold our pages.
using var pdfDocument = new Document();

// Open the JPEG you want to convert.
using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

// Define the full‑size rectangle (the page) – 600 × 800 points works well for most photos.
var pageBounds = new Rectangle(0, 0, 600, 800);
```

¿Por qué un rectángulo? En Aspose.Pdf un `Rectangle` representa tanto las dimensiones de la página como la región de la imagen que deseas mostrar. Al separar la *página* del *área de recorte* obtienes un control granular sobre lo que termina en el PDF.

---

## Paso 3: Elegir el área de recorte (cuadrante superior‑izquierdo)

Supongamos que solo necesitas el cuadrante superior‑izquierdo de la foto. Calculamos esa región en relación con el tamaño de la página:

```csharp
// Crop the upper‑left quarter of the image.
var cropArea = new Rectangle(
    pageBounds.LLX,                                 // left X (0)
    pageBounds.LLY + pageBounds.Height / 2,         // bottom Y (halfway up)
    pageBounds.LLX + pageBounds.Width / 2,          // right X (halfway across)
    pageBounds.URY);                                // top Y (full height)
```

El constructor de `Rectangle` recibe los valores **X/Y inferior‑izquierdo** y **X/Y superior‑derecho**. Al añadir la mitad de la altura a `LLY` desplazamos la parte inferior del recorte hacia arriba, descartando efectivamente la mitad inferior de la imagen. Ajusta estos cálculos si necesitas una porción diferente.

> **¿Por qué recortar antes de agregar?**  
> Recortar del lado del PDF evita crear un bitmap temporal en disco, ahorrando tanto I/O como memoria. Aspose maneja los cálculos por ti, y el resultado es un PDF limpio y amigable con vectores.

---

## Paso 4: Añadir una nueva página e insertar la imagen recortada

Ahora realmente colocamos la imagen en una página PDF. Aquí es donde brilla la palabra clave **how to add new pdf page**.

```csharp
// Add a new page to the document.
var page = pdfDocument.Pages.Add();

// Insert the image using both the page bounds and the crop rectangle.
page.AddImage(imageStream, pageBounds, cropArea);
```

`AddImage` recibe tres argumentos:

1. **Stream** – el JPEG de origen.  
2. **Page rectangle** – define el tamaño de la página (nuestro `pageBounds`).  
3. **Crop rectangle** – indica a Aspose qué parte de la imagen renderizar.

Si necesitas más páginas, simplemente repite el patrón `Add` + `AddImage` con un nuevo `imageStream` cada vez. Esto satisface el requisito de **how to add new pdf page** mientras mantiene el código ordenado.

---

## Paso 5: Guardar el PDF y verificar el resultado

El paso final es una sola línea, pero no lo subestimes: guardar en la ruta correcta garantiza que el archivo pueda abrirse con cualquier visor de PDF.

```csharp
// Save the PDF to disk.
pdfDocument.Save(@"C:\Output\cropped_image.pdf");

// Optional: open the file automatically (Windows only).
System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
```

Al abrir `cropped_image.pdf`, deberías ver una sola página que contiene solo el cuadrante superior‑izquierdo del JPEG original, perfectamente centrado dentro de la página de 600 × 800.

---

## Ejemplo completo (todos los pasos combinados)

A continuación se muestra el programa completo que puedes copiar y pegar en una aplicación de consola. Compila tal cual, asumiendo que has instalado Aspose.Pdf y colocado un JPEG en la ubicación especificada.

```csharp
using Aspose.Pdf;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document.
        using var pdfDocument = new Document();

        // 2️⃣ Open the source JPEG.
        using var imageStream = File.OpenRead(@"C:\Images\photo.jpg");

        // 3️⃣ Define the page size (600 × 800 points).
        var pageBounds = new Rectangle(0, 0, 600, 800);

        // 4️⃣ Calculate the crop area – upper‑left quarter.
        var cropArea = new Rectangle(
            pageBounds.LLX,
            pageBounds.LLY + pageBounds.Height / 2,
            pageBounds.LLX + pageBounds.Width / 2,
            pageBounds.URY);

        // 5️⃣ Add a new page and insert the cropped image.
        var page = pdfDocument.Pages.Add();
        page.AddImage(imageStream, pageBounds, cropArea);

        // 6️⃣ Save the resulting PDF.
        pdfDocument.Save(@"C:\Output\cropped_image.pdf");

        // 7️⃣ (Optional) Open the PDF automatically.
        System.Diagnostics.Process.Start(@"C:\Output\cropped_image.pdf");
    }
}
```

### Resultado esperado

- **Archivo:** `cropped_image.pdf` (≈ 30 KB).  
- **Contenido:** Una página, 600 × 800 puntos, mostrando el cuadrante superior‑izquierdo de `photo.jpg`.  
- **Comportamiento:** Sin distorsión; la imagen conserva su resolución original dentro de los límites recortados.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si necesito conservar la imagen completa, no solo un cuarto?

Simplemente establece `cropArea` igual a `pageBounds`:

```csharp
var cropArea = pageBounds; // No cropping – full image.
```

### ¿Puedo usar un tamaño de página diferente (p. ej., A4)?

Claro. Reemplaza los valores de `pageBounds` con las dimensiones de una página A4 en puntos (595 × 842):

```csharp
var pageBounds = new Rectangle(0, 0, 595, 842);
```

El rectángulo de recorte puede permanecer igual o recalcularse para coincidir con la nueva relación de aspecto.

### ¿Cómo añado múltiples imágenes, cada una en su propia página?

Itera sobre una colección de rutas de archivo:

```csharp
foreach (var path in imagePaths)
{
    using var stream = File.OpenRead(path);
    var page = pdfDocument.Pages.Add();
    page.AddImage(stream, pageBounds, pageBounds); // No crop for each image.
}
```

### ¿Qué pasa con la transparencia o imágenes PNG?

Aspose.Pdf trata los PNG de la misma manera que los JPEG. Si la fuente tiene un canal alfa, el PDF lo preservará, siempre que la versión del PDF admita transparencia (el valor predeterminado está bien).

### ¿Funciona esto en .NET Core en Linux?

Sí. Aspose.Pdf es multiplataforma; solo asegúrate de que `imageStream` apunte a una ruta de archivo válida en el sistema operativo de destino. No se utilizan APIs exclusivas de Windows.

---

## Consejos y buenas prácticas

- **Gestión de memoria:** Siempre envuelve los streams en sentencias `using` (como se muestra) para evitar bloqueos de archivos.  
- **Rendimiento:** Si procesas decenas de imágenes, considera reutilizar una única instancia de `Document` y llamar a `pdfDocument.Pages.Add()` para cada imagen.  
- **Manejo de errores:** Envuelve toda la rutina en un bloque `try/catch` y registra `PdfException` para la solución de problemas.  
- **Control de calidad:** Aspose.Pdf permite establecer la resolución de la imagen mediante `ImageFragment`. Para escaneos de alta DPI, establece `ImageFragment.Resolution = 300;`.  
- **Seguridad:** Si el PDF se compartirá externamente, puedes añadir cifrado con `pdfDocument.Encrypt("ownerPwd", "userPwd", Permission.All);`.

---

## Conclusión

Acabamos de cubrir cómo **crear PDF a partir de JPG** en C#, **recortar una imagen en PDF**, y **añadir una nueva página PDF** para crear documentos multipágina. El mismo patrón te permite **convertir JPG a PDF con recorte** y **insertar imagen en PDF C#** para cualquier escenario, desde recibos simples hasta libros de fotos complejos.  

Pruébalo: cambia la lógica de recorte, experimenta con páginas A4 o encadena varias imágenes. La biblioteca Aspose.Pdf hace que estas tareas sean sencillas, y el código anterior es una referencia sólida y digna de citar que puedes pegar en cualquier proyecto.

---

### ¿Qué sigue?

- **Añadir anotaciones de texto** al PDF (p. ej., subtítulos bajo cada imagen).  
- **Crear una tabla de contenidos** automáticamente para PDFs multipágina.  
- **Combinar varios PDFs** usando `pdfDocument.Pages.AddRange(otherDoc.Pages);`.  

Cada uno de esos temas se basa en los fundamentos que acabas de dominar, por lo que estás bien posicionado para explorarlos

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}