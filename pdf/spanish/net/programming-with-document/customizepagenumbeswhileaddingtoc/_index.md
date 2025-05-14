---
"description": "Aprenda a personalizar los números de página mientras agrega una tabla de contenido a sus documentos PDF usando Aspose.PDF para .NET en este completo tutorial."
"linktitle": "Personalizar los números de página al agregar la tabla de contenidos"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Personalizar los números de página al agregar la tabla de contenidos"
"url": "/es/net/programming-with-document/customizepagenumbeswhileaddingtoc/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Personalizar los números de página al agregar la tabla de contenidos

## Introducción

En el mundo de la gestión documental, los PDF son la norma. Son el formato predilecto para compartir y conservar documentos en diversas plataformas. Pero ¿qué ocurre cuando se desea mejorar los documentos PDF con funciones como una tabla de contenido (TOC)? ¡Aquí es donde entra en juego Aspose.PDF para .NET! Esta potente biblioteca permite a los desarrolladores manipular archivos PDF con facilidad, permitiéndoles añadir, modificar y personalizar contenido sin esfuerzo. En este tutorial, profundizaremos en cómo personalizar los números de página al añadir una TOC a los documentos PDF con Aspose.PDF para .NET. ¡Así que, a desarrollar, y empecemos!

## Prerrequisitos

Antes de pasar al código, hay algunas cosas que debes tener en cuenta:

1. Visual Studio: Asegúrese de tener Visual Studio instalado en su equipo. Este será nuestro entorno de desarrollo.
2. Aspose.PDF para .NET: Necesita descargar e instalar la biblioteca Aspose.PDF. Puede encontrarla aquí. [aquí](https://releases.aspose.com/pdf/net/).
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.
4. Un archivo PDF de muestra: Tenga listo un archivo PDF de muestra con el que podamos trabajar. Puede crear uno simple o descargar uno existente.

## Importar paquetes

Para empezar, necesitamos importar los paquetes necesarios. Abra su proyecto de Visual Studio y agregue una referencia a la biblioteca Aspose.PDF. Puede hacerlo usando el Administrador de paquetes NuGet:

1. Haga clic derecho en su proyecto en el Explorador de soluciones.
2. Seleccione "Administrar paquetes NuGet".
3. Busque “Aspose.PDF” e instálelo.

```csharp
using Aspose.Pdf.Text;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

¡Una vez que tengas la biblioteca instalada, puedes comenzar a codificar!

## Paso 1: Configure su directorio de documentos

Primero, debemos configurar nuestro directorio de documentos. Aquí almacenaremos nuestros archivos PDF de entrada y salida. 

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "42824.pdf";
string outFile = dataDir + "42824_out.pdf";
```

En este fragmento, reemplace `YOUR DOCUMENT DIRECTORY` Con la ruta de acceso de sus archivos PDF. Esto nos permitirá cargar el PDF existente y guardar la versión modificada.

## Paso 2: Cargue el archivo PDF existente

Ahora que tenemos configurado nuestro directorio de documentos, carguemos el archivo PDF existente. 

```csharp
Document doc = new Document(inFile);
```

Aquí creamos uno nuevo `Document` objeto pasando la ruta del archivo de entrada. Esto nos permite manipular el contenido del PDF mediante programación.

## Paso 3: Insertar una nueva página para la tabla de contenidos

A continuación, necesitamos crear una nueva página en nuestro PDF donde residirá la Tabla de Contenidos.

```csharp
Aspose.Pdf.Page tocPage = doc.Pages.Insert(1);
```

Esta línea inserta una nueva página al principio del documento. La tabla de contenidos se mostrará en esta página.

## Paso 4: Crear información de tabla de contenidos

Ahora, creemos un objeto para representar la información TOC.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocInfo.PageNumbersPrefix = "P";
tocPage.TocInfo = tocInfo;
```

En este paso, creamos un `TocInfo` objeto y establecemos su título como "Índice". También personalizamos el tamaño y el estilo de la fuente. `PageNumbersPrefix` se establece en "P", que precederá los números de página en la tabla de contenidos.

## Paso 5: Agregar encabezados a la tabla de contenidos

¡Ahora viene la parte divertida! Recorreremos las páginas del documento y añadiremos encabezados a nuestra tabla de contenidos.

```csharp
for (int i = 1; i < doc.Pages.Count; i++)
{
    Aspose.Pdf.Heading heading2 = new Aspose.Pdf.Heading(1);
    TextSegment segment2 = new TextSegment();
    heading2.TocPage = tocPage;
    heading2.Segments.Add(segment2);
    heading2.DestinationPage = doc.Pages[i + 1];
    heading2.Top = doc.Pages[i + 1].Rect.Height;
    segment2.Text = "Page " + i.ToString();
    tocPage.Paragraphs.Add(heading2);
}
```

En este bucle, creamos un nuevo `Heading` Objeto para cada página. Establecemos la página de destino para cada encabezado y especificamos el texto que se mostrará: "Página X", donde X es el número de página. Finalmente, añadimos el encabezado a la página de índice.

## Paso 6: Guarde el documento actualizado

Después de agregar todos los encabezados necesarios, es hora de guardar nuestro documento actualizado.

```csharp
doc.Save(outFile);
```

Esta línea guarda el PDF modificado con la tabla de contenidos incluida. ¡Ahora puede abrir el archivo de salida y ver su tabla de contenidos personalizada!

## Conclusión

¡Y listo! Has personalizado correctamente la numeración de páginas y añadido una tabla de contenido a tu documento PDF con Aspose.PDF para .NET. Esta potente biblioteca facilita la manipulación de archivos PDF y, con solo unas pocas líneas de código, puedes mejorar significativamente tus documentos. Ya sea que estés creando informes, ebooks o cualquier otro tipo de PDF, tener una tabla de contenido puede mejorar enormemente la navegación de tus lectores. ¿A qué esperas? ¡Sumérgete en Aspose.PDF y empieza a crear PDF increíbles hoy mismo!

## Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?
Aspose.PDF para .NET es una biblioteca que permite a los desarrolladores crear, manipular y convertir documentos PDF mediante programación.

### ¿Puedo utilizar Aspose.PDF gratis?
Sí, Aspose ofrece una versión de prueba gratuita que puedes usar para explorar las funciones de la biblioteca. Puedes descargarla. [aquí](https://releases.aspose.com/).

### ¿Cómo puedo obtener soporte para Aspose.PDF?
Puede obtener ayuda visitando el foro de Aspose [aquí](https://forum.aspose.com/c/pdf/10).

### ¿Existe una licencia temporal disponible?
Sí, puede solicitar una licencia temporal para Aspose.PDF [aquí](https://purchase.aspose.com/temporary-license/).

### ¿Dónde puedo comprar Aspose.PDF para .NET?
Puedes comprar Aspose.PDF para .NET [aquí](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}