---
category: general
date: 2026-01-15
description: Agrega números Bates a tu PDF rápidamente con Aspose.Pdf. Aprende cómo
  agregar un pie de página al PDF, agregar números de página al PDF y agregar numeración
  de página personalizada.
draft: false
keywords:
- add bates numbers
- bates numbering pdf
- add footer to pdf
- add page numbers pdf
- add custom page numbering
language: es
og_description: Agrega números Bates a tu PDF rápidamente con Aspose.Pdf. Aprende
  cómo añadir un pie de página al PDF, agregar números de página al PDF y crear numeración
  de página personalizada.
og_title: Agregar números Bates al PDF – numeración Bates PDF
tags:
- Aspose.Pdf
- C#
- PDF manipulation
title: Agregar números Bates a PDF – numeración Bates PDF
url: /es/net/programming-with-text/add-bates-numbers-to-pdf-bates-numbering-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar números Bates a PDF – Guía completa

¿Alguna vez necesitaste **add bates numbers** a un PDF pero no sabías por dónde empezar? No estás solo—los equipos legales, auditores y cualquiera que maneje grandes conjuntos de documentos se topan con este problema a diario. ¿La buena noticia? Con Aspose.Pdf para .NET puedes añadir esos números a cada página con solo unas pocas líneas.

En este tutorial recorreremos todo el proceso: desde importar la biblioteca Aspose.Pdf, cargar tu archivo fuente, configurar un *BatesNumberingArtifact*, adjuntarlo como pie de página y, finalmente, guardar el resultado. Al final también sabrás cómo **add footer to pdf**, **add page numbers pdf**, e incluso **add custom page numbering** para esos casos límite complicados.

## Lo que necesitarás

- .NET 6+ (o .NET Framework 4.8 si aún estás en la pila clásica)  
- Una referencia al paquete NuGet **Aspose.Pdf** (`Install-Package Aspose.Pdf`)  
- Un archivo PDF que deseas marcar (lo llamaremos `source.pdf`)  

Eso es todo—sin herramientas extra, sin editores PDF pesados. Vamos a sumergirnos.

![add bates numbers example](https://example.com/images/add-bates-numbers.png "add bates numbers example")

## Paso 1: Agregar números Bates – Cargar el documento PDF

Primero, necesitamos un objeto `Document` que represente el PDF que vamos a modificar. Piensa en esto como abrir un documento de Word antes de comenzar a escribir.

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the PDF you want to add bates numbers to
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // The rest of the steps go here...
    }
}
```

> **Por qué es importante:** Cargar el archivo te da acceso a su colección `Pages`, que es donde adjuntaremos el artefacto de numeración Bates más adelante. Si el archivo no se encuentra, Aspose lanzará una clara `FileNotFoundException`, así que verifica nuevamente la ruta.

## Paso 2: Configurar la numeración bates pdf

Ahora definimos *cómo* deben verse los números. El `BatesNumberingArtifact` te permite establecer un prefijo, número inicial, relleno de dígitos, sufijo y ubicación. Esto es el núcleo de **bates numbering pdf**.

```csharp
// Step 2: Create and configure the Bates numbering artifact
var batesArtifact = new BatesNumberingArtifact
{
    Prefix = "CASE-",
    StartNumber = 1000,
    NumberDigits = 5,          // forces 5 digits, e.g., 01000
    Suffix = "-A",
    Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
};
```

> **Consejo profesional:** Si necesitas que los números aparezcan en el encabezado en su lugar, cambia `BottomCenter` por `TopCenter`. El enum de ubicación también admite `BottomLeft`, `BottomRight`, etc., dándote flexibilidad para diferentes estilos de **add footer to pdf**.

## Paso 3: Agregar números de página pdf – Adjuntar el artefacto a cada página

Con el artefacto listo, iteramos por cada página y lo añadimos a la colección `Artifacts`. Este es el paso que realmente **adds page numbers pdf**.

```csharp
// Step 3: Attach the artifact to each page
foreach (Page page in pdfDocument.Pages)
{
    page.Artifacts.Add(batesArtifact);
}
```

> **¿Qué ocurre bajo el capó?** La colección `Artifacts` se renderiza después del contenido principal de la página, asegurando que el número Bates quede encima de cualquier texto existente pero debajo de las anotaciones. Si necesitas que el número esté detrás del contenido (raro), usarías `page.Artifacts.Insert(0, batesArtifact)`.

## Paso 4: Agregar numeración de página personalizada – Guardar el PDF actualizado

Finalmente, escribimos el documento modificado en disco. El archivo de salida contendrá los números Bates como parte permanente de cada página.

```csharp
// Step 4: Save the PDF with the new numbering
pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
```

> **Consejo de verificación:** Abre `bates_out.pdf` en cualquier visor. Deberías ver algo como `CASE-01000-A` centrado en la parte inferior de cada página. Si los números faltan, verifica nuevamente que la propiedad `Placement` coincida con la ubicación deseada.

## Ejemplo completo en funcionamiento

Juntando todo, aquí tienes el programa completo, listo para ejecutar:

```csharp
using Aspose.Pdf;
using System;

