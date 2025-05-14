---
"description": "Aprenda a etiquetar imágenes en archivos PDF existentes con Aspose.PDF para .NET. Guía paso a paso para mejorar la accesibilidad con compatibilidad con PDF/UA."
"linktitle": "Etiquetar imagen en un PDF existente"
"second_title": "Referencia de la API de Aspose.PDF para .NET"
"title": "Etiquetar imagen en un PDF existente"
"url": "/es/net/programming-with-tagged-pdf/tag-image-in-existing-pdf/"
"weight": 210
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Etiquetar imagen en un PDF existente

## Introducción

En este tutorial, le mostraremos cómo etiquetar una imagen en un PDF existente con Aspose.PDF para .NET. Al finalizar esta guía, podrá configurar texto alternativo para imágenes, ajustar atributos de diseño y garantizar que su PDF cumpla con los estándares de accesibilidad.

## Prerrequisitos

Antes de comenzar, repasemos lo que necesitarás para comenzar:

- Aspose.PDF para .NET: asegúrese de haber descargado e instalado la última versión de Aspose.PDF para .NET. [Descargar aquí](https://releases.aspose.com/pdf/net/).
- .NET Framework: asegúrese de tener configurado un entorno de desarrollo .NET como Visual Studio.
- Comprensión básica de la estructura de PDF: familiaridad con los elementos de la estructura de PDF, como párrafos, espacios, tablas e imágenes.
- Una licencia válida: puedes comprar una licencia [aquí](https://purchase.aspose.com/buy) o utilizar uno temporal [aquí](https://purchase.aspose.com/temporary-license/).

## Importar paquetes

Para empezar a codificar, necesitas importar los espacios de nombres esenciales de Aspose.PDF para .NET. Estos te darán acceso a las clases y métodos necesarios para manipular el documento PDF.

```csharp
using Aspose.Pdf.LogicalStructure;
using Aspose.Pdf.Tagged;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Ahora que hemos preparado el escenario, dividamos el proceso de etiquetado de una imagen en varios pasos.

## Paso 1: Cargue el documento PDF existente

El primer paso es cargar el archivo PDF con el que desea trabajar. Puede ser cualquier archivo PDF con una imagen que desee etiquetar.

```csharp
// La ruta al directorio de documentos.
string dataDir = "YOUR DOCUMENT DIRECTORY";
string inFile = dataDir + "TH.pdf";
string outFile = dataDir + "TH_out.pdf";
string logFile = dataDir + "TH_out.xml";

// Abrir el documento
Document document = new Document(inFile);
```

- Reemplazar `"YOUR DOCUMENT DIRECTORY"` con la ruta real a su archivo.
- El `Document` Esta clase permite cargar un PDF existente. Modificarás este PDF para etiquetar la imagen.

## Paso 2: Acceder al contenido etiquetado y al elemento de estructura raíz

Una vez abierto el PDF, el siguiente paso es acceder al contenido etiquetado e identificar el elemento raíz de la estructura. Esto es crucial, ya que permite navegar por los elementos del PDF y realizar modificaciones.

```csharp
// Obtener contenido etiquetado y elemento de estructura raíz
ITaggedContent taggedContent = document.TaggedContent;
StructureElement rootElement = taggedContent.RootElement;
```

- `TaggedContent` Proporciona acceso a los elementos estructurados en el PDF.
- El `RootElement` Es el elemento de estructura superior, desde el cual se puede pasar a otros elementos como párrafos, tablas e imágenes.

## Paso 3: Establezca el título para el documento PDF etiquetado

Agregar un título al documento PDF etiquetado garantiza que su documento esté correctamente etiquetado, lo que es útil para la accesibilidad y el cumplimiento de PDF/UA.

```csharp
// Establecer título para el documento PDF etiquetado
taggedContent.SetTitle("Document with images");
```

- Establecer un título para su PDF etiquetado mejora la accesibilidad y mejora la claridad del documento para los lectores de pantalla y las tecnologías de asistencia.

## Paso 4: Busque y etiquete la imagen

Ahora, busquemos el elemento de imagen (al que se hace referencia como `FigureElement` en Aspose.PDF), establezca un texto alternativo para él y configure sus atributos de diseño.

```csharp
// Recorrer todos los elementos de la figura (imágenes) y establecer texto alternativo y atributos de diseño
foreach (FigureElement figureElement in rootElement.FindElements<FigureElement>(true))
{
    // Establecer texto alternativo para la figura
    figureElement.AlternativeText = "Figure alternative text (technique 2)";
    
    // Crear y configurar el atributo BBox (cuadro delimitador)
    StructureAttribute bboxAttribute = new StructureAttribute(AttributeKey.BBox);
    bboxAttribute.SetRectangleValue(new Aspose.Pdf.Rectangle(0.0, 0.0, 100.0, 100.0));
    
    // Establecer atributos de diseño para la figura
    StructureAttributes figureLayoutAttributes = figureElement.Attributes.GetAttributes(AttributeOwnerStandard.Layout);
    figureLayoutAttributes.SetAttribute(bboxAttribute);
}
```

- Este código recorre todos los `FigureElement` objetos en la estructura raíz, que representan imágenes.
- Establece el texto alternativo para accesibilidad (los lectores de pantalla lo usarán para describir la imagen).
- El cuadro delimitador (`BBox`) especifica las coordenadas para el diseño de la imagen, garantizando que se muestre correctamente en el documento.

## Paso 5: Modificar elementos Span dentro de la tabla

En algunos casos, puede que necesite modificar elementos de extensión dentro de una tabla. Aquí le mostraremos cómo encontrar un `SpanElement` y moverlo a un párrafo.

```csharp
// Encuentre los elementos de tabla, lapso y párrafo
TableElement tableElement = rootElement.FindElements<TableElement>(true)[0];
SpanElement spanElement = tableElement.FindElements<SpanElement>(true)[0];
TableTDElement firstTdElement = tableElement.FindElements<TableTDElement>(true)[0];
ParagraphElement paragraph = firstTdElement.FindElements<ParagraphElement>(true)[0];

// Mueva el elemento span al párrafo
spanElement.ChangeParentElement(paragraph);
```

- Aquí, localizamos el `TableElement`, `SpanElement`, y `ParagraphElement` dentro del PDF.
- Usando el `ChangeParentElement` Método, movemos el espacio dentro del párrafo para garantizar una estructura y etiquetado adecuados.

## Paso 6: Guarde el documento y valide la conformidad con PDF/UA

Una vez realizados todos los cambios, el paso final es guardar el PDF actualizado y verificar si cumple con los estándares PDF/UA.

```csharp
// Guardar el documento PDF actualizado
document.Save(outFile);

// Validar la conformidad con PDF/UA
document = new Document(outFile);
bool isPdfUaCompliance = document.Validate(logFile, PdfFormat.PDF_UA_1);
Console.WriteLine(String.Format("PDF/UA compliance: {0}", isPdfUaCompliance));
```

- El `Validate` El método verifica el documento PDF con los estándares PDF/UA y registra los resultados.
- Garantizar el cumplimiento ayuda a mejorar la accesibilidad y cumplir los requisitos reglamentarios para la publicación de documentos.

## Conclusión

En este tutorial, le mostramos cómo etiquetar imágenes en un PDF existente con Aspose.PDF para .NET. Al configurar texto alternativo, ajustar los atributos de diseño y validar la compatibilidad del documento con PDF/UA, puede garantizar que sus PDF sean accesibles y cumplan con los estándares modernos. Aspose.PDF facilita el trabajo con elementos estructurados, lo que le permite controlar el diseño y la accesibilidad de su documento.

## Preguntas frecuentes

### ¿Para qué se utiliza Aspose.PDF para .NET?
Aspose.PDF para .NET es una potente biblioteca utilizada para crear, editar y manipular documentos PDF mediante programación en un entorno .NET.

### ¿Cómo puedo garantizar la conformidad con PDF/UA?
Puedes utilizar Aspose.PDF `Validate` Método para verificar la conformidad con PDF/UA después de realizar modificaciones en el documento.

### ¿Qué es el texto alternativo en archivos PDF?
El texto alternativo es una descripción que se agrega a las imágenes en archivos PDF para mejorar la accesibilidad, especialmente para los usuarios que dependen de lectores de pantalla.

### ¿Puedo manipular tablas y espacios en un PDF con Aspose.PDF?
Sí, Aspose.PDF le permite manipular tablas, intervalos y otros elementos estructurados dentro de un documento PDF.

### ¿Dónde puedo descargar Aspose.PDF para .NET?
Puede descargar la última versión de Aspose.PDF para .NET [aquí](https://releases.aspose.com/pdf/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}