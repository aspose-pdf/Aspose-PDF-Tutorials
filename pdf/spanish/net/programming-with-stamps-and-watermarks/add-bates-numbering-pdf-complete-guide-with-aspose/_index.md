---
category: general
date: 2026-06-08
description: Agregar numeración Bates a PDF usando Aspose.Pdf en C#. Aprende cómo
  agregar Bates, agregar números de página al PDF, agregar números secuenciales al
  PDF y ver un ejemplo de numeración Bates en PDF.
draft: false
keywords:
- add bates numbering pdf
- how to add bates
- add page numbers pdf
- add sequential numbers pdf
- bates number pdf example
language: es
og_description: Agregar numeración Bates a PDF en C#. Este tutorial muestra cómo agregar
  Bates, agregar números de página a PDF y agregar números secuenciales a PDF con
  un ejemplo completo de numeración Bates en PDF.
og_title: Agregar numeración Bates a PDF – Guía completa con Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  headline: Add Bates Numbering PDF – Complete Guide with Aspose
  type: TechArticle
- description: Add bates numbering pdf using Aspose.Pdf in C#. Learn how to add bates,
    add page numbers pdf, add sequential numbers pdf, and see a bates number pdf example.
  name: Add Bates Numbering PDF – Complete Guide with Aspose
  steps:
  - name: Install the Aspose.Pdf NuGet Package
    text: 'First, add the library to your project. Open the Package Manager Console
      and run:'
  - name: Open the Source PDF Document
    text: Now we load the PDF we want to stamp. The `using` statement ensures the
      file is closed properly even if an exception occurs.
  - name: Create a Bates Numbering Facade
    text: 'The *facade* pattern hides the complexity of the underlying PDF structure.
      Here’s how we instantiate it:'
  - name: Configure the Starting Number and Prefix
    text: Bates numbers often include a case‑specific prefix. You can also control
      the number of digits, the separator, and the placement on the page.
  - name: Apply the Bates Numbering to the Document
    text: 'With the facade configured, we now stamp every page:'
  - name: Save the Modified PDF
    text: 'Finally, write the output to disk:'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF processing
title: Añadir numeración Bates a PDF – Guía completa con Aspose
url: /es/net/programming-with-stamps-and-watermarks/add-bates-numbering-pdf-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar Numeración Bates PDF – Guía Completa de Programación

¿Alguna vez necesitaste **add bates numbering pdf** pero no sabías por dónde empezar? Si alguna vez te has preguntado *cómo agregar bates* a un documento legal, estás en el lugar correcto. En este tutorial recorreremos un ejemplo práctico, de extremo a extremo, que no solo agrega números Bates sino que también te muestra cómo **add page numbers pdf**, **add sequential numbers pdf**, y además proporciona un **bates number pdf example** listo para ejecutar.

Usaremos la biblioteca Aspose.Pdf para .NET, porque abstrae los detalles internos de bajo nivel del PDF mientras te brinda control granular. Al final de esta guía tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto C#, y comprenderás por qué cada línea es importante.

## Qué Necesitarás

- **.NET 6.0** o posterior (el código también funciona en .NET Framework 4.6+).  
- Una **licencia** para Aspose.Pdf o una clave de evaluación temporal gratuita.  
- Un PDF de ejemplo llamado `input.pdf` colocado en una carpeta a la que puedas referenciar.  
- Visual Studio, Rider, o cualquier editor de C# que prefieras.

Eso es todo—sin herramientas extra, sin acrobacias de línea de comandos. ¿Listo? Vamos a sumergirnos.

## Agregar Numeración Bates PDF – Implementación Paso a Paso

A continuación dividimos el proceso en seis pasos lógicos. Cada paso incluye un fragmento de código breve, una explicación del *por qué* lo hacemos y un consejo que puede resultarte útil.

### Paso 1: Instalar el Paquete NuGet Aspose.Pdf

Primero, agrega la biblioteca a tu proyecto. Abre la Consola del Administrador de Paquetes y ejecuta:

