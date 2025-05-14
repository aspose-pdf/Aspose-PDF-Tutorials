---
"description": "Aprenda a heredar el zoom en archivos PDF con Aspose.PDF para .NET con esta guía paso a paso. Mejore su experiencia de visualización de PDF."
"linktitle": "Heredar zoom en archivo PDF"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Heredar zoom en archivo PDF"
"url": "/es/net/programming-with-bookmarks/inherit-zoom/"
"weight": 90
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Heredar zoom en archivo PDF

## Introducción

¿Alguna vez has abierto un archivo PDF y te has dado cuenta de que el nivel de zoom no es el correcto? Puede ser frustrante, sobre todo cuando intentas centrarte en un contenido específico. Por suerte, con Aspose.PDF para .NET, puedes configurar fácilmente un nivel de zoom predeterminado para tus documentos PDF. Esta guía te guiará paso a paso por el proceso, garantizando que tus lectores tengan la mejor experiencia posible al visualizar tus PDF. ¡Así que, ponte a programar y manos a la obra!

## Prerrequisitos

Antes de comenzar, hay algunas cosas que debes tener en cuenta:

1. Visual Studio: Asegúrate de tener Visual Studio instalado en tu equipo. Es el mejor entorno para el desarrollo .NET.
2. Aspose.PDF para .NET: Necesitará descargar e instalar la biblioteca Aspose.PDF. Puede encontrarla aquí. [aquí](https://releases.aspose.com/pdf/net/).
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.

## Importar paquetes

Para empezar, necesitas importar los paquetes necesarios a tu proyecto. Así es como puedes hacerlo:

### Crear un nuevo proyecto

Abra Visual Studio y cree un nuevo proyecto de C#. Puede elegir una aplicación de consola para simplificar.

### Añadir referencia de Aspose.PDF

1. Haga clic derecho en su proyecto en el Explorador de soluciones.
2. Seleccione "Administrar paquetes NuGet".
3. Busque "Aspose.PDF" e instale la última versión.

### Importar el espacio de nombres

En la parte superior de su archivo C#, importe el espacio de nombres Aspose.PDF:

```csharp
using System;
using System.IO;
using Aspose.Pdf.Annotations;
using Aspose.Pdf;
```

¡Ahora que ya tienes todo configurado, pasemos a la codificación real!

## Paso 1: Definir el directorio del documento

Primero, debe especificar la ruta a su directorio de documentos. Aquí se guardará el archivo PDF de entrada y el de salida.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

## Paso 2: Abra el documento PDF

A continuación, deberá abrir el documento PDF que desea modificar. Esto se hace usando el `Document` clase de la biblioteca Aspose.PDF.

```csharp
Document doc = new Document(dataDir + "input.pdf");
```

## Paso 3: Acceda a la colección de esquemas/marcadores

Ahora, vayamos al meollo del asunto: los contornos o marcadores del PDF. Estos son los elementos de navegación que permiten a los usuarios acceder a secciones específicas del documento.

```csharp
OutlineItemCollection item = new OutlineItemCollection(doc.Outlines);
```

## Paso 4: Establezca el nivel de zoom

¡Aquí es donde ocurre la magia! Puedes ajustar el nivel de zoom usando el `XYZExplicitDestination` Clase. En este ejemplo, estableceremos el nivel de zoom en 0, lo que significa que el documento heredará el nivel de zoom del visor.

```csharp
XYZExplicitDestination dest = new XYZExplicitDestination(2, 100, 100, 0);
```

## Paso 5: Agregar la acción a la colección de contornos

Ahora que ya tienes establecido tu destino, es momento de agregar esta acción a la colección de contornos del PDF.

```csharp
item.Action = new GoToAction(dest);
```

## Paso 6: Agregar el elemento a la colección de contornos

A continuación, deberá agregar el elemento a la colección de contornos del archivo PDF. Este paso garantiza que se guarden los cambios.

```csharp
doc.Outlines.Add(item);
```

## Paso 7: Guardar el PDF de salida

Finalmente, debe guardar el documento PDF modificado. Especifique la ruta donde desea guardar el nuevo archivo.

```csharp
dataDir = dataDir + "InheritZoom_out.pdf";
doc.Save(dataDir);
```

## Paso 8: Confirmar la actualización

Para finalizar, imprimamos un mensaje de confirmación en la consola para informarnos que todo salió bien.

```csharp
Console.WriteLine("\nBookmarks updated successfully.\nFile saved at " + dataDir);
```

## Conclusión

¡Listo! Has heredado correctamente el nivel de zoom en tus archivos PDF con Aspose.PDF para .NET. Esta sencilla pero potente función puede mejorar enormemente la experiencia del usuario, haciendo que tus documentos sean más accesibles y fáciles de navegar. Así que, la próxima vez que crees un PDF, ¡recuerda configurar el nivel de zoom!

## Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?
Aspose.PDF para .NET es una potente biblioteca que permite a los desarrolladores crear, manipular y convertir documentos PDF mediante programación.

### ¿Puedo utilizar Aspose.PDF gratis?
Sí, Aspose ofrece una versión de prueba gratuita que puedes usar para probar la biblioteca. Puedes descargarla. [aquí](https://releases.aspose.com/).

### ¿Dónde puedo encontrar la documentación?
Puede encontrar la documentación de Aspose.PDF para .NET [aquí](https://reference.aspose.com/pdf/net/).

### ¿Cómo compro una licencia?
Puedes comprar una licencia de Aspose.PDF para .NET [aquí](https://purchase.aspose.com/buy).

### ¿Qué pasa si necesito ayuda?
Si necesita ayuda, puede visitar el foro de soporte de Aspose [aquí](https://forum.aspose.com/c/pdf/10).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}