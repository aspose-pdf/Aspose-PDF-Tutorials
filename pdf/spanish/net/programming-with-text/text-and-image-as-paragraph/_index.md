---
"description": "Crea archivos PDF con texto e imágenes con Aspose.PDF para .NET. Aprende a añadir texto e imágenes en línea paso a paso."
"linktitle": "Texto e imagen como párrafo en un archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Texto e imagen como párrafo en un archivo PDF"
"url": "/es/net/programming-with-text/text-and-image-as-paragraph/"
"weight": 530
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Texto e imagen como párrafo en un archivo PDF

## Introducción

En el mundo digital actual, los PDF son un formato de documento universal que la mayoría de nosotros utilizamos a diario. Ya sea un informe, un ebook o una factura comercial, los PDF facilitan compartir información entre diversas plataformas. Pero ¿qué ocurre si desea personalizar un PDF mediante programación? Ahí es donde entra en juego Aspose.PDF para .NET. En este tutorial, le guiaremos en la inserción de texto e imágenes como párrafos en línea en un archivo PDF con Aspose.PDF para .NET.

## Prerrequisitos

Antes de sumergirnos en el código, asegurémonos de que tienes todo lo que necesitas para seguirlo sin problemas:

- Biblioteca Aspose.PDF para .NET: Necesitará instalar Aspose.PDF para .NET. Puede descargarla. [aquí](https://releases.aspose.com/pdf/net/).
- Visual Studio: cualquier versión que admita .NET funcionará bien.
- Comprensión básica de C#: será útil tener cierta familiaridad con C#, pero no se preocupe: ¡lo guiaré paso a paso!
- Documento PDF listo: si desea agregar una imagen personalizada, téngala lista.

También puedes obtener una prueba gratuita de la biblioteca. [aquí](https://releases.aspose.com/), o si estás trabajando en un proyecto a gran escala, considera comprarlo [aquí](https://purchase.aspose.com/buy)¿Necesitas más información? Consulta la documentación. [aquí](https://reference.aspose.com/pdf/net/).

## Importar paquetes

Para empezar a usar Aspose.PDF para .NET, debe importar los espacios de nombres necesarios. Estos espacios de nombres permiten que su código C# interactúe con las funcionalidades de Aspose.PDF.

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using Aspose.Pdf.Facades;
using System;
```

Sencillo, ¿verdad? Ahora pasemos a la parte divertida: crear tu propio archivo PDF.

## Guía paso a paso: Cómo crear un PDF con texto e imagen en línea

Analicemos esto en pasos fáciles de entender y seguir. Imagina que estás armando un rompecabezas; cada paso consiste en encontrar y colocar la pieza correcta.

## Paso 1: Inicializar el documento PDF

El primer paso es inicializar un nuevo documento PDF con Aspose.PDF. Este documento servirá como base para agregar texto e imágenes.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
// Crear una instancia de documento
Document doc = new Document();
```

¿Qué está pasando aquí? Simplemente estamos creando un nuevo documento usando el `Document` Clase y definir el directorio donde quieres guardar el PDF. ¡Es como abrir un nuevo lienzo para tu obra maestra!

## Paso 2: Agrega una página a tu PDF

Un documento no sirve de mucho sin páginas, ¿verdad? Añadamos una página en blanco a tu documento.

```csharp
// Agregar página a la colección de páginas de la instancia de Documento
Page page = doc.Pages.Add();
```

Este fragmento de código añade una nueva página a la colección de páginas de tu documento. Es como abrir una página en blanco de un cuaderno.

## Paso 3: Agregar texto como párrafo

A continuación, añadiremos un párrafo de texto. Aquí podrás insertar tu mensaje o encabezado.

```csharp
// Crear fragmento de texto
TextFragment text = new TextFragment("Hello World.. ");
// Agregar fragmento de texto a la colección de párrafos del objeto Página
page.Paragraphs.Add(text);
```

Aquí creamos un `TextFragment` Objeto para contener el texto "Hola Mundo...", que luego se añade a la página como párrafo. Es como escribir la primera oración de un documento PDF.

## Paso 4: Agregar una imagen como párrafo en línea

Ahora que tenemos el texto, vamos a darle un toque más atractivo añadiendo una imagen como párrafo en línea. Un párrafo en línea simplemente significa que la imagen aparecerá justo después del texto, de forma similar a cómo se muestran las imágenes en los documentos de Word.

```csharp
// Crear una instancia de imagen
Aspose.Pdf.Image image = new Aspose.Pdf.Image();
// Establecer la imagen como párrafo en línea para que aparezca justo después 
// El objeto del párrafo anterior (TextFragment)
image.IsInLineParagraph = true;
// Especificar la ruta del archivo de imagen 
image.File = dataDir + "aspose-logo.jpg";
```

En este fragmento, creamos un `Image` objeto, indíquele que se alinee con el texto y especifique la ruta del archivo de imagen. Esto equivale a pegar una imagen justo después de una oración en un documento. Puede sustituir "aspose-logo.jpg" por la imagen que desee.

## Paso 5: Establecer el tamaño de la imagen (opcional)

¿Quieres cambiar el tamaño de la imagen? No hay problema. Aspose.PDF te permite ajustar la altura y el ancho de la imagen antes de añadirla al documento.

```csharp
// Establecer la altura de la imagen (opcional)
image.FixHeight = 30;
// Establecer el ancho de la imagen (opcional)
image.FixWidth = 100;
```

Esta parte es opcional, pero te ayuda a controlar el tamaño de la imagen en tu PDF. Es como cambiar el tamaño de una foto antes de imprimirla.

## Paso 6: Agregar imagen a la colección de párrafos

Hemos preparado la imagen. Ahora, insertémosla en el documento como un párrafo en línea.

```csharp
// Agregar imagen a la colección de párrafos del objeto de página
page.Paragraphs.Add(image);
```

Esta línea añade la imagen justo después del texto en la colección de párrafos. Es como pulsar el botón "Insertar imagen" en un editor de texto.

## Paso 7: Agregar otro párrafo de texto en línea

¿Qué pasa si quieres añadir más texto justo después de la imagen? Para ello, inserta otro fragmento de texto en línea.

```csharp
// Reinicializar el objeto TextFragment con contenido diferente
text = new TextFragment(" Hello Again..");
// Establecer TextFragment como párrafo en línea
text.IsInLineParagraph = true;
// Agregar un TextFragment recién creado a la colección de párrafos de la página
page.Paragraphs.Add(text);
```

Estamos reutilizando el `TextFragment` Aquí se añade el nuevo texto ("Hola de nuevo...") y se inserta en línea, justo después de la imagen. Esto le da a tu PDF un aspecto fluido y cohesivo.

## Paso 8: Guarde el documento PDF

¡Ya casi terminamos! Ahora, guardemos el documento en el directorio especificado.

```csharp
dataDir = dataDir + "TextAndImageAsParagraph_out.pdf";
doc.Save(dataDir);
Console.WriteLine("\nText and image added successfully as inline paragraphs.\nFile saved at " + dataDir);
```

Este último paso guarda el archivo en tu directorio con el nombre "TextAndImageAsParagraph_out.pdf". ¡Felicitaciones! ¡Has creado un PDF con texto e imágenes integradas!

## Conclusión

Y listo: crear un PDF con texto e imágenes como párrafos en línea con Aspose.PDF para .NET es tan sencillo como seguir estos pasos. Con solo unas líneas de código, puedes añadir contenido dinámico a tus archivos PDF, haciéndolos visualmente más atractivos y profesionales. Ya sea para un informe empresarial o un ebook, controlar el diseño de tus PDF puede marcar la diferencia.

## Preguntas frecuentes

### ¿Puedo agregar varias imágenes como párrafos en línea?  
Sí, puedes agregar varias imágenes creando archivos separados. `Image` objetos y agregarlos a la colección de párrafos.

### ¿Puedo controlar la posición del texto y la imagen en el PDF?  
Sí, al utilizar propiedades como márgenes, puedes controlar la ubicación precisa de tu texto e imágenes.

### ¿Aspose.PDF para .NET es gratuito?  
No, es un producto con licencia, pero puedes obtener uno [prueba gratuita](https://releases.aspose.com/) o comprar una licencia [aquí](https://purchase.aspose.com/buy).

### ¿Puedo agregar hipervínculos al texto?  
Sí, Aspose.PDF permite agregar hipervínculos dentro de fragmentos de texto. Consulta la [documentación](https://reference.aspose.com/pdf/net/) Para más detalles.

### ¿Puedo personalizar la fuente y el estilo del texto?  
¡Por supuesto! Puedes personalizar fácilmente las fuentes, los colores y otras propiedades de estilo de los fragmentos de texto.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}