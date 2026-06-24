---
category: general
date: 2026-06-21
description: Crea un campo de texto PDF con C# y aprende cómo duplicar un campo de
  formulario PDF o agregar un cuadro de texto a un formulario PDF en solo unas pocas
  líneas de código.
draft: false
keywords:
- create pdf textbox field
- duplicate pdf form field
- add textbox to pdf form
- pdf form automation
- c# pdf library
language: es
og_description: Crea rápidamente un campo de texto PDF. Esta guía muestra cómo duplicar
  un campo de formulario PDF y agregar un cuadro de texto al formulario PDF usando
  una biblioteca PDF moderna de C#.
og_title: Crear campo de texto PDF – Tutorial completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  headline: Create PDF Textbox Field – Step‑by‑Step Guide
  type: TechArticle
- description: Create PDF textbox field with C# and learn how to duplicate PDF form
    field or add textbox to PDF form in just a few lines of code.
  name: Create PDF Textbox Field – Step‑by‑Step Guide
  steps:
  - name: What if I need the field on *more* than two pages?
    text: Just repeat the clone‑and‑add steps for each additional page. The underlying
      data object stays the same, so all widgets stay in sync.
  - name: How do I change the appearance (font, border, background)?
    text: Each `Widget` has a `SetBorderColor`, `SetBorderWidth`, and `SetBackgroundColor`
      method. You can also assign a default appearance string (`DA`) to control the
      font and size.
  - name: Can I make the field read‑only after the user fills it?
    text: Yes. Set the `ReadOnly` flag on the field after you’ve collected the data,
      or toggle it based on your workflow.
  - name: What about PDFs that already contain a form?
    text: If the document already has an AcroForm, `doc.GetForm()` simply returns
      it. You can then add new fields without disturbing existing ones. Just be careful
      to use unique field names.
  type: HowTo
tags:
- PDF
- C#
- FormFields
title: Crear campo de texto PDF – Guía paso a paso
url: /es/net/programming-with-forms/create-pdf-textbox-field-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF Textbox Field – Tutorial completo en C#

¿Alguna vez necesitaste **create PDF textbox field** pero no estabas seguro de qué llamadas API usar? No estás solo. Ya sea que estés construyendo un portal de firma de contratos o una hoja simple de captura de datos, agregar cuadros de texto interactivos a un PDF es una habilidad esencial para cualquier desarrollador de automatización de formularios.  

En esta guía recorreremos un ejemplo práctico que no solo **adds textbox to PDF form**, sino que también muestra cómo **duplicate PDF form field** para que la misma entrada aparezca en varias páginas. Al final tendrás un programa ejecutable que puedes incorporar en cualquier proyecto .NET.

## Lo que necesitarás

- .NET 6.0 o posterior (el código también funciona con .NET Core)  
- Una biblioteca PDF moderna para C# – el fragmento a continuación usa **PDFTron SDK**, pero los conceptos se pueden aplicar a iText 7, PdfSharp u otras bibliotecas.  
- Visual Studio 2022 (o cualquier IDE que prefieras)  

Eso es todo – sin servicios adicionales, sin dependencias obscuras. Si ya tienes un PDF que deseas ampliar, simplemente apunta el código a él.

---

## Paso 1: Configurar el proyecto e importar el SDK

Primero, crea una aplicación de consola:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
```

Agrega el paquete NuGet de PDFTron:

```bash
dotnet add package PDFTron.NET
```

Ahora abre `Program.cs` y agrega los espacios de nombres que necesitaremos:

```csharp
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;
```

> **Pro tip:** Si estás usando una biblioteca diferente, reemplaza las declaraciones `using` por sus equivalentes (p.ej., `iText.Kernel.Pdf` para iText 7).

## Paso 2: Inicializar el documento PDF y el formulario

Comenzaremos con un PDF nuevo que contiene dos páginas – la página de origen para el cuadro de texto original y una página de destino para el duplicado.

```csharp
PDFNet.Initialize();                     // Initialize the PDFTron runtime