class Program
{
    static void Main()
    {
        // Load the source PDF
        var pdfDocument = new Document(@"YOUR_DIRECTORY\source.pdf");

        // Configure Bates numbering artifact
        var batesArtifact = new BatesNumberingArtifact
        {
            Prefix = "CASE-",
            StartNumber = 1000,
            NumberDigits = 5,
            Suffix = "-A",
            Placement = BatesNumberingArtifact.PlacementLocation.BottomCenter
        };

        // Attach artifact to each page (adds page numbers pdf)
        foreach (Page page in pdfDocument.Pages)
        {
            page.Artifacts.Add(batesArtifact);
        }

        // Save the new PDF (adds footer to pdf)
        pdfDocument.Save(@"YOUR_DIRECTORY\bates_out.pdf");

        Console.WriteLine("Bates numbers added successfully! Check bates_out.pdf.");
    }
}
```

### Resultado esperado

- **Archivo:** `bates_out.pdf` en la misma carpeta que `source.pdf`
- **Visual:** Texto centrado en la parte inferior `CASE-01000-A`, `CASE-01001-A`, … para cada página subsiguiente
- **Comportamiento:** Los números están incrustados permanentemente; sobreviven a la impresión, aplanado y posteriores ediciones.

## Variaciones comunes y casos límite

| Situation | How to Adjust |
|-----------|---------------|
| **Número de inicio diferente** | Cambiar `StartNumber` a cualquier entero (p.ej., `StartNumber = 500`). |
| **Sufijos de letra por volumen** | Usa un bucle para modificar `Suffix` por página, o crea varios artefactos con diferentes sufijos. |
| **Numeración alineada a la derecha** | Establece `Placement = BatesNumberingArtifact.PlacementLocation.BottomRight`. |
| **Documentos grandes (más de 10k páginas)** | Considera procesar páginas por lotes o aumentar `NumberDigits` para evitar desbordamiento. |
| **Necesidad de ocultar números en ciertas páginas** | Omite esas páginas en el bucle `foreach` (p.ej., `if (page.Number != 1) page.Artifacts.Add(batesArtifact);`). |

> **Cuidado con:** Usar un `Prefix` o `Suffix` que contenga caracteres ilegales para nombres de archivo (p.ej., `*` o `?`). Aspose aún los incrustará, pero pueden causar problemas al extraer el texto más adelante.

## Consejos profesionales para uso en producción

- **Cachea el artefacto** si estás procesando muchos PDFs consecutivamente; crearlo una vez ahorra unos milisegundos por archivo.  
- **Seguridad en hilos:** La instancia `BatesNumberingArtifact` no es segura para hilos, así que proporciona a cada hilo su propia copia.  
- **Rendimiento:** Para lotes masivos, desactiva la compresión PDF (`pdfDocument.Compress = false`) antes de guardar, y luego vuelve a activarla si es necesario.  
- **Pruebas:** Siempre realiza una rápida verificación visual del primer PDF generado para asegurar que la ubicación coincida con los estándares de tu equipo legal.  

## Conclusión

Ahora tienes una receta sólida, de extremo a extremo, para **add bates numbers** a cualquier PDF usando Aspose.Pdf, completa con opciones para **add footer to pdf**, **add page numbers pdf**, y **add custom page numbering**. El código es totalmente autónomo, funciona con .NET 6 y posteriores, y puede integrarse en cualquier canal de automatización existente.

¿Qué sigue? Prueba cambiar la ubicación `BottomCenter` por un estilo de encabezado, experimenta con prefijos dinámicos (p.ej., IDs de casos desde una base de datos), o combina esto con las funciones de extracción de texto de Aspose para generar un índice buscable de tus documentos recién numerados. El cielo es el límite, y acabas de obtener una herramienta poderosa para el control de documentos.

¡Feliz codificación, y que tus PDFs siempre permanezcan perfectamente numerados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}