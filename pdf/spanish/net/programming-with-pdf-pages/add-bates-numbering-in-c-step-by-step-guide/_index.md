---
category: general
date: 2026-03-27
description: Agrega numeración Bates en C# rápidamente. Aprende cómo añadir números
  de página personalizados, añadir números de página secuenciales y añadir números
  personalizados a documentos de Word.
draft: false
keywords:
- add bates numbering
- how to add bates
- add custom page numbers
- add sequential page numbers
- add custom numbers
language: es
og_description: Añade numeración Bates en C# con un ejemplo claro. Esta guía muestra
  cómo agregar números de página personalizados, agregar números de página secuenciales
  y más.
og_title: Añadir numeración Bates en C# – Tutorial completo
tags:
- C#
- Document Processing
- Bates Numbering
title: Agregar numeración Bates en C# – Guía paso a paso
url: /es/net/programming-with-pdf-pages/add-bates-numbering-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar numeración Bates en C# – Guía paso a paso

¿Alguna vez te has preguntado cómo **agregar numeración bates** a un documento Word sin volverte loco? No eres el único. En muchos proyectos legales o de cumplimiento, cada página necesita un identificador único, y hacerlo a mano es una pesadilla.  

En este tutorial recorreremos un ejemplo completo y ejecutable que **agrega numeración bates**, te muestra **cómo agregar bates** en unas pocas líneas, y además cubre cómo **agregar números de página personalizados** y **agregar números de página secuenciales** cuando los necesites. Al final tendrás un archivo .docx marcado con los números que elijas, sin necesidad de herramientas de terceros.

## Lo que aprenderás

- Cargar un archivo DOCX con la API Aspose.Words para .NET (o cualquier biblioteca compatible).  
- Configurar **agregar números personalizados** como un prefijo, un valor inicial y un tamaño de fuente.  
- Aplicar la numeración a cada página en una sola llamada.  
- Guardar el resultado y verificar que los números aparezcan como se espera.  

No se requiere experiencia previa con la numeración Bates; solo una configuración básica de C# y una copia del documento fuente. Vamos a sumergirnos.

## Prerrequisitos

- .NET 6+ (el código funciona tanto en .NET Core como en .NET Framework).  
- Aspose.Words para .NET instalado vía NuGet (`Install-Package Aspose.Words`).  
- Un documento Word llamado `input.docx` colocado en una carpeta que puedas referenciar (`YOUR_DIRECTORY`).  
- Visual Studio, VS Code, o cualquier IDE de C# que prefieras.

> **Consejo profesional:** Si estás usando una biblioteca diferente (p.ej., Open XML SDK), los conceptos siguen siendo los mismos; solo cambia las llamadas a la API.

## Paso 1: Cargar el documento fuente

Primero necesitamos cargar el archivo Word en memoria.

```csharp
using Aspose.Words;

// Step 1: Load the source document
Document document = new Document("YOUR_DIRECTORY/input.docx");
```

*Por qué es importante:* Cargar el archivo crea un objeto `Document` que te da acceso a páginas, secciones y al árbol de nodos de bajo nivel. Sin él no puedes adjuntar ninguna numeración.

## Paso 2: Configurar opciones de numeración Bates

Ahora definimos exactamente cómo deben verse los números. Aquí es donde **agregas números de página personalizados** o **agregas números de página secuenciales**.

```csharp
// Step 2: Define Bates numbering options (prefix, start number, font size)
BatesNumberingOptions batesOptions = new BatesNumberingOptions
{
    // Prefix that appears before every number, e.g., "ABC"
    Prefix = "ABC",
    // The first number in the sequence; change to 1 if you prefer
    Start = 1000,
    // Font size in points; 9 works well for most legal docs
    FontSize = 9
};
```

*Por qué es importante:* El `Prefix` te permite **agregar números personalizados** como un ID de caso, mientras que `Start` determina el contador inicial. Cambiar `FontSize` asegura que los números no invadan los márgenes de la página.

## Paso 3: Aplicar numeración Bates a cada página

Con las opciones listas, le indicamos a la biblioteca que marque cada página.

```csharp
// Step 3: Apply Bates numbering to all pages of the document
document.Pages.AddBatesNumbering(batesOptions);
```