// Create a new PDF document
using (PDFDoc doc = new PDFDoc())
{
    // Add two blank pages (letter size)
    Page sourcePage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(sourcePage);
    Page targetPage = doc.PageCreate(new Size(612, 792));
    doc.PagePushBack(targetPage);

    // Get (or create) the AcroForm object
    Form form = doc.GetForm();
```

El objeto `Form` es donde viven todos los campos interactivos. Si el documento no tenía ya un formulario, `GetForm()` crea uno para nosotros.

## Paso 3: **Create PDF Textbox Field** en la primera página

Ahora llega el núcleo de nuestro tutorial – crear un campo de texto. Las coordenadas del rectángulo se expresan en puntos (1 pulgada = 72 puntos). El ejemplo coloca el cuadro cerca de la parte superior‑central de la primera página.

```csharp
    // Step 1: Create a text box field on the first page and set its initial value
    TextBoxField textBoxField = new TextBoxField(sourcePage, new Rect(100, 500, 300, 520))
    {
        Value = "Sample"
    };
```

¿Por qué establecemos `Value` de inmediato? Pre‑poblar el campo le da a los usuarios una pista sobre la entrada esperada, y también demuestra que el campo funciona completamente.

## Paso 4: Añadir el campo al formulario – **Add Textbox to PDF Form**

A continuación, registramos el campo en el formulario usando un nombre lógico. Este nombre es el que referenciarás más adelante cuando necesites leer o modificar los datos del campo programáticamente.

```csharp
    // Step 2: Add the field to the form with a logical name
    form.Add(textBoxField, "multiBox");
```

Elegir un nombre claro (como `"multiBox"`) hace que el código posterior sea más fácil de entender, especialmente cuando tienes docenas de campos.

## Paso 5: **Duplicate PDF Form Field** en otra página

Un requisito común es mostrar el mismo campo en varias páginas – piensa en un cuadro de “Customer Name” que aparece en cada página de factura. PDFTron nos permite clonar la anotación del widget, que es la representación visual del campo.

```csharp
    // Step 3: Clone the field's widget annotation so it can appear on another page
    Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

    // Step 4: Place the cloned widget on the second page
    targetPage.Annotations.Add(clonedWidget);
```

El widget clonado comparte los mismos datos subyacentes que el cuadro de texto original. Cuando un usuario escribe en una instancia, la otra se actualiza automáticamente – esa es la magia de **duplicate PDF form field**.

## Paso 6: Guardar el documento y limpiar

Finalmente, escribe el PDF en disco y cierra el runtime de PDFNet.

```csharp
    // Save the resulting PDF
    doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
    Console.WriteLine("PDF created: output.pdf");
}

// Shut down PDFNet (optional but good practice)
PDFNet.Terminate();
```

Ejecutar el programa produce un PDF de dos páginas (`output.pdf`). Ábrelo en Adobe Acrobat Reader, haz clic en el cuadro de texto de la página 1, escribe algo, luego cambia a la página 2 – el mismo texto aparece instantáneamente. Ese es un ejemplo totalmente funcional de **create pdf textbox field** con un campo duplicado.

---

## Ejemplo completo funcional (listo para copiar‑pegar)

```csharp
// Program.cs
using System;
using pdftron;
using pdftron.Common;
using pdftron.PDF;
using pdftron.SDF;

