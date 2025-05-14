---
"description": "Aprenda a configurar títulos de botones de opción en archivos PDF con Aspose.PDF para .NET. Esta guía paso a paso le guiará en la carga, modificación y guardado de sus formularios PDF."
"linktitle": "Establecer título del botón de opción"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Establecer título del botón de opción"
"url": "/es/net/programming-with-forms/set-radio-button-caption/"
"weight": 280
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Establecer título del botón de opción

## Introducción

Si te estás iniciando en la manipulación de PDF con Aspose.PDF para .NET, ¡te espera una sorpresa! Hoy nos centraremos en una función práctica: configurar los títulos de los botones de opción en tus formularios PDF. Los botones de opción son esenciales para los formularios de usuario donde necesitas elegir entre un conjunto de opciones. Imagínalos como preguntas de opción múltiple con solo una respuesta. Este tutorial te guiará en el proceso de actualizar los títulos de los botones de opción en un formulario PDF, para que tus documentos sean interactivos y fáciles de usar. 

## Prerrequisitos

Antes de sumergirte en el código, hay algunas cosas que deberás asegurarte de tener:

1. Aspose.PDF para .NET: Asegúrese de tener instalada la biblioteca Aspose.PDF. Esta biblioteca le ayudará a manipular archivos PDF mediante programación.
2. Entorno de desarrollo: debe tener configurado un entorno de desarrollo .NET, como Visual Studio.
3. Formulario PDF de muestra: Para este tutorial, necesitará un formulario PDF de muestra con botones de opción. Puede usar cualquier formulario PDF existente o crear uno nuevo con botones de opción.
4. Conocimientos básicos de C#: esta guía asume que tienes un conocimiento básico de los conceptos de programación de C# y .NET.

