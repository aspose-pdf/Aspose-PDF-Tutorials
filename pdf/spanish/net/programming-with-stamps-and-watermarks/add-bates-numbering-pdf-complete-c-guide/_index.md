---
category: general
date: 2026-02-14
description: Agrega numeración Bates en PDF a tus documentos sin esfuerzo. Aprende
  cómo añadir números de página en el pie de página y numeración secuencial en PDF
  con Aspose.Pdf en minutos.
draft: false
keywords:
- add bates numbering pdf
- add footer page numbers
- how to add bates numbers
- add sequential numbers pdf
language: es
og_description: Añade numeración Bates a PDF rápidamente. Esta guía muestra cómo agregar
  números de página en el pie de página y números secuenciales a PDF usando Aspose.Pdf,
  con código completo y consejos.
og_title: Agregar numeración Bates a PDF – Tutorial paso a paso en C#
tags:
- Aspose.Pdf
- C#
- PDF automation
title: Añadir numeración Bates a PDF – Guía completa de C#
url: /es/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-c-guide/
---

: fenced code blocks. But these placeholders are not fenced. Probably they are placeholders for code blocks inserted later. Should keep them as is.

We need to translate everything else.

Let's produce final content.

Be careful to keep markdown formatting: headings, lists, blockquotes.

Translate sentences.

Let's do it.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir numeración Bates a PDF – Guía completa en C#

¿Alguna vez necesitaste **añadir numeración Bates a archivos PDF** pero no sabías por dónde empezar? No estás solo. Los equipos legales, auditores y cualquier persona que maneje grandes conjuntos de documentos preguntan constantemente: “¿Cómo añado números Bates sin romper el diseño?” La buena noticia es que con Aspose.Pdf para .NET puedes insertar esos números como un simple pie de página—sin necesidad de edición manual.

En este tutorial recorreremos una solución práctica, de extremo a extremo, que no solo **añade números de página en el pie de página**, sino que también te permite **añadir números secuenciales a PDF** con un prefijo personalizado, tamaño de fuente y alineación. Al final tendrás un programa C# listo para ejecutar, una comprensión clara de por qué cada configuración es importante y algunos consejos profesionales para evitar los errores más comunes.

## Lo que aprenderás

- Cómo cargar un PDF existente y prepararlo para la numeración Bates.  
- Qué propiedades de **BatesNumberingOptions** controlan la apariencia y la posición.  
- Cómo aplicar la numeración a cada página en una sola llamada.  
- Formas de personalizar el prefijo, el número inicial y los márgenes para diferentes formatos legales.  
- Manejo de casos extremos—qué hacer con PDFs encriptados o documentos que ya contienen pies de página.

**Requisitos previos**: .NET 6+ (o .NET Framework 4.7+), una versión reciente de Aspose.Pdf (el ejemplo usa la 23.10) y un PDF de entrada del que tengas derechos de modificación. No se necesitan otras bibliotecas de terceros.

---

## Paso 1 – Cargar el PDF que deseas numerar

Lo primero que hacemos es crear una instancia de `Document` que apunte al archivo fuente. Usar el patrón `using var` garantiza que el manejador del archivo se libere automáticamente.

```csharp
using Aspose.Pdf;

// Replace with the path to your source PDF
using var doc = new Document("YOUR_DIRECTORY/input.pdf");
```

> **Por qué es importante:** Aspose.Pdf lee toda la estructura del PDF en memoria, lo que nos permite manipular páginas, anotaciones y metadatos sin tocar el archivo original en disco. Si el PDF está protegido con contraseña, puedes pasar la contraseña al constructor—consulta la nota “PDFs encriptados” al final.

---

## Paso 2 – Definir tus opciones de numeración Bates

Los números Bates son esencialmente pies de página con un prefijo configurable y un contador secuencial. La clase `BatesNumberingOptions` te permite afinar cada aspecto visual.

```csharp
var batesOptions = new BatesNumberingOptions
{
    // The text that will appear before the numeric part
    Prefix = "ABC-",

    // Starting number; the library will increment this automatically
    StartNumber = 1000,

    // Font size of the footer text (points)
    FontSize = 12,

    // Align the number to the right side of the page
    HorizontalAlignment = HorizontalAlignment.Right,

    // Place the number at the bottom of the page
    VerticalAlignment = VerticalAlignment.Bottom,

    // Margins: left, top, right, bottom (in points)
    Margin = new MarginInfo(0, 20, 0, 0)
};
```

### Consejo rápido

- **Prefix**: Usa un identificador corto y único (p. ej., número de caso) para que el pie de página sea legible.  
- **StartNumber**: Los despachos legales suelen comenzar en `1` o con un desplazamiento personalizado; elige lo que coincida con tu sistema de archivo.  
- **Margins**: Un margen inferior de `20` puntos mantiene el texto alejado de notas al pie o firmas que ya puedan estar cerca del borde de la página.

---

## Paso 3 – Aplicar la numeración a todas las páginas

Con las opciones configuradas, la inyección real es una sola línea. Aspose.Pdf gestiona la paginación, actualiza los flujos de contenido existentes y respeta la rotación de la página automáticamente.

