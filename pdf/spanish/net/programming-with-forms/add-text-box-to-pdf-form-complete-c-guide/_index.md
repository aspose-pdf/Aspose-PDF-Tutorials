---
category: general
date: 2026-06-18
description: Añade un cuadro de texto a un formulario PDF rápidamente. Aprende cómo
  crear un cuadro de texto PDF rellenable y cómo agregar un campo de comentarios PDF
  usando Aspose.PDF para .NET.
draft: false
keywords:
- add text box to pdf form
- create fillable pdf textbox
- how to add comment field pdf
language: es
og_description: Agregar cuadro de texto a un formulario PDF con Aspose.PDF para .NET.
  Este tutorial muestra cómo crear un cuadro de texto PDF rellenable y cómo añadir
  un campo de comentario PDF en solo unas pocas líneas.
og_title: Agregar cuadro de texto a formulario PDF – Guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  headline: Add Text Box to PDF Form – Complete C# Guide
  type: TechArticle
- description: Add text box to PDF form quickly. Learn how to create fillable PDF
    textbox and how to add comment field PDF using Aspose.PDF for .NET.
  name: Add Text Box to PDF Form – Complete C# Guide
  steps:
  - name: – Load the PDF document
    text: We need a `Document` object that represents the existing file. Aspose.PDF
      makes this a one‑liner.
  - name: – Create a TextBox field on the target page
    text: We’ll place the textbox on page 1 (index 0) inside a rectangle that defines
      its size and position. The rectangle uses points (1 inch = 72 points).
  - name: – Assign a name to the field
    text: Every form field needs a unique identifier. This name is what you’ll reference
      later when extracting data.
  - name: – Enable multiple widget annotations (optional but handy)
    text: If you want the same textbox to appear on several pages, set `MultipleWidgetAnnotations`
      to `true`. For a single‑page comment field you can skip this, but it doesn’t
      hurt.
  - name: – Add the TextBox field to the document’s form collection
    text: Now the field becomes part of the PDF’s interactive form.
  - name: – Save the modified PDF
    text: Finally, write the changes back to disk.
  - name: Can I set a default value?
    text: Yes. Just assign `textBox.Value = "Enter your comment here";` before adding
      the field.
  - name: What if I need a multiline textbox?
    text: 'Set the `IsMultiline` property:'
  - name: How do I change the appearance (border, background)?
    text: '```csharp textBox.BorderColor = Color.Black; textBox.BorderWidth = 1; textBox.BackgroundColor
      = Color.LightYellow; ```'
  - name: Does this work with PDF/A or encrypted PDFs?
    text: 'Aspose.PDF can handle PDF/A‑1b, PDF/A‑2b, and encrypted files as long as
      you provide the password when loading:'
  type: HowTo
tags:
- pdf
- csharp
- pdf-form
- textbox
- aspnet
title: Agregar cuadro de texto a formulario PDF – Guía completa de C#
url: /es/net/programming-with-forms/add-text-box-to-pdf-form-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Añadir cuadro de texto a formulario PDF – Guía completa en C#

¿Alguna vez necesitaste **añadir un cuadro de texto a un formulario PDF** pero no estabas seguro de qué llamadas a la API usar? No eres el único. Ya sea que estés construyendo un recopilador de comentarios, un portal de firma de contratos o un simple campo de observaciones, un cuadro de texto rellenable es la solución ideal. En esta guía recorreremos paso a paso los pasos exactos para **crear un cuadro de texto PDF rellenable** y también responderemos la consulta frecuente **cómo añadir un campo de comentario PDF** usando Aspose.PDF para .NET.

Comenzaremos con un PDF limpio, añadiremos un cuadro de texto en la página 1, le daremos un nombre amigable, habilitaremos varios widgets y, finalmente, guardaremos el resultado. Al final tendrás un PDF listo para usar que cualquiera podrá abrir en Adobe Reader, escribir un comentario y pulsar Guardar. Sin herramientas externas, sin edición manual—solo código puro en C#.

## Requisitos previos

- .NET 6.0 o superior (el código también funciona con .NET Framework 4.7+)
- Visual Studio 2022 o cualquier IDE que prefieras
- Paquete NuGet Aspose.PDF para .NET (`Install-Package Aspose.PDF`)
- Un PDF de origen (`input.pdf`) ubicado en una carpeta que controles  

Eso es todo. Si ya tienes esos elementos, puedes continuar.

## Añadir cuadro de texto a formulario PDF con C#

A continuación está el corazón del tutorial. Cada paso se explica y luego sigue el fragmento de C# correspondiente. Siéntete libre de copiar‑pegar todo el bloque en una aplicación de consola; compila y se ejecuta tal cual.

### Paso 1 – Cargar el documento PDF

Necesitamos un objeto `Document` que represente el archivo existente. Aspose.PDF lo hace en una sola línea.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing;

// Load the source PDF
Document doc = new Document(@"C:\MyPdfs\input.pdf");
```

