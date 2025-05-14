---
"description": "Aprenda a añadir una marca de fecha y hora a sus archivos PDF con Aspose.PDF para .NET con esta guía paso a paso. Ideal para mejorar la autenticidad de los documentos."
"linktitle": "Agregar sello de fecha y hora en un archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Agregar sello de fecha y hora en un archivo PDF"
"url": "/es/net/programming-with-stamps-and-watermarks/add-date-time-stamp/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar sello de fecha y hora en un archivo PDF

## Introducción

Al gestionar documentos, especialmente PDF, añadir una marca de fecha y hora puede ser revolucionario. Ya sea que trabaje con documentos legales, informes de proyectos o facturas, una marca de tiempo no solo aporta autenticidad, sino que también proporciona un registro claro de cuándo se creó o modificó el documento. En esta guía, le guiaremos por el proceso para añadir una marca de fecha y hora a un archivo PDF con la biblioteca Aspose.PDF para .NET. 

Este artículo está diseñado para ser claro y fácil de seguir, así que incluso si eres nuevo en programación o en la biblioteca Aspose.PDF, podrás implementar esta función con confianza. ¡Comencemos!

## Prerrequisitos

Antes de comenzar, hay algunos requisitos previos que debes tener en cuenta:

1. Visual Studio: Asegúrate de tener Visual Studio instalado en tu equipo. Aquí es donde escribirás y ejecutarás tu código.
2. Aspose.PDF para .NET: Necesita descargar e instalar la biblioteca Aspose.PDF. Puede encontrar la última versión. [aquí](https://releases.aspose.com/pdf/net/).
3. Conocimientos básicos de C#: Estar familiarizado con la programación en C# te ayudará a comprender mejor los ejemplos, pero no te preocupes si recién estás comenzando; te explicaremos todo paso a paso.
4. Un archivo PDF: Tenga listo un archivo PDF de muestra. Para nuestro ejemplo, usaremos un archivo llamado `AddTextStamp.pdf`.

Una vez que tenga estos requisitos previos, ¡estará listo para comenzar a agregar marcas de fecha y hora a sus archivos PDF!

## Importar paquetes

Para empezar, necesitas importar los espacios de nombres necesarios en tu proyecto de C#. Así es como se hace:

### Crear un nuevo proyecto

1. Abrir Visual Studio: inicie su aplicación de Visual Studio.
2. Crear un nuevo proyecto: seleccione “Crear un nuevo proyecto” en la pantalla de inicio.
3. Elegir aplicación de consola: seleccione “Aplicación de consola (.NET Framework)” de la lista de plantillas de proyecto.
4. Nombre su proyecto: Dé un nombre a su proyecto, por ejemplo, `PDFDateTimeStamp`.

### Añadir referencia de Aspose.PDF

1. Haga clic derecho en Referencias: en el Explorador de soluciones, haga clic derecho en la carpeta “Referencias” de su proyecto.
2. Seleccionar “Agregar referencia”: Elija “Agregar referencia” en el menú contextual.
3. Busque Aspose.PDF: Vaya a la ubicación donde descargó Aspose.PDF y selecciónelo. Haga clic en "Aceptar" para agregarlo a su proyecto.

### Importar espacios de nombres requeridos

En la parte superior de tu `Program.cs` archivo, debe importar los siguientes espacios de nombres:

```csharp
using System.IO;
using Aspose.Pdf;
using Aspose.Pdf.Text;
using System;
using Aspose.Pdf.Annotations;
```

Ahora que tenemos todo configurado, desglosemos el proceso de agregar una marca de fecha y hora a un archivo PDF en pasos claros y manejables.

## Paso 1: Establecer el directorio del documento

Primero, debe especificar el directorio donde se encuentra su archivo PDF. Esto es crucial, ya que el código buscará el PDF en este directorio.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Reemplazar con su ruta actual
```

Asegúrese de reemplazar `YOUR DOCUMENT DIRECTORY` con la ruta real a su archivo PDF.

## Paso 2: Abra el documento PDF

continuación, abrirá el documento PDF donde desea agregar la marca de tiempo. 

```csharp
// Abrir documento
Document pdfDocument = new Document(dataDir + "AddTextStamp.pdf");
```

Esta línea de código inicializa el `Document` clase y carga su archivo PDF en el `pdfDocument` objeto.

## Paso 3: Crear la marca de fecha y hora

Ahora es el momento de generar la marca de fecha y hora. La formatearás para que se muestre de una forma específica. 

```csharp
string annotationText = DateTime.Now.ToString("MM/dd/yy hh:mm:ss tt ");
```

Aquí, `DateTime.Now` obtiene la fecha y hora actuales, y `ToString` lo formatea al formato que desees.

## Paso 4: Crea un sello de texto

Con la cadena de fecha y hora lista, ahora puedes crear un sello de texto que se agregará a tu PDF.

```csharp
// Crear sello de texto
TextStamp textStamp = new TextStamp(annotationText);
```

Esta línea crea una nueva instancia de `TextStamp` utilizando la cadena de fecha y hora formateada.

## Paso 5: Establecer las propiedades del sello

Puedes personalizar la apariencia y la posición del sello. Aquí te explicamos cómo configurar sus propiedades:

```csharp
// Establecer propiedades del sello
textStamp.BottomMargin = 10;
textStamp.RightMargin = 20;
textStamp.HorizontalAlignment = Aspose.Pdf.HorizontalAlignment.Right;
textStamp.VerticalAlignment = VerticalAlignment.Bottom;
```

En este paso, establecemos los márgenes y alineamos el sello con la esquina inferior derecha de la página PDF.

## Paso 6: Agrega el sello al PDF

Ahora es el momento de agregar el sello de texto a su documento PDF. 

```csharp
// Añadir un sello a la colección de sellos
pdfDocument.Pages[1].AddStamp(textStamp);
```

Esta línea añade el sello a la primera página del PDF. Puedes cambiar el número de página si quieres colocarlo en otra página.

## Paso 7: Crear una anotación de texto libre (opcional)

Si desea agregar una anotación al sello, puede crear una `FreeTextAnnotation` como sigue:

```csharp
DefaultAppearance default_appearance = new DefaultAppearance("Arial", 6, System.Drawing.Color.Black);
FreeTextAnnotation textAnnotation = new FreeTextAnnotation(pdfDocument.Pages[1], new Aspose.Pdf.Rectangle(0, 0, 0, 0), default_appearance);
textAnnotation.Name = "Stamp";
textAnnotation.Accept(new AnnotationSelector(textAnnotation));
textAnnotation.Contents = textStamp.Value;
```

Este paso opcional crea una anotación de texto libre que puede proporcionar contexto o información adicional sobre el sello.

## Paso 8: Configurar el borde de anotación

Si deseas personalizar el borde de tu anotación, también puedes hacerlo:

```csharp
Border border = new Border(textAnnotation);
border.Width = 0;
border.Dash = new Dash(1, 1);
textAnnotation.Border = border;
textAnnotation.Rect = new Aspose.Pdf.Rectangle(0, 0, 0, 0);
pdfDocument.Pages[1].Annotations.Add(textAnnotation);
```

Este fragmento de código establece el ancho del borde en 0, haciéndolo invisible, y agrega la anotación al PDF.

## Paso 9: Guarde el documento PDF

Por último, debes guardar el documento PDF modificado. 

```csharp
dataDir = dataDir + "AddDateTimeStamp_out.pdf"; // Especifique el nombre del archivo de salida
pdfDocument.Save(dataDir);
Console.WriteLine("\nDate time stamp added successfully.\nFile saved at " + dataDir);
```

Esta línea guarda el PDF con la marca de tiempo añadida en un nuevo archivo. Puede consultar el directorio especificado para ver el resultado.

## Conclusión

¡Felicitaciones! Ha agregado correctamente una marca de fecha y hora a un archivo PDF con Aspose.PDF para .NET. Esta sencilla pero eficaz función puede mejorar sus documentos, haciéndolos más profesionales y proporcionando un registro claro de cuándo se crearon o modificaron. 

## Preguntas frecuentes

### ¿Puedo personalizar el formato de fecha en la marca de tiempo?
Sí, puedes modificar el `ToString` Método para cambiar el formato de fecha según su preferencia.

### ¿Aspose.PDF es de uso gratuito?
Aspose.PDF ofrece una prueba gratuita, pero para disfrutar de todas las funciones, necesita adquirir una licencia. Puede obtener una licencia temporal. [aquí](https://purchase.aspose.com/temporary-license/).

### ¿Puedo agregar varias marcas de tiempo a un PDF?
¡Por supuesto! Puedes crear varios. `TextStamp` instancias y agregarlas a diferentes páginas o posiciones en el PDF.

### ¿Qué pasa si no tengo Visual Studio?
Puede utilizar cualquier IDE de C# o editor de texto, pero para ejecutar y depurar su proyecto, se recomienda Visual Studio.

### ¿Dónde puedo encontrar más ejemplos del uso de Aspose.PDF?
Puede explorar más ejemplos y tutoriales en el [Documentación de Aspose.PDF](https://reference.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}