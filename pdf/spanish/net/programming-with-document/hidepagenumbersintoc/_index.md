---
"description": "Aprenda a ocultar los números de página en la tabla de contenido con Aspose.PDF para .NET. Siga esta guía detallada con ejemplos de código para crear archivos PDF profesionales."
"linktitle": "Ocultar números de página en la tabla de contenidos"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Ocultar números de página en la tabla de contenidos"
"url": "/es/net/programming-with-document/hidepagenumbersintoc/"
"weight": 220
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ocultar números de página en la tabla de contenidos

## Introducción

Al trabajar con archivos PDF, a veces es posible que quieras generar una tabla de contenido (TOC) pero mantener la nitidez ocultando los números de página. Quizás el documento fluya mejor sin ellos, o quizás sea una cuestión estética. Sea cual sea el motivo, si trabajas con Aspose.PDF para .NET, este tutorial te mostrará exactamente cómo ocultar los números de página en tu TOC.

## Prerrequisitos

Antes de empezar, hay algunas cosas que necesitarás tener en cuenta. Aquí tienes una lista rápida:

- Visual Studio instalado: necesitará una versión funcional de Visual Studio para codificar.
- Biblioteca Aspose.PDF para .NET: asegúrese de haber instalado la biblioteca Aspose.PDF para .NET.
  - Enlace de descarga: [Aspose.PDF para .NET](https://releases.aspose.com/pdf/net/)
- Licencia temporal: si está probando las funciones, es útil tener una licencia temporal.
  - Licencia temporal: [Consíguelo aquí](https://purchase.aspose.com/temporary-license/)

## Importar paquetes

Antes de comenzar con el código, asegúrese de importar los siguientes espacios de nombres a su proyecto de C#. Estos proporcionarán las clases y los métodos necesarios para trabajar con documentos PDF y crear su tabla de contenido (TOC).

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;
```

Ahora que su entorno está listo y los paquetes se han importado, desglosemos cada paso del proceso. Cubriremos cada parte del código para garantizar la claridad y que pueda seguirlo fácilmente.

## Paso 1: Inicialice su documento PDF

Lo primero que debemos hacer es crear un nuevo documento PDF y agregar una página para la Tabla de Contenidos (TOC).


```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string outFile = dataDir + "HiddenPageNumbers_out.pdf";
Document doc = new Document();
Page tocPage = doc.Pages.Add();
```

- dataDir: este es el directorio donde se guardará el archivo de salida.
- Documento(): Inicializa un nuevo documento PDF.
- Pages.Add(): agrega una nueva página en blanco al documento, que más tarde contendrá su tabla de contenidos.

## Paso 2: Configurar la información y el título de la tabla de contenidos

A continuación, definiremos la información de la tabla de contenidos, incluida la configuración del título que aparecerá en la parte superior de la tabla de contenidos.

```csharp
TocInfo tocInfo = new TocInfo();
TextFragment title = new TextFragment("Table Of Contents");
title.TextState.FontSize = 20;
title.TextState.FontStyle = FontStyles.Bold;
tocInfo.Title = title;
tocPage.TocInfo = tocInfo;
```

- TocInfo: este objeto contiene toda la información sobre la tabla de contenidos.
- TextFragment: Representa el texto del título del TOC, aquí lo establecemos como "Tabla de contenido".
- FontStyle: Damos estilo al título de la tabla de contenidos estableciendo su tamaño en 20 y poniéndolo en negrita.
- tocPage.TocInfo: Asignamos la información del TOC a la página que mostrará el TOC.

## Paso 3: Ocultar los números de página en la tabla de contenidos

¡Ahora viene la parte divertida! Aquí configuramos la tabla de contenidos para ocultar los números de página.

```csharp
tocInfo.IsShowPageNumbers = false;
tocInfo.FormatArrayLength = 4;
```

- IsShowPageNumbers: Este es el interruptor que oculta los números de página. Configúrelo en `false`y los números de página no aparecerán en la tabla de contenidos.
- FormatArrayLength: lo establecemos en 4, lo que indica que queremos definir el formato para cuatro niveles de encabezados de TOC.

## Paso 4: Personalizar el formato de la tabla de contenidos

Para agregar más estilo a su tabla de contenido, ahora definiremos el formato para diferentes niveles de encabezados.

```csharp
tocInfo.FormatArray[0].Margin.Right = 0;
tocInfo.FormatArray[0].TextState.FontStyle = FontStyles.Bold | FontStyles.Italic;
tocInfo.FormatArray[1].Margin.Left = 30;
tocInfo.FormatArray[1].TextState.Underline = true;
tocInfo.FormatArray[1].TextState.FontSize = 10;
tocInfo.FormatArray[2].TextState.FontStyle = FontStyles.Bold;
tocInfo.FormatArray[3].TextState.FontStyle = FontStyles.Bold;
```

- FormatArray: Esta matriz controla el formato de las entradas de la tabla de contenidos. Cada índice representa un nivel de encabezado diferente.
- Margen y estilo de texto: establecemos márgenes y aplicamos estilos de fuente como negrita, cursiva y subrayado para cada nivel de encabezado.

## Paso 5: Agregar encabezados al documento

Por último, agreguemos los encabezados reales que formarán parte de la tabla de contenidos.

```csharp
Page page = doc.Pages.Add();
for (int Level = 1; Level != 5; Level++)
{ 
    Heading heading2 = new Heading(Level); 
    TextSegment segment2 = new TextSegment(); 
    heading2.TocPage = tocPage; 
    heading2.Segments.Add(segment2); 
    heading2.IsAutoSequence = true; 
    segment2.Text = "this is heading of level " + Level; 
    heading2.IsInList = true; 
    page.Paragraphs.Add(heading2); 
}
```

- Encabezado y segmento de texto: Representan los encabezados que aparecerán en la tabla de contenidos. Cada nivel tiene su propio encabezado.
- IsAutoSequence: numera automáticamente los encabezados.
- IsInList: garantiza que cada encabezado aparezca en la tabla de contenidos.

## Paso 6: Guardar el documento

Una vez que todo esté configurado, guarde el documento PDF en el archivo de salida especificado.

```csharp
doc.Save(outFile);
```

¡Listo! Has creado un PDF con índice, ¡y los números de página están ocultos!

## Conclusión

Crear una tabla de contenido en un PDF y ocultar los números de página puede parecer complicado, pero con Aspose.PDF para .NET, es facilísimo. Siguiendo esta guía paso a paso, has aprendido a personalizar el formato de la tabla de contenido, ocultar los números de página y aplicar diferentes estilos a tus encabezados. Ahora puedes crear PDF profesionales adaptados a tus necesidades.

## Preguntas frecuentes

### ¿Puedo mostrar números de página para encabezados específicos en la tabla de contenidos?
No, Aspose.PDF oculta o muestra los números de página de toda la tabla de contenidos. No se pueden ocultar de forma selectiva para entradas específicas.

### ¿Es posible agregar más niveles al TOC?
Sí, puedes aumentar el `FormatArrayLength` para definir más niveles de encabezados de TOC.

### ¿Cómo puedo cambiar la fuente de todas las entradas de la tabla de contenidos?
Puede cambiar la fuente modificando el `TextState.Font` propiedad para cada nivel en el `FormatArray`.

### ¿Puedo insertar hipervínculos en la tabla de contenidos?
Sí, puedes vincular cada entrada de la tabla de contenidos a una sección específica del documento mediante el botón `Heading.TocPage` propiedad.

### ¿Necesito una licencia para Aspose.PDF?
Sí, se requiere una licencia válida para el uso en producción. Puede obtener una licencia temporal. [aquí](https://purchase.aspose.com/temporary-license/) para probar las funciones.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}