*Por qué es importante:* Cargar el PDF nos da acceso a sus páginas, anotaciones y a la colección de formularios donde viven los campos. Sin una instancia de `Document` no podemos añadir nada.

### Paso 2 – Crear un campo TextBox en la página objetivo

Colocaremos el cuadro de texto en la página 1 (índice 0) dentro de un rectángulo que define su tamaño y posición. El rectángulo usa puntos (1 pulgada = 72 puntos).

```csharp
// Define the rectangle: left, bottom, right, top
Rectangle rect = new Rectangle(100, 600, 300, 630);

// Create the TextBox field on page 1
TextBoxField textBox = new TextBoxField(doc.Pages[1], rect);
```

*Por qué es importante:* El rectángulo determina dónde verá el usuario el campo. Ajusta las coordenadas para que encajen en tu diseño. La clase `TextBoxField` hereda automáticamente propiedades visuales como borde y fondo.

### Paso 3 – Asignar un nombre al campo

Cada campo de formulario necesita un identificador único. Este nombre será el que referencies más adelante al extraer datos.

```csharp
textBox.FieldName = "Comments";
```

*Por qué es importante:* Nombrar el campo `"Comments"` te permite recuperar la entrada del usuario con `doc.Form["Comments"]` después de que el PDF haya sido completado. También aparece en la lista de campos de los lectores de PDF.

### Paso 4 – Habilitar múltiples anotaciones de widget (opcional pero útil)

Si deseas que el mismo cuadro de texto aparezca en varias páginas, establece `MultipleWidgetAnnotations` a `true`. Para un campo de comentario de una sola página puedes omitirlo, pero no causa problemas.

```csharp
textBox.MultipleWidgetAnnotations = true;
```

*Por qué es importante:* Múltiples widgets comparten los mismos datos, de modo que el usuario escribe una vez y ve el mismo comentario en cada página que contiene el widget. Es un truco práctico para contratos de varias páginas.

### Paso 5 – Añadir el campo TextBox a la colección de formularios del documento

Ahora el campo pasa a ser parte del formulario interactivo del PDF.

```csharp
doc.Form.Add(textBox);
```

*Por qué es importante:* Añadir el campo lo registra en el diccionario AcroForm del PDF. Sin este paso, el cuadro de texto existiría solo en memoria y nunca aparecería en el archivo guardado.

### Paso 6 – Guardar el PDF modificado

Finalmente, escribe los cambios de vuelta al disco.

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

*Por qué es importante:* Guardar persiste el nuevo campo de formulario. Abre `output.pdf` en Adobe Reader y verás un cuadro de texto vacío etiquetado “Comments” listo para escribir.

## Ejemplo completo funcional

Juntando todo, aquí tienes una aplicación de consola autocontenida que puedes ejecutar de inmediato:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Forms;
using System.Drawing; // for Rectangle

