---
title: Agregar Encabezado, Idioma y Título a un PDF usando Aspose.PDF for .NET
weight: 110
limit:
description: Cree un PDF, establezca su idioma y título, y agregue un encabezado de nivel 1 con Aspose.PDF for .NET.
keywords: [Aspose.PDF for .NET, add heading pdf .net, set pdf language, pdf document title, ITaggedContent example, StructureElement pdf]
url: /net/programming-with-headings/add-heading/
date: '2026-09-29'
lastmod: '2026-09-29'
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Cree un PDF, establezca su idioma y título, y agregue un encabezado
    de nivel 1 con Aspose.PDF for .NET.
  headline: Agregar Encabezado, Idioma y Título a un PDF usando Aspose.PDF for .NET
  type: TechArticle
- description: Cree un PDF, establezca su idioma y título, y agregue un encabezado
    de nivel 1 con Aspose.PDF for .NET.
  name: Agregar Encabezado, Idioma y Título a un PDF usando Aspose.PDF for .NET
  steps:
  - name: Defina el nombre del archivo de salida para el PDF generado.
    text: Defina el nombre del archivo de salida para el PDF generado.
  - name: Cree una nueva instancia vacía de documento PDF (`pdfDoc`) dentro de un
      bloque `using`.
    text: Cree una nueva instancia vacía de documento PDF (`pdfDoc`) dentro de un
      bloque `using`.
  - name: Obtenga la interfaz `ITaggedContent` para trabajar con estructuras PDF etiquetadas.
    text: Obtenga la interfaz `ITaggedContent` para trabajar con estructuras PDF etiquetadas.
  - name: Establezca el idioma predeterminado del documento a English (US) y asigne
      un metadato de título.
    text: Establezca el idioma predeterminado del documento a English (US) y asigne
      un metadato de título.
  - name: Recupere el elemento raíz del árbol de estructura lógica.
    text: Recupere el elemento raíz del árbol de estructura lógica.
  - name: Cree un elemento de encabezado de nivel 1, establezca su texto visible y
      especifique su idioma.
    text: Cree un elemento de encabezado de nivel 1, establezca su texto visible y
      especifique su idioma.
  - name: Agregue el elemento de encabezado a la raíz, haciendo que el encabezado
      aparezca en el PDF.
    text: Agregue el elemento de encabezado a la raíz, haciendo que el encabezado
      aparezca en el PDF.
  - name: Guarde el PDF en el archivo especificado y cierre el ámbito del documento.
    text: Guarde el PDF en el archivo especificado y cierre el ámbito del documento.
  - name: Muestre un mensaje de confirmación en la consola.
    text: Muestre un mensaje de confirmación en la consola.
  type: HowTo
- questions:
  - answer: '`SetLanguage` define el idioma predeterminado para toda la estructura
      lógica del documento; cualquier elemento que no tenga su propio idioma establecido
      heredará \"en-US\".'
    question: ¿Cuál es el efecto de llamar a `tagContent.SetLanguage(\"en-US\")` en
      el PDF?
  - answer: Establecer `header.Language` es opcional; el encabezado heredará el idioma
      predeterminado del documento a menos que asigne un valor diferente, como se
      muestra en el ejemplo.
    question: ¿Necesito establecer `header.Language` si ya llamé a `SetLanguage` en
      el documento?
  - answer: Utilice `tagContent.CreateHeaderElement(2)` para crear un encabezado de
      nivel 2; el argumento numérico especifica el nivel de encabezado que se reflejará
      en el árbol de estructura del PDF.
    question: ¿Cómo puedo crear un encabezado de nivel 2 en lugar de un encabezado
      de nivel 1?
  - answer: '`SetTitle` escribe la cadena proporcionada en el campo de título de los
      metadatos del documento PDF, que puede verse en los lectores de PDF y usarse
      para búsqueda o indexación.'
    question: ¿Qué hace `tagContent.SetTitle(\"PDF Example with Header\")`?
  - answer: El elemento de encabezado no se añadirá al árbol de estructura lógica,
      por lo que no aparecerá en la salida del PDF ni será reconocido como encabezado
      por las herramientas de accesibilidad.
    question: ¿Qué ocurre si omito `rootElement.AppendChild(header)`?
  type: FAQPage
images:
- /net/programming-with-headings/add-heading/og-image.png
og_title: Insertar un encabezado y establecer el idioma en un PDF
og_description: Aprenda a crear un PDF, establecer su idioma y título, y luego agregar un encabezado de nivel 1 con unas pocas líneas de código .NET.
og_image_alt: Guía que muestra cómo agregar un encabezado, establecer el idioma y el título en un PDF usando Aspose.PDF for .NET
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar Encabezado, Idioma y Título a un PDF usando Aspose.PDF
Este tutorial le guía paso a paso para crear un nuevo documento PDF con Aspose.PDF for .NET, asignar un idioma predeterminado y un título al documento, e insertar un encabezado de nivel 1. Verá cómo trabajar con las clases Document, ITaggedContent, StructureElement y HeaderElement para producir un PDF correctamente etiquetado, adecuado para herramientas de accesibilidad.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-headings/add-heading" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: ¿Cuál es el efecto de llamar a `tagContent.SetLanguage(\"en-US\")` en el PDF?**  
A: `SetLanguage` define el idioma predeterminado para toda la estructura lógica del documento; cualquier elemento que no tenga su propio idioma establecido heredará \"en-US\".

**Q: ¿Necesito establecer `header.Language` si ya llamé a `SetLanguage` en el documento?**  
A: Establecer `header.Language` es opcional; el encabezado heredará el idioma predeterminado del documento a menos que asigne un valor diferente, como se muestra en el ejemplo.

**Q: ¿Cómo puedo crear un encabezado de nivel 2 en lugar de un encabezado de nivel 1?**  
A: Utilice `tagContent.CreateHeaderElement(2)` para crear un encabezado de nivel 2; el argumento numérico especifica el nivel de encabezado que se reflejará en el árbol de estructura del PDF.

**Q: ¿Qué hace `tagContent.SetTitle(\"PDF Example with Header\")`?**  
A: `SetTitle` escribe la cadena proporcionada en el campo de título de los metadatos del documento PDF, que puede verse en los lectores de PDF y usarse para búsqueda o indexación.

**Q: ¿Qué ocurre si omito `rootElement.AppendChild(header)`?**  
A: El elemento de encabezado no se añadirá al árbol de estructura lógica, por lo que no aparecerá en la salida del PDF ni será reconocido como encabezado por las herramientas de accesibilidad.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}