Si aún no ha instalado Aspose.PDF para .NET o necesita una licencia temporal, puede [Descárgalo aquí](https://releases.aspose.com/pdf/net/) o [obtener una licencia temporal](https://purchase.aspose.com/temporary-license/).

## Importar paquetes

Para empezar, necesitas importar los paquetes necesarios en tu proyecto de C#. Aquí te explicamos cómo incluir la biblioteca Aspose.PDF:

```csharp
using System;
using Aspose.Pdf.Forms;
using System.Collections.Generic;
using Aspose.Pdf.Text;
```

Asegúrese de tener estos paquetes agregados a su proyecto a través de NuGet o su método preferido.

## Paso 1: Cargue el formulario PDF

Primero, debe cargar el formulario PDF que contiene los botones de opción. `Aspose.Pdf.Facades.Form` La clase se utiliza para este propósito. Así es como se hace:

```csharp
// Define la ruta a tu directorio de documentos
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Cargar el formulario PDF de origen
Aspose.Pdf.Facades.Form form1 = new Aspose.Pdf.Facades.Form(dataDir + "RadioButtonField.pdf");
Document PDF_Template_PDF_HTML = new Document(dataDir + "RadioButtonField.pdf");
```

En este fragmento de código:
- `dataDir` Especifica la ruta donde se encuentra su PDF.
- `Form` La clase se utiliza para interactuar con los campos de formulario dentro del PDF.
- `Document` La clase proporciona acceso a las páginas del documento PDF.

## Paso 2: Iterar a través de los campos del botón de opción

A continuación, deberá iterar a través de los campos de su formulario para identificar y manipular los campos del botón de opción:

```csharp
foreach (var item in form1.FieldNames)
{
    Console.WriteLine(item.ToString());
    Dictionary<string, string> radioOptions = form1.GetButtonOptionValues(item);
```

En este bucle:
- `FieldNames` Proporciona una lista de todos los nombres de campos en el PDF.
- `GetButtonOptionValues(item)` recupera las opciones disponibles para cada botón de opción.

## Paso 3: Modificar las opciones del botón de opción

Una vez identificados los campos del botón de opción, puede modificar sus opciones. Para ello, debe convertir el campo a `RadioButtonField` y actualizar sus opciones:

```csharp
    if (item.Contains("radio1"))
    {
        Aspose.Pdf.Forms.RadioButtonField field0 = PDF_Template_PDF_HTML.Form[item] as Aspose.Pdf.Forms.RadioButtonField;
        Aspose.Pdf.Forms.RadioButtonOptionField fieldoption = new Aspose.Pdf.Forms.RadioButtonOptionField();
        fieldoption.OptionName = "Yes";
        fieldoption.PartialName = "Yesname";
```

Aquí:
- Comprobamos si el nombre del campo contiene "radio1" para identificar el campo de botón de opción específico que queremos modificar.
- `RadioButtonField` Se emite desde los campos del formulario para realizar modificaciones específicas.

## Paso 4: Establezca el título para el botón de opción

Para configurar o actualizar el título del botón de opción, deberá crear un `TextFragment` uso `TextBuilder` Para colocarlo en la ubicación deseada:

```csharp
        var updatedFragment = new Aspose.Pdf.Text.TextFragment("test123");
        updatedFragment.TextState.Font = FontRepository.FindFont("Arial");
        updatedFragment.TextState.FontSize = 10;
        updatedFragment.TextState.LineSpacing = 6.32f;

        // Crear objeto TextParagraph
        TextParagraph par = new TextParagraph();
        // Establecer la posición del párrafo
        par.Position = new Position(field0.Rect.LLX, field0.Rect.LLY + updatedFragment.TextState.FontSize);
        // Especificar el modo de ajuste de línea
        par.FormattingOptions.WrapMode = TextFormattingOptions.WordWrapMode.ByWords;
        // Agregar nuevo TextFragment al párrafo
        par.AppendLine(updatedFragment);
        // Agregue el TextParagraph usando TextBuilder
        TextBuilder textBuilder = new TextBuilder(PDF_Template_PDF_HTML.Pages[1]);
        textBuilder.AppendParagraph(par);
```

En esta parte:
- `TextFragment` Se utiliza para definir el texto y su apariencia.
- `TextParagraph` Ayuda a posicionar y formatear el texto.
- `TextBuilder` Agrega el texto a la página especificada del PDF.

## Paso 5: Guarde el PDF actualizado

Por último, guarde el PDF actualizado en un nuevo archivo:

```csharp
        field0.DeleteOption("item1");
    }
}
PDF_Template_PDF_HTML.Save(dataDir + "RadioButtonField_out.pdf");
```

Esto garantizará que:
- Los cambios se aplican al PDF.
- La opción del botón de opción original se elimina según lo especificado.

## Conclusión

Modificar los títulos de los botones de opción en un formulario PDF con Aspose.PDF para .NET puede mejorar considerablemente la interactividad y la usabilidad de sus documentos. Con los pasos descritos en este tutorial, podrá cargar fácilmente un PDF, actualizar las opciones de los botones de opción y guardar los cambios. Este método es práctico para la gestión de formularios y garantiza que sus PDF satisfagan las necesidades específicas de sus usuarios. ¡Explore Aspose.PDF y explore sus funciones para otras manipulaciones de PDF!

## Preguntas frecuentes

### ¿Puedo actualizar varios campos de botón de opción a la vez?
Sí, puede iterar a través de todos los campos del botón de opción y aplicar cambios según sea necesario.

### ¿Necesito una licencia para utilizar Aspose.PDF?
Puede comenzar con una prueba gratuita, pero se requiere una licencia para un uso prolongado. [Obtenga una licencia aquí](https://purchase.aspose.com/buy).

### ¿Cómo puedo probar los cambios antes de guardar el PDF?
Puede obtener una vista previa del PDF en su entorno de desarrollo o utilizar un visor de PDF para comprobar las modificaciones.

### ¿Aspose.PDF es compatible con todas las versiones .NET?
Aspose.PDF es compatible con varias versiones de .NET. Asegúrese de comprobar la compatibilidad con su versión específica de .NET.

### ¿Puedo manipular otros campos de formulario de manera similar?
Sí, se pueden aplicar técnicas similares a otros tipos de campos de formulario en documentos PDF.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}