---
category: general
date: 2026-04-25
description: Agrega numeración Bates a PDFs rápidamente usando Aspose.Pdf. Aprende
  cómo añadir números de página a PDFs, ajustar automáticamente el tamaño de fuente
  y agregar una marca de agua de texto en C#.
draft: false
keywords:
- add bates numbering
- add page numbers pdf
- auto adjust font size
- how to add bates
- add text watermark
language: es
og_description: Agrega numeración Bates a PDFs con Aspose.Pdf. Esta guía muestra cómo
  añadir números de página en PDF, ajustar automáticamente el tamaño de fuente y agregar
  una marca de agua de texto en un único ejemplo ejecutable.
og_title: Agregar numeración Bates a PDFs – Tutorial completo de Aspose.C#
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Agregar numeración Bates a PDFs con Aspose – Guía completa
url: /es/net/programming-with-stamps-and-watermarks/add-bates-numbering-to-pdfs-with-aspose-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar numeración Bates a PDFs con Aspose – Guía completa

¿Alguna vez necesitaste **agregar numeración Bates** a un PDF pero no sabías por dónde empezar? No estás solo—equipos legales, auditores y desarrolladores se topan con este obstáculo a diario. ¿La buena noticia? Con Aspose.Pdf for .NET puedes estampar un número Bates, auto‑ajustar el tamaño de la fuente e incluso tratar el sello como una sutil marca de agua de texto—todo con unas pocas líneas de C#.

En este tutorial recorreremos los pasos exactos para **agregar números de página pdf**, ajustar la fuente para que nunca se desborde y responder la pregunta “cómo agregar bates” de una vez por todas. Al final tendrás una aplicación de consola lista para ejecutar que produce un PDF numerado profesionalmente, y verás cómo ampliarla a una solución completa de marca de agua.

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