```csharp
doc.Pages.AddBatesNumbering(batesOptions);
```

> **¿Qué ocurre tras bambalinas?** La biblioteca itera sobre cada objeto `Page`, crea un `TextFragment` que incorpora el prefijo y el contador actual, y luego lo dibuja usando el sistema de coordenadas de la página. Como establecimos `HorizontalAlignment.Right` y `VerticalAlignment.Bottom`, el texto se ancla a la esquina inferior‑derecha sin importar el tamaño de la página.

---

## Paso 4 – Guardar el PDF modificado

Finalmente, escribe el resultado en un nuevo archivo. Sobrescribir el original es posible, pero conservar una copia ayuda con el control de versiones.

```csharp
doc.Save("YOUR_DIRECTORY/output.pdf");
```

Si necesitas preservar los metadatos originales (autor, fecha de creación), Aspose.Pdf los copia por defecto. También puedes especificar un objeto `SaveOptions` para cumplimiento PDF/A o compresión.

---

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para ejecutar. Pégalo en un proyecto de aplicación de consola, ajusta las rutas de archivo y pulsa **F5**.

```csharp
using Aspose.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using var doc = new Document("YOUR_DIRECTORY/input.pdf");

        // 2️⃣ Configure Bates numbering options
        var batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC-",
            StartNumber = 1000,
            FontSize = 12,
            HorizontalAlignment = HorizontalAlignment.Right,
            VerticalAlignment = VerticalAlignment.Bottom,
            Margin = new MarginInfo(0, 20, 0, 0)
        };

        // 3️⃣ Apply numbering to every page
        doc.Pages.AddBatesNumbering(batesOptions);

        // 4️⃣ Save the output PDF
        doc.Save("YOUR_DIRECTORY/output.pdf");

        System.Console.WriteLine("Bates numbering added successfully!");
    }
}
```

**Resultado esperado:** Cada página de `output.pdf` muestra ahora un pie de página como `ABC-1000`, `ABC-1001`, … anclado a la esquina inferior‑derecha. Abre el archivo en cualquier lector de PDF para verificar.

---

## Manejo de variaciones comunes

### Añadir solo números de página en el pie de página

Si solo necesitas números de página simples sin prefijo, establece `Prefix = ""` y quizá ajusta el margen para evitar colisiones con pies de página existentes.

```csharp
batesOptions.Prefix = "";
batesOptions.StartNumber = 1; // classic page numbering
```

### Usar una alineación diferente

Los documentos legales a veces requieren que el número esté centrado en la parte inferior. Cambia la alineación:

```csharp
batesOptions.HorizontalAlignment = HorizontalAlignment.Center;
```

### Trabajar con PDFs encriptados

Cuando el PDF fuente está protegido con contraseña, proporciona la contraseña así:

```csharp
using var doc = new Document("secure.pdf", new LoadOptions { Password = "mySecret" });
```

El resto del flujo de trabajo permanece idéntico.

### Omitir pies de página existentes

Si un documento ya contiene un pie de página que no deseas sobrescribir, puedes anteponer una cadena personalizada que haga que el nuevo número sea distinto, o iterar manualmente las páginas y añadir un `TextFragment` solo donde el pie de página esté ausente. La clase `Page` de la biblioteca expone las colecciones `Annotations` y `Contents` para un control granular.

---

## Consejos profesionales y trampas comunes

- **Evitar recortes**: Márgenes inferiores muy pequeños pueden hacer que el texto se corte en impresoras. Prueba con una impresión física si vas a distribuir copias en papel.  
- **Rendimiento**: Añadir números Bates a un PDF de 500 páginas lleva menos de un segundo en un portátil moderno, pero lotes grandes se benefician del procesamiento en paralelo—solo recuerda que `Document` no es seguro para hilos, así que cada hilo necesita su propia instancia.  
- **Compatibilidad de versiones**: El código funciona con Aspose.Pdf 23.10 y versiones posteriores. Si usas una versión anterior, los nombres de propiedades son los mismos pero el constructor de `MarginInfo` podría requerir argumentos `float`.  
- **Cumplimiento legal**: Algunas jurisdicciones exigen que el número Bates se coloque en una ubicación específica (p. ej., inferior‑izquierda). Ajusta `HorizontalAlignment` en consecuencia.  

---

## Conclusión

Acabamos de demostrar cómo **añadir numeración Bates a archivos PDF** usando Aspose.Pdf para .NET, cubriendo todo, desde la carga del documento hasta el guardado de la versión final con un pie de página limpio. Ajustando un puñado de propiedades también puedes **añadir números de página en el pie**, **añadir números secuenciales a PDF**, o personalizar la apariencia para cumplir cualquier norma legal.

¿Listo para el siguiente paso? Prueba combinar esta técnica con la extracción de texto OCR para incrustar palabras clave buscables junto a tus números Bates, o automatiza el proceso para carpetas completas usando `Directory.GetFiles`. Las posibilidades son infinitas, y la base que ahora tienes hará que esas extensiones sean sencillas.

¡Feliz codificación, y que tus PDFs estén siempre perfectamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}