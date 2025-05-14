---
"description": "Aprenda a crear botones de opción alineados horizontal y verticalmente en PDF usando Aspose.PDF para .NET con este tutorial paso a paso."
"linktitle": "Botones de opción horizontales y verticales"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Botones de opción horizontales y verticales"
"url": "/es/net/programming-with-forms/horizontally-and-vertically-radio-buttons/"
"weight": 180
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Botones de opción horizontales y verticales

## Introducción

Crear formularios PDF interactivos puede mejorar significativamente la experiencia del usuario, especialmente al recopilar información. Uno de los elementos de formulario más comunes es el botón de opción, que permite a los usuarios seleccionar una opción de un conjunto. En este tutorial, exploraremos cómo crear botones de opción alineados horizontal y verticalmente con Aspose.PDF para .NET. Tanto si eres un desarrollador experimentado como si estás empezando, esta guía te guiará paso a paso por el proceso, asegurándote de que comprendas cada parte.

## Prerrequisitos

Antes de sumergirse en el código, hay algunos requisitos previos que debe tener en cuenta:

1. Aspose.PDF para .NET: Asegúrese de tener instalada la biblioteca Aspose.PDF. Puede descargarla desde [sitio](https://releases.aspose.com/pdf/net/).
2. Visual Studio: un entorno de desarrollo donde puedes escribir y probar tu código.
3. Conocimientos básicos de C#: la familiaridad con la programación en C# le ayudará a comprender mejor los fragmentos de código.

## Importar paquetes

Para empezar, necesitas importar los paquetes necesarios en tu proyecto de C#. Así es como puedes hacerlo:

### Crear un nuevo proyecto

Abra Visual Studio y cree un nuevo proyecto de C#. Puede elegir una aplicación de consola para simplificar.

### Añadir referencia de Aspose.PDF

1. Haga clic derecho en su proyecto en el Explorador de soluciones.
2. Seleccione "Administrar paquetes NuGet".
3. Busque "Aspose.PDF" e instale la última versión.

```csharp
using System;
using System.IO;
using Aspose.Pdf.Facades;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
```

Ahora que tienes todo configurado, analicemos el código para crear botones de opción alineados horizontal y verticalmente.

## Paso 1: Configurar el directorio de documentos

En este paso definiremos la ruta al directorio donde se almacenarán sus documentos PDF.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
```

Reemplazar `"YOUR DOCUMENT DIRECTORY"` Con la ruta donde desea guardar su archivo PDF. Esto es crucial, ya que le indica al programa dónde buscar los archivos de entrada y dónde guardar el de salida.

## Paso 2: Cargue el documento PDF existente

A continuación, necesitamos cargar el documento PDF con el que trabajaremos. Esto se hace usando el `FormEditor` clase.

```csharp
FormEditor formEditor = new FormEditor();
formEditor.BindPdf(dataDir + "input.pdf");
```

Aquí, creamos una instancia de `FormEditor` y vincularlo a un archivo PDF existente llamado `input.pdf`Asegúrese de que este archivo exista en el directorio especificado.

## Paso 3: Configurar las propiedades del botón de opción

Ahora, configuremos algunas propiedades para nuestros botones de opción. Esto incluye la separación entre ellos, su orientación y su tamaño.

```csharp
formEditor.RadioGap = 4; // Distancia entre las opciones de los botones de opción
formEditor.RadioHoriz = true; // Establecer como verdadero para la alineación horizontal
formEditor.RadioButtonItemSize = 20; // Tamaño del botón de opción
formEditor.Facade.BorderWidth = 1; // Ancho del borde
formEditor.Facade.BorderColor = System.Drawing.Color.Black; // Color del borde
```

Estas propiedades ayudarán a definir cómo aparecerán los botones de opción en el PDF. `RadioGap` La propiedad controla el espacio entre los botones, mientras que `RadioHoriz` determina su diseño.

## Paso 4: Agregar botones de opción horizontales

Ahora, agreguemos los botones de opción horizontales al PDF.

```csharp
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField1", 1, 40, 600, 120, 620);
```

En este código, definimos los elementos para los botones de opción y los agregamos al PDF. `AddField` El método toma varios parámetros, incluido el tipo de campo, el nombre del campo y las coordenadas para la ubicación.

## Paso 5: Agregar botones de opción verticales

A continuación, agregaremos los botones de opción verticales. Para ello, debemos volver a cambiar la orientación a vertical.

```csharp
formEditor.RadioHoriz = false; // Establecer como falso para la alineación vertical
formEditor.Items = new string[] { "First", "Second", "Third" };
formEditor.AddField(FieldType.Radio, "NewField2", 1, 40, 500, 60, 550);
```

Al igual que antes, definimos los elementos y los agregamos al PDF, pero esta vez estarán alineados verticalmente.

## Paso 6: Guarde el documento PDF

Por último, necesitamos guardar el documento PDF modificado.

```csharp
dataDir = dataDir + "HorizontallyAndVerticallyRadioButtons_out.pdf";
formEditor.Save(dataDir);
Console.WriteLine("\nHorizontally and vertically laid out radio buttons successfully.\nFile saved at " + dataDir);
```

Este código guarda el PDF con los nuevos botones de opción. Asegúrese de verificar el directorio especificado para el archivo de salida.

## Conclusión

Crear botones de opción en un PDF con Aspose.PDF para .NET es un proceso sencillo. Siguiendo los pasos de este tutorial, podrá agregar fácilmente botones de opción alineados horizontal y verticalmente a sus formularios PDF. Esto no solo mejora la interactividad de sus documentos, sino también la experiencia general del usuario. ¡Anímese a probarlo!

## Preguntas frecuentes

### ¿Qué es Aspose.PDF para .NET?
Aspose.PDF para .NET es una potente biblioteca que permite a los desarrolladores crear, manipular y convertir documentos PDF mediante programación.

### ¿Puedo utilizar Aspose.PDF gratis?
Sí, Aspose ofrece una versión de prueba gratuita que puedes usar para evaluar la biblioteca. Puedes descargarla. [aquí](https://releases.aspose.com/).

### ¿Cómo puedo obtener soporte para Aspose.PDF?
Puede obtener ayuda visitando el [Foro de Aspose](https://forum.aspose.com/c/pdf/10).

### ¿Es posible crear otros elementos de formulario con Aspose.PDF?
¡Por supuesto! Aspose.PDF admite varios elementos de formulario, como campos de texto, casillas de verificación y menús desplegables.

### ¿Dónde puedo comprar Aspose.PDF para .NET?
Puede comprar Aspose.PDF para .NET en [página de compra](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}