```powershell
Install-Package Aspose.Pdf
```

> **Consejo profesional:** Si trabajas con .NET Core, también puedes usar `dotnet add package Aspose.Pdf`.

Instalar el paquete te da acceso a la clase `Aspose.Pdf.Facades.BatesNumbering`, que es la pieza clave para **add bates numbering pdf**.

### Paso 2: Abrir el Documento PDF de Origen

Ahora cargamos el PDF que queremos estampar. La instrucción `using` garantiza que el archivo se cierre correctamente incluso si ocurre una excepción.

```csharp
using (var doc = new Aspose.Pdf.Document(@"C:\MyPdfs\input.pdf"))
{
    // All further steps happen inside this block.
}
```

¿Por qué usar `Aspose.Pdf.Document`? Representa todo el PDF en memoria, permitiéndonos manipular páginas, fuentes y metadatos sin tocar el archivo original en disco.

### Paso 3: Crear una Fachada de Numeración Bates

El patrón *fachada* oculta la complejidad de la estructura subyacente del PDF. Así es como lo instanciamos:

```csharp
var bates = new Aspose.Pdf.Facades.BatesNumbering();
```

Este objeto se configurará más adelante con un prefijo, número inicial y opciones de formato. Piensa en él como el “motor” que **add page numbers pdf** de forma compatible con Bates.

### Paso 4: Configurar el Número Inicial y el Prefijo

Los números Bates a menudo incluyen un prefijo específico del caso. También puedes controlar la cantidad de dígitos, el separador y la ubicación en la página.

```csharp
bates.StartNumber = 1000;          // First number in the sequence
bates.Prefix = "CASE-";            // Prefix that appears before each number
bates.NumberOfDigits = 5;          // Pads numbers with leading zeros (e.g., 01000)
bates.Separator = "-";             // Optional separator between prefix and number
bates.Location = new Aspose.Pdf.Rectangle(0, 0, 200, 20); // Bottom‑left corner
bates.FontSize = 12;
bates.FontColor = System.Drawing.Color.Blue;
```

**¿Por qué estos ajustes?**  
- `StartNumber` te permite continuar una serie previa.  
- `NumberOfDigits` garantiza una longitud uniforme, lo cual es crucial para la indexación legal.  
- `Location` define dónde aparecerá el **add sequential numbers pdf**; puedes moverlo a la esquina superior derecha si lo prefieres.

### Paso 5: Aplicar la Numeración Bates al Documento

Con la fachada configurada, ahora estampamos cada página:

```csharp
bates.AddBatesNumbering(doc);
```

Internamente, Aspose recorre cada página, dibuja el texto en la ubicación especificada y respeta cualquier contenido existente. Esta única línea es la que realmente **add bates numbering pdf** a tu archivo.

### Paso 6: Guardar el PDF Modificado

Finalmente, escribe el resultado en disco:

```csharp
doc.Save(@"C:\MyPdfs\output.pdf");
```

Ahora tienes un PDF donde cada página lleva un identificador Bates único, listo para descubrimiento o presentación en tribunal.

#### Ejemplo Completo Funcional (Bates Number PDF Example)