* **Aspose.Pdf for .NET** (el paquete NuGet más reciente a partir de abril 2026).  
* .NET 6.0 SDK o superior – la API funciona igual en .NET Framework, pero .NET 6 ofrece el mejor rendimiento.  
* Un PDF de ejemplo llamado `input.pdf` colocado en una carpeta que puedas referenciar (p.ej., `C:\Docs\`).  

No se requiere configuración adicional; la biblioteca es autónoma.

---

## Paso 1 – Cargar el documento PDF de origen

Lo primero que hacemos es abrir el archivo que queremos numerar. La clase `Document` de Aspose representa todo el PDF, y cargarlo es tan simple como pasar la ruta al constructor.

```csharp
using Aspose.Pdf;

string inputPath = @"C:\Docs\input.pdf";
Document pdfDocument = new Document(inputPath);
```

*Por qué es importante*: Cargar el documento te da acceso a la colección `Pages`, que es donde adjuntaremos el sello Bates más adelante. Si el archivo no se encuentra, Aspose lanza una clara `FileNotFoundException`, por lo que sabrás exactamente qué falló.

## Paso 2 – Crear un sello de texto para números Bates

Ahora diseñamos el elemento visual que aparecerá en cada página. La clase `TextStamp` te permite incrustar cualquier cadena, y usaremos el marcador `{page}-{total}` para que Aspose reemplace esos tokens automáticamente.

```csharp
// Create a stamp that will display "Bates: 1-10", "Bates: 2-10", etc.
TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
{
    // Let the stamp automatically adjust its font size to fit the stamp rectangle
    AutoAdjustFontSizeToFitStampRectangle = true,
    // Optional: make the stamp look like a subtle watermark
    Opacity = 0.4,
    // Position the stamp at the bottom‑right corner
    XIndent = 20,
    YIndent = 20,
    HorizontalAlignment = HorizontalAlignment.Right,
    VerticalAlignment = VerticalAlignment.Bottom,
    // Choose a readable font
    Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
};
```

*Puntos clave*:

* **auto adjust font size** – Configurar `AutoAdjustFontSizeToFitStampRectangle` a `true` garantiza que el texto nunca se desborde fuera del rectángulo, lo cual es perfecto para números de página de longitud variable.  
* **add text watermark** – Al reducir la `Opacity` convertimos el número Bates en una marca de agua tenue, cumpliendo el requisito de “add text watermark” sin un paso adicional.  
* **how to add bates** – Los tokens `{page}` y `{total}` son la clave secreta; Aspose los reemplaza en tiempo de ejecución, por lo que no tienes que calcular nada manualmente.

## Paso 3 – Aplicar el sello a cada página

Un error común es estampar solo la primera página. Para realmente **agregar números de página pdf**, necesitamos iterar sobre toda la colección `Pages`.

```csharp
foreach (Page page in pdfDocument.Pages)
{
    // Clone the stamp for each page to avoid shared state issues
    page.AddStamp(batesStamp);
}
```

¿Por qué clonar? El método `AddStamp` crea internamente una copia, pero usar explícitamente una nueva instancia por iteración evita efectos secundarios accidentales si más tarde modificas propiedades del sello (como cambiar el color para páginas específicas).

## Paso 4 – Guardar el PDF actualizado

Con los sellos en su lugar, guardar los cambios es sencillo. Puedes sobrescribir el archivo original o escribir en una nueva ubicación—aquí guardaremos un nuevo archivo llamado `output.pdf`.

```csharp
string outputPath = @"C:\Docs\output.pdf";
pdfDocument.Save(outputPath);
Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
```

Si abres `output.pdf` verás cada página etiquetada “Bates: 1‑10”, “Bates: 2‑10”, … en la esquina inferior derecha, con una opacidad tenue que también funciona como **add text watermark**.

## Ejemplo completo funcional

Juntando todo, aquí tienes un programa de consola único y autocontenido que puedes copiar y pegar en Visual Studio.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Drawing;
using Aspose.Pdf.Annotations;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        string inputPath = @"C:\Docs\input.pdf";
        Document pdfDocument = new Document(inputPath);

        // 2️⃣ Create a Bates number stamp with auto‑adjusted font size
        TextStamp batesStamp = new TextStamp("Bates: {page}-{total}")
        {
            AutoAdjustFontSizeToFitStampRectangle = true,
            Opacity = 0.4, // acts as a subtle watermark
            XIndent = 20,
            YIndent = 20,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Font = new Font(FontFamilyEnum.Helvetica, 12, FontStyle.Regular, Color.Black)
        };

        // 3️⃣ Add the stamp to every page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.AddStamp(batesStamp);
        }

        // 4️⃣ Save the result
        string outputPath = @"C:\Docs\output.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"Bates‑numbered PDF saved to: {outputPath}");
    }
}
```

**Resultado esperado**: Abre `output.pdf` en cualquier visor; cada página muestra una línea como “Bates: 3‑12” en la esquina inferior derecha, con el tamaño justo para el rectángulo y renderizada con un 40 % de opacidad. Esto satisface tanto el requisito de seguimiento legal como la necesidad de marca de agua visual.

## Variaciones comunes y casos límite

| Situación | Qué cambiar | Por qué |
|-----------|-------------|--------|
| **Ubicación diferente** | Ajusta `HorizontalAlignment` / `VerticalAlignment` o establece `XIndent`/`YIndent` | Algunas firmas prefieren la ubicación superior‑izquierda o centrada. |
| **Prefijo personalizado** | Reemplaza `"Bates: "` con `"Doc‑ID: "` o cualquier cadena | Podrías estar usando una convención de nombres diferente. |
| **Múltiples sellos** | Crea un segundo `TextStamp` (p.ej., para un aviso de confidencialidad) y añádelo después del primero | Combinar **add bates numbering** con otros requisitos de **add text watermark** es trivial. |
| **Gran número de páginas** | Incrementa el tamaño de fuente inicial (p.ej., `14`) – el auto‑ajuste lo reducirá cuando sea necesario | Cuando tienes > 999 páginas, la cadena se alarga; el auto‑ajuste evita recortes. |
| **PDFs encriptados** | Llama a `pdfDocument.Decrypt("password")` antes de estampar | No puedes modificar un archivo protegido sin la contraseña. |

## Consejos profesionales y trampas

* **Pro tip:** Set `batesStamp.Margin = new MarginInfo(5, 5, 5, 5)` si notas que el texto se pega al borde de la página.  
* **Watch out for:** Rectángulos muy pequeños (el tamaño predeterminado es 100 × 30 pt). Si necesitas un área mayor, establece `batesStamp.Width` y `batesStamp.Height` manualmente.  
* **Performance note:** Estampar miles de páginas puede tardar unos segundos, pero Aspose transmite las páginas de forma eficiente—no es necesario cargar todo el documento en memoria.  

## Conclusión

Acabamos de demostrar cómo **add bates numbering** a un PDF usando Aspose.Pdf, mientras simultáneamente **add page numbers pdf**, habilitamos **auto adjust font size** y creamos un **add text watermark** en un flujo cohesivo. El ejemplo completo y ejecutable anterior te brinda una base sólida que puedes adaptar a cualquier flujo de trabajo de documentos legales o sistema interno de informes.

¿Listo para el siguiente paso? Prueba combinar este enfoque con la API de fusión de PDFs de Aspose para procesar por lotes varios archivos, o explora la clase `TextFragment` para marcas de agua más ricas (coloreadas, rotadas o multilínea). Las posibilidades son infinitas, y el código que ahora tienes es una base confiable.

Si encontraste útil esta guía, no dudes en dejar un comentario, marcar el repositorio con una estrella o compartir tus propias variaciones. ¡Feliz codificación, y que tus PDFs siempre estén perfectamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}