class Program
{
    static void Main()
    {
        PDFNet.Initialize();

        using (PDFDoc doc = new PDFDoc())
        {
            // Create two pages
            Page sourcePage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(sourcePage);
            Page targetPage = doc.PageCreate(new Size(612, 792));
            doc.PagePushBack(targetPage);

            // Get the form (creates one if missing)
            Form form = doc.GetForm();

            // Step 1: Create a text box field on the first page
            TextBoxField textBoxField = new TextBoxField(sourcePage,
                new Rect(100, 500, 300, 520))
            {
                Value = "Sample"
            };

            // Step 2: Add the field to the form
            form.Add(textBoxField, "multiBox");

            // Step 3: Clone the widget so it appears on page 2
            Widget clonedWidget = textBoxField.CreateWidgetAnnotation();

            // Step 4: Attach the cloned widget to the second page
            targetPage.Annotations.Add(clonedWidget);

            // Save the file
            doc.Save("output.pdf", SDFDoc.SaveOptions.e_linearized);
            Console.WriteLine("PDF created: output.pdf");
        }

        PDFNet.Terminate();
    }
}
```

**Salida esperada:** Un archivo llamado `output.pdf` que contiene dos páginas. Ambas páginas muestran el mismo cuadro de texto editable etiquetado “Sample”. Editar uno actualiza el otro instantáneamente.

---

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito el campo en *más* de dos páginas?

Simplemente repite los pasos de clonar‑y‑añadir para cada página adicional. El objeto de datos subyacente permanece igual, por lo que todos los widgets se mantienen sincronizados.

```csharp
Widget anotherClone = textBoxField.CreateWidgetAnnotation();
thirdPage.Annotations.Add(anotherClone);
```

### ¿Cómo cambio la apariencia (fuente, borde, fondo)?

Cada `Widget` tiene los métodos `SetBorderColor`, `SetBorderWidth` y `SetBackgroundColor`. También puedes asignar una cadena de apariencia predeterminada (`DA`) para controlar la fuente y el tamaño.

```csharp
textBoxField.SetBorderColor(new ColorPt(0, 0, 1), 3); // blue border
textBoxField.SetBackgroundColor(new ColorPt(0.9, 0.9, 0.9), 3); // light gray fill
textBoxField.SetDefaultAppearance("Helvetica 12 Tf 0 g");
```

### ¿Puedo hacer que el campo sea de solo lectura después de que el usuario lo complete?

Sí. Establece la bandera `ReadOnly` en el campo después de haber recopilado los datos, o alterna su valor según tu flujo de trabajo.

```csharp
textBoxField.SetFlag(Field.Flag.e_readonly, true);
```

### ¿Qué pasa con los PDFs que ya contienen un formulario?

Si el documento ya tiene un AcroForm, `doc.GetForm()` simplemente lo devuelve. Entonces puedes añadir nuevos campos sin alterar los existentes. Solo ten cuidado de usar nombres de campo únicos.

---

## Consejos para proyectos del mundo real

- **Convención de nombres:** Prefija los nombres de campo con la página o sección (p.ej., `invoice_customer_name`) para evitar colisiones.  
- **Validación:** Usa acciones JavaScript (`field.SetAction(Field.Action.e_keystroke, "event.rc = /^[A-Za-z]+$/.test(event.change);")`) si necesitas validación del lado del cliente.  
- **Rendimiento:** Al trabajar con PDFs grandes, llama a `doc.Lock()` antes de operaciones masivas para reducir la sobrecarga de I/O.  
- **Accesibilidad:** Establece la propiedad `AlternateName` para que los lectores de pantalla puedan describir el campo.

---

## Conclusión

Acabamos de **create PDF textbox field**, mostrar cómo **duplicate PDF form field** a través de páginas, y demostrar la forma más simple de **add textbox to PDF form** usando C#. El código completo y ejecutable está arriba, y puedes ampliarlo con estilos, validación o páginas adicionales según sea necesario.

¿Listo para el siguiente paso? Prueba incrustar un menú desplegable (`ChoiceField`) o un widget de firma, o explora cómo aplanar el formulario después de la entrada de datos para fines de archivo. El PDFTron SDK (o cualquier biblioteca comparable) te brinda los bloques de construcción—tu imaginación decide la forma final.

Si encuentras algún problema, deja un comentario abajo o revisa la documentación oficial de la biblioteca; está llena de ejemplos que complementan lo que cubrimos aquí. ¡Feliz codificación, y que tus formularios siempre estén sincronizados!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Create PDF with Aspose – Add Form Field and Pages](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [Add Form Field in PDF Document using Java](/pdf/english/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)
- [Add Form Field In Pdf Document Using Java](/pdf/german/java/pdf-form-fields/add-form-field-in-pdf-document-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}