Juntándolo todo, aquí tienes un programa completo, autocontenido, que puedes compilar y ejecutar:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Facades;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source PDF
        using (var doc = new Document(@"C:\MyPdfs\input.pdf"))
        {
            // 2️⃣ Create the Bates numbering facade
            var bates = new BatesNumbering();

            // 3️⃣ Configure prefix, start number, and formatting
            bates.StartNumber = 1000;
            bates.Prefix = "CASE-";
            bates.NumberOfDigits = 5;
            bates.Separator = "-";
            bates.Location = new Rectangle(0, 0, 200, 20); // Bottom‑left
            bates.FontSize = 12;
            bates.FontColor = Color.Blue;

            // 4️⃣ Apply the numbering to every page
            bates.AddBatesNumbering(doc);

            // 5️⃣ Save the result
            doc.Save(@"C:\MyPdfs\output.pdf");
        }

        Console.WriteLine("Bates numbering added successfully!");
    }
}
```

> **Salida esperada:** Abre `output.pdf` y verás “CASE‑01000”, “CASE‑01001”, … en la esquina inferior izquierda de cada página.

![Captura de pantalla de una página PDF con números Bates en la esquina inferior izquierda – ejemplo de agregar numeración bates pdf](https://example.com/bates-numbering-screenshot.png "ejemplo de agregar numeración bates pdf")

*(Texto alternativo de la imagen: *ejemplo de agregar numeración bates pdf* – muestra los números Bates aplicados a un PDF de muestra.)*

## Cómo Agregar Bates – Entendiendo la Fachada

Quizás te preguntes **how to add bates** sin la fachada de Aspose. La alternativa es dibujar texto manualmente en cada página usando operadores PDF de bajo nivel, pero ese enfoque es propenso a errores y requiere un conocimiento profundo de la especificación PDF. La fachada abstrae esos detalles, permitiéndote enfocarte en *qué* quieres (un prefijo, un número inicial) en lugar de *cómo* renderizarlo.

Si alguna vez necesitas **add page numbers pdf** en un estilo no Bates (por ejemplo, “Página 3 de 12”), puedes reutilizar la misma clase `BatesNumbering`—simplemente cambia el `Prefix` a una cadena vacía y ajusta el `Location`. El motor subyacente es el mismo, lo que significa que obtienes un renderizado consistente en ambos casos de uso.

## Agregar Números de Página PDF – Personalizando Posición y Estilo

Los equipos legales a menudo solicitan el número de página en el encabezado, mientras que el personal de soporte de litigios lo prefiere en el pie de página. Aquí tienes un ajuste rápido:

```csharp
bates.Location = new Rectangle(0, doc.Pages[1].PageInfo.Height - 20, 200, 20); // Top‑right
bates.Prefix = "";               // No prefix for plain page numbers
bates.StartNumber = 1;           // Start from 1
bates.NumberOfDigits = 0;        // No padding
bates.FontColor = Color.Black;
```

La misma llamada `AddBatesNumbering` ahora **add page numbers pdf** en la parte superior de cada página. Como la fachada opera sobre el objeto documento, puedes alternar entre numeración Bates y numeración simple con unos pocos cambios de propiedad—sin necesidad de reescribir el bucle.

## Agregar Números Secuenciales PDF – Formato Avanzado

Supongamos que necesitas un formato como `2023-CASE-00123`. Puedes combinar un prefijo de fecha con la configuración existente:

```csharp
bates.Prefix = $"{DateTime.Now:yyyy}-CASE-";
bates.NumberOfDigits = 5;
bates.Separator = "-";
```

Ahora cada página mostrará `2023-CASE-00123`, `2023-CASE-00124`, etc. Esto demuestra lo fácil que es **add sequential numbers pdf** que cumplan convenciones de nombres complejas.

## Casos Límite y Errores Comunes

| Situación | Qué vigilar | Solución sugerida |
|-----------|--------------|-------------------|
| **PDF muy grandes ( > 500 MB )** | El consumo de memoria puede dispararse porque todo el documento se carga en RAM. | Usa `Document` con configuraciones de `MemoryManagement` o procesa el archivo en fragmentos con `PdfFileEditor`. |
| **Números de página existentes** |  |  |

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Add and Customize Page Numbers in PDFs Using Aspose.PDF for .NET | Document Manipulation Guide](/pdf/english/net/document-manipulation/add-customize-page-numbers-aspose-pdf-dot-net/)
- [How to Add Page Number Stamps in PDFs Using Aspose.PDF for .NET | Watermarks & Backgrounds](/pdf/english/net/watermarks-backgrounds/add-page-number-stamp-using-aspose-pdf-dotnet/)
- [Aspose.PDF .NET: Add Page Numbers to PDFs Using FloatingBox](/pdf/english/net/text-operations/aspose-pdf-net-floatingbox-page-numbering/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}