*Por qué es importante:* El método `AddBatesNumbering` recorre la colección interna de páginas e inserta un cuadro de texto en la esquina inferior derecha (la ubicación predeterminada). Es el núcleo de **cómo agregar bates** sin escribir un bucle tú mismo.

## Paso 4: Guardar el documento actualizado

Finalmente, escribimos el archivo modificado de nuevo en el disco.

```csharp
// Step 4: Save the updated document
document.Save("YOUR_DIRECTORY/output.docx");
```

*Por qué es importante:* Guardar crea un nuevo `output.docx` que puedes abrir en Word, LibreOffice o cualquier visor para confirmar que los números aparecen.

## Resultado esperado

Abre `output.docx`. Cada página debería mostrar algo como:

```
ABC‑1000   (on page 1)
ABC‑1001   (on page 2)
ABC‑1002   (on page 3)
...
```

Si abres la vista previa de impresión del documento verás los números en la esquina inferior derecha, coincidiendo con el tamaño de fuente que configuraste.

## Casos límite y variaciones

| Situación | Qué cambiar | Por qué |
|-----------|-------------|---------|
| **No se necesita prefijo** | `Prefix = string.Empty` | Elimina la parte “ABC‑”, dejando solo la secuencia numérica. |
| **Comenzar en 1** | `Start = 1` | Útil para **agregar números de página secuenciales** simples sin un prefijo personalizado. |
| **Documentos grandes (>10,000 páginas)** | Incrementar `FontSize` o ajustar `Location` (usar sobrecargas de `AddBatesNumbering`) | Previene superposición con pies de página o encabezados. |
| **Archivo fuente de solo lectura** | Abrir con `LoadOptions` que permitan acceso de escritura, o copiar el archivo primero | De lo contrario `document.Save` lanzará una excepción. |
| **Ubicación diferente** | Usar `batesOptions.Position = BatesNumberingPosition.TopLeft` (u otro enum) | Algunas firmas requieren los números en la parte superior de la página. |

> **Nota:** No todas las bibliotecas exponen una clase `BatesNumberingOptions`. Con Open XML SDK deberías insertar un `TextBox` manualmente—mismo principio, más código.

## Ejemplo completo funcional

Aquí tienes el programa completo en un solo lugar. Copia‑y‑pega en una aplicación de consola y ejecútalo.

```csharp
using System;
using Aspose.Words;

class Program
{
    static void Main()
    {
        // Load the source document
        Document document = new Document("YOUR_DIRECTORY/input.docx");

        // Define Bates numbering options
        BatesNumberingOptions batesOptions = new BatesNumberingOptions
        {
            Prefix = "ABC",      // custom prefix
            Start = 1000,        // starting number
            FontSize = 9         // font size in points
        };

        // Apply numbering to every page
        document.Pages.AddBatesNumbering(batesOptions);

        // Save the result
        document.Save("YOUR_DIRECTORY/output.docx");

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

Ejecuta el programa, abre `output.docx` y verás la numeración exactamente donde esperabas. 🎉

## Preguntas frecuentes

**P: ¿Puedo cambiar el color de los números?**  
R: Sí. Después de llamar a `AddBatesNumbering`, puedes obtener los objetos `Shape` generados y establecer su propiedad `FillColor`.

**P: ¿Qué pasa si necesito los números en el lado izquierdo en lugar del derecho?**  
R: Usa `batesOptions.Position = BatesNumberingPosition.BottomLeft` (o `TopLeft`, `TopRight`). La API soporta las cuatro esquinas.

**P: ¿Esto funciona con salida PDF?**  
R: Absolutamente. Después de agregar la numeración, llama a `document.Save("output.pdf")`. Los números se renderizan en el PDF igual que en Word.

## Conclusión

Ahora sabes **cómo agregar numeración bates** a un archivo Word usando C#. El tutorial cubrió cargar un documento, configurar **agregar números personalizados**, aplicar **agregar números de página secuenciales**, y guardar el resultado final. Con el ejemplo de código completo, puedes incorporar esto en cualquier proyecto y comenzar a marcar documentos al instante.

¿Listo para el siguiente desafío? Intenta combinar esto con un procesador por lotes que recorra una carpeta de archivos, o explora **agregar números de página personalizados** en el encabezado/pie de página para un aspecto más pulido. De cualquier forma, tienes una base sólida para cualquier tarea de automatización legal‑tech o de cumplimiento.

¿Tienes preguntas o un caso de uso interesante? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}