namespace PdfFormDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the existing PDF
            string inputPath = @"C:\MyPdfs\input.pdf";
            Document doc = new Document(inputPath);

            // 2️⃣ Define the rectangle where the textbox will live
            Rectangle rect = new Rectangle(100, 600, 300, 630);

            // 3️⃣ Create the TextBox field on page 1 (index 1)
            TextBoxField textBox = new TextBoxField(doc.Pages[1], rect)
            {
                // 4️⃣ Give it a meaningful name
                FieldName = "Comments",

                // 5️⃣ Allow the same widget on multiple pages (optional)
                MultipleWidgetAnnotations = true
            };

            // 6️⃣ Add the field to the form collection
            doc.Form.Add(textBox);

            // 7️⃣ Save the updated PDF
            string outputPath = @"C:\MyPdfs\output.pdf";
            doc.Save(outputPath);

            Console.WriteLine("✅ Text box added successfully! Check " + outputPath);
        }
    }
}
```

**Salida esperada:** Cuando abras `output.pdf` verás un área rectangular de entrada en la página 1. Al hacer clic dentro podrás escribir cualquier comentario. El campo persiste después de guardar, lo que significa que has respondido con éxito a **cómo añadir un campo de comentario PDF**.

## Preguntas frecuentes y casos especiales

### ¿Puedo establecer un valor predeterminado?

Sí. Simplemente asigna `textBox.Value = "Enter your comment here";` antes de añadir el campo.

### ¿Qué pasa si necesito un cuadro de texto multilínea?

Establece la propiedad `IsMultiline`:

```csharp
textBox.IsMultiline = true;
textBox.MaxLength = 500; // optional limit
```

### ¿Cómo cambio la apariencia (borde, fondo)?

```csharp
textBox.BorderColor = Color.Black;
textBox.BorderWidth = 1;
textBox.BackgroundColor = Color.LightYellow;
```

### ¿Funciona con PDF/A o PDFs encriptados?

Aspose.PDF puede manejar PDF/A‑1b, PDF/A‑2b y archivos encriptados siempre que proporciones la contraseña al cargar:

```csharp
Document doc = new Document(inputPath, new LoadOptions { Password = "secret" });
```

### ¿Qué pasa si necesito el cuadro de texto en una página diferente?

Reemplaza `doc.Pages[1]` por el índice de página deseado (`doc.Pages[2]` para la página 3, etc.). Recuerda que las colecciones de páginas son **basadas en 1** en Aspose.PDF.

## Consejos profesionales

- **Consejo pro:** Usa `doc.Form.RefreshAppearance();` después de añadir varios campos para asegurar que todos los widgets se rendericen correctamente en visores PDF antiguos.
- **Cuidado con:** Rectángulos superpuestos. Si dos campos comparten la misma zona, Acrobat puede ocultar uno de ellos.
- **Nota de rendimiento:** Al procesar miles de PDFs, reutiliza una única instancia de `Document` para la lectura y solo clona el campo de formulario para evitar asignaciones repetidas.

## Próximos pasos

Ahora que sabes cómo **añadir un cuadro de texto a un formulario PDF**, quizás quieras explorar temas relacionados:

- **Crear cuadro de texto PDF rellenable** con reglas de validación (`textBox.Validate = new RegExValidator("[A-Za-z0-9]+");`)
- **Añadir botones de opción o casillas de verificación** para construir un cuestionario completo
- **Aplanar el formulario** después del envío para evitar ediciones posteriores (`doc.Form.Flatten();`)
- **Extraer los datos introducidos** usando `doc.Form["Comments"].Value` y almacenarlos en una base de datos

Todo esto se basa en los mismos conceptos centrales que cubrimos, así que estás bien posicionado para ampliar tu kit de herramientas de automatización PDF.

---

*¡Feliz codificación! Si encuentras algún inconveniente, deja un comentario abajo y lo solucionaremos juntos.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Add TextBox Fields in PDFs Using Aspose.PDF for .NET&#58; A Step-by-Step Guide](/pdf/english/net/forms-annotations/add-textbox-field-aspose-pdf-net/)
- [How to Add and Extract PDF Form Fields Using Aspose.PDF for .NET&#58; A Comprehensive Guide](/pdf/english/net/forms-annotations/manage-pdf-form-fields-aspose-dotnet/)
- [How to Add Tooltips to PDF Text Using Aspose.PDF for .NET ( Forms & Annotations )](/pdf/english/net/forms-annotations/aspose-pdf-net-add-tooltips-pdfs/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}