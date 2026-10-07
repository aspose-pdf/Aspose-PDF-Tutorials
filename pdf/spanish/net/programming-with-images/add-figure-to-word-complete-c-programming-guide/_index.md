---
category: general
date: 2026-04-12
description: Agrega una figura a Word rápidamente con C#. Aprende a posicionar la
  figura en Word, insertar la figura en un docx y añadir XML personalizado para un
  diseño avanzado.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: es
og_description: Agrega una figura a Word rápidamente con C#. Aprende cómo posicionar
  la figura en Word, insertar la figura en un docx y agregar XML personalizado para
  un diseño avanzado.
og_title: Agregar figura a Word – Guía completa de programación en C#
tags:
- C#
- Word Automation
- Document Generation
title: Agregar figura a Word – Guía completa de programación en C#
url: /es/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar figura a Word – Guía completa de programación en C#

¿Alguna vez necesitaste **agregar figura a Word** pero no estabas seguro de por dónde empezar? No estás solo. En muchos proyectos de automatización de oficina, la pieza que falta es una imagen o diagrama bien colocado que vive dentro de una parte XML personalizada. Esta guía te muestra exactamente cómo **posicionar figura en Word**, insertar la figura en un archivo *.docx* e incluso ajustar el XML personalizado subyacente para que la shape se comporte como cualquier objeto nativo de Word.

Recorreremos un ejemplo del mundo real usando la biblioteca GemBox.Document (gratuita para archivos pequeños, comercial para cargas de trabajo mayores). Al final tendrás un programa autónomo y ejecutable que coloca una figura en las coordenadas X = 50, Y = 200 dentro de un contenedor de contenido etiquetado. Sin atajos vagos de “ver la documentación”, solo código claro, por qué funciona y consejos que puedes copiar directamente a tu propio proyecto.

## Requisitos previos

- .NET 6.0 o posterior (el código también se compila con .NET Core 3.1)
- **GemBox.Document** paquete NuGet (`Install-Package GemBox.Document`)
- Un archivo Word de inicio (`input.docx`) que ya contiene una etiqueta XML personalizada donde deseas que aparezca la figura
- Conocimientos básicos de C# (verás por qué cada línea es importante)

> **Consejo profesional:** Si no tienes un documento pre‑etiquetado, puedes crear uno en Word insertando un *Content Control* → *XML Mapping Pane* → asignar una parte XML personalizada. La biblioteca tratará ese control como `TaggedContent`.

## Paso 1 – Cargar el documento fuente

Lo primero que hacemos es abrir el archivo *.docx* existente. `Document` es el punto de entrada para todas las operaciones de GemBox.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*¿Por qué?* Cargar el archivo nos da acceso a sus partes internas, incluyendo cualquier contenedor XML personalizado. Sin esto, no podríamos localizar el nodo `TaggedContent` que contendrá nuestra figura.

## Paso 2 – Acceder al contenido etiquetado (contenedor XML personalizado)

El XML personalizado se almacena dentro de un *content control* en Word. GemBox lo expone como `TaggedContent`. 

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

Si el documento tiene múltiples secciones etiquetadas, `TaggedContent` devuelve la **primera**. También puedes enumerar `doc.TaggedContents` para seleccionar una etiqueta específica por nombre.

## Paso 3 – Crear el elemento Figure

Un `FigureElement` representa una imagen, gráfico o cualquier objeto visual que Word trata como una *shape*. Lo crearemos dentro del contenedor etiquetado.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*¿Por qué crear una figura aquí?* Al adjuntarla al nodo XML personalizado, Word sabe que la figura pertenece a esa sección lógica, lo cual es crucial para ediciones posteriores o flujos de trabajo basados en controles de contenido.

## Paso 4 – Posicionar la figura con precisión

Word usa puntos (1 pt ≈ 1/72 in) para posicionar. La estructura `PointF` nos permite establecer coordenadas X/Y fácilmente.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **Cómo posicionar shape word:** La propiedad `Position` acepta un `PointF` donde el primer valor es el desplazamiento horizontal (izquierda) y el segundo es el desplazamiento vertical (arriba) relativo al margen de la página. Ajusta estos números para afinar la ubicación.

## Paso 5 – Insertar la figura en el árbol de contenido etiquetado

Ahora adjuntamos la figura al elemento raíz del árbol XML personalizado. Esto agrega físicamente la shape al documento Word.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

En este punto la figura está dentro del documento, pero aún no tiene una fuente de imagen. Añadamos un PNG sencillo desde el disco.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Paso 6 – Guardar el documento modificado

Finalmente, escribimos los cambios en un nuevo archivo *.docx*.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

Cuando abras `output.docx` en Word, verás la imagen posicionada exactamente en (50, 200) dentro del bloque XML personalizado que apuntaste.

### Ejemplo completo y funcional

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Resultado esperado:** Al abrir `output.docx` se muestra el PNG colocado exactamente donde especificaste, anidado dentro de la parte XML personalizada. Si inspeccionas el XML del documento (`.docx` → unzip → `word/document.xml`), verás un elemento `<w:pict>` con las coordenadas correctas del `<v:shape>`.

## Preguntas frecuentes y casos límite

### ¿Qué pasa si el documento tiene múltiples secciones etiquetadas?

Usa `doc.TaggedContents` para enumerar y seleccionar por nombre de etiqueta:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### ¿Cómo agregar un título a la figura?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### ¿Esto funciona con Word 2010 y versiones posteriores?

Sí. GemBox.Document se basa en el estándar Open XML, que es compatible con Word 2007 + (incluyendo 2010, 2013, 2016, 2019 y Microsoft 365).

### ¿Qué pasa si necesito rotar la shape?

```csharp
figure.Rotation = 45; // degrees
```

### ¿Cómo agregar un gráfico vectorial en lugar de una imagen raster?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Consejos profesionales y trampas

- **Rutas de archivo:** Usa `Path.Combine` para evitar separadores codificados, especialmente en plataformas que no son Windows.
- **Límites de licencia:** La licencia gratuita de GemBox limita el tamaño del documento a 20 KB. Para archivos más grandes, compra una clave comercial.
- **Rendimiento:** Reutilizar una única instancia de `Document` para procesamiento por lotes reduce drásticamente el consumo de memoria.
- **Desbordamiento de shape:** Si las dimensiones de la figura exceden los márgenes de la página, Word la recortará. Ajusta `figure.Width` y `figure.Height` según corresponda.

## Conclusión

Ahora sabes **cómo agregar figura a Word**, **posicionar figura en Word** con precisión, y manipular el XML personalizado subyacente para que la shape se comporte como cualquier elemento nativo. El ejemplo completo y ejecutable muestra cada paso: desde cargar el documento, crear un `FigureElement`, establecer sus coordenadas, adjuntar una imagen y, finalmente, guardar el *.docx* actualizado.

A continuación, prueba a experimentar con **insert figure into docx** añadiendo múltiples figuras, usando bucles o generando gráficos al vuelo. También podrías explorar **how to add custom xml** para controles de contenido más ricos o aprender **how to position shape word** en tablas y encabezados. Las posibilidades son infinitas, y con los fundamentos cubiertos aquí estás listo para automatizar documentos Word como un profesional.

¡Feliz codificación, y siéntete libre de dejar un comentario si encuentras algún problema!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}