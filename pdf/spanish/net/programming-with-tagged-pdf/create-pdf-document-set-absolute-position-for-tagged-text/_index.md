---
category: general
date: 2026-03-24
description: Crea un documento PDF y aprende cómo establecer la posición absoluta
  para texto etiquetado. Este tutorial muestra cómo añadir un elemento <span>, cómo
  agregar contenido etiquetado y posicionar texto en la página.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: es
og_description: Crea un documento PDF y ve al instante cómo establecer una posición
  absoluta, añadir un elemento <span> y posicionar texto en la página con contenido
  PDF etiquetado.
og_title: Crear documento PDF – Posicionamiento absoluto de texto etiquetado
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: Crear documento PDF – Establecer posición absoluta para texto etiquetado
url: /es/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento PDF – Establecer posición absoluta para texto etiquetado

¿Alguna vez necesitaste **crear documento pdf** que contenga texto accesible y etiquetado posicionado exactamente donde lo deseas? Tal vez estés construyendo un PDF tipo formulario donde la etiqueta debe estar en una coordenada precisa, o estés generando un certificado y el nombre tiene que alinearse perfectamente con una imagen de fondo.

En esta guía recorreremos un ejemplo completo y ejecutable que muestra **cómo agregar contenido etiquetado**, **establecer posición absoluta**, y **agregar elemento span** para que puedas **posicionar texto en la página** sin adivinar. Sin referencias externas—solo el código que puedes copiar‑pegar, más explicaciones del “por qué” detrás de cada línea.

## Requisitos previos

- .NET 6+ (o .NET Framework 4.6+) con un compilador C#  
- Aspose.Pdf for .NET (última versión al momento de escribir, 23.12) instalado vía NuGet  
- Familiaridad básica con la sintaxis de C#  

Si los tienes, comencemos.

---

## Crear documento PDF – Estableciendo la posición absoluta

Lo primero que hacemos es instanciar un `Document` vacío. Este objeto representa todo el archivo PDF y nos brinda acceso al árbol de contenido etiquetado.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Por qué esto importa:**  
`Document` es la raíz de la estructura PDF. Al crearla primero nos aseguramos de que haya un lienzo tanto para los elementos visuales (páginas, gráficos) como para la estructura lógica (etiquetas). La instrucción `using` garantiza que el archivo se libere correctamente, lo que evita fugas de manejadores de archivo en Windows.

---

## Habilitar contenido etiquetado (Cómo agregar etiquetado)

Antes de poder insertar cualquier elemento etiquetado, el documento debe estar marcado como *tagged*. Aspose.Pdf crea automáticamente un objeto `TaggedContent`, pero aún necesitas activar la bandera.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**¿Qué ocurre internamente?**  
Establecer `TaggedContent` a `true` indica a los lectores PDF que el archivo contiene un árbol de estructura lógica. Esto es crucial para los lectores de pantalla y para que el método `SetPosition` funcione correctamente en un elemento span.

---

## Obtener el elemento raíz del árbol de contenido etiquetado

El elemento raíz es el punto de entrada para todas las etiquetas estructurales (como `<Document>`, `<Section>`, `<Span>`). Piensa en él como el “cuerpo” invisible del PDF.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Por qué necesitamos la raíz:**  
Todas las etiquetas posteriores deben estar adjuntas en algún lugar del árbol; de lo contrario no aparecerán en la jerarquía de accesibilidad.

---

## Agregar un elemento Span – El bloque de construcción para texto en línea

Un *span* es el equivalente PDF de un `<span>` HTML—perfecto para fragmentos cortos de texto que deseas posicionar con precisión.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Nota de diseño:**  
Si necesitas un formato más rico (negrita, cursiva, hipervínculos), puedes envolver el span en un `<Paragraph>` o usar objetos `TextFragment` más adelante. Para posicionamiento absoluto, un span simple es el más liviano.

---

## Establecer posición absoluta – X=100, Y=200

Ahora llega la parte divertida: colocar el span en una ubicación exacta en la página. El sistema de coordenadas comienza en la esquina inferior‑izquierda (0,0) y usa puntos (1 pt ≈ 1/72 in).

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**¿Por qué posicionamiento absoluto?**  
Cuando necesitas un diseño pixel‑perfecto—piensa en certificados, facturas o formularios—el flujo relativo (como texto de izquierda a derecha) no es suficiente. `SetPosition` elude el flujo de texto normal y fija el elemento donde lo indicas.

---

## Agregar texto al Span

Con el span posicionado, ahora inyectamos la cadena real.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**Consejo:**  
Si necesitas caracteres Unicode o scripts de derecha a izquierda, simplemente pasa la cadena; Aspose.Pdf maneja la codificación automáticamente.

---

## Adjuntar el Span al elemento raíz

Finalmente, adjuntamos el span al árbol lógico del documento para que forme parte del PDF final.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**¿Qué pasa si olvidas este paso?**  
El span existiría en memoria pero nunca se serializaría en el archivo, por lo que no verías texto y el árbol de accesibilidad quedaría incompleto.

---

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que puedes colocar en una aplicación de consola. Crea un PDF de una página, agrega un span etiquetado en (100, 200) y guarda el archivo como `TaggedPositioned.pdf`.

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new PDF document
        using var pdfDocument = new Document();

        // 2️⃣ Enable tagging for accessibility
        pdfDocument.TaggedContent = true;

        // 3️⃣ Add a blank page (required for visual placement)
        var page = pdfDocument.Pages.Add();

        // 4️⃣ Get the root element of the tagged‑content tree
        var rootElement = pdfDocument.TaggedContent.RootElement;

        // 5️⃣ Create a span element that will hold the text
        var spanElement = rootElement.CreateSpanElement();

        // 6️⃣ Position the span at an absolute location on the page (X=100, Y=200)
        spanElement.SetPosition(100, 200);

        // 7️⃣ Add the desired text to the span
        spanElement.AddText("Positioned tagged text");

        // 8️⃣ Append the span to the root so it becomes part of the PDF structure
        rootElement.AppendChild(spanElement);

        // 9️⃣ Save the document
        pdfDocument.Save("TaggedPositioned.pdf");

        Console.WriteLine("PDF created successfully – check TaggedPositioned.pdf");
    }
}
```

**Salida esperada:**  
Abre `TaggedPositioned.pdf` en cualquier visor (Adobe Acrobat, Foxit, etc.). Verás la frase **“Positioned tagged text”** exactamente a 100 pt del borde izquierdo y 200 pt del borde inferior de la página. Si inspeccionas el panel *Tags*, aparecerá un elemento `<Span>` bajo la raíz del documento, confirmando que el contenido está correctamente etiquetado.

---

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito posicionar texto en una página específica distinta a la primera?

Añade la página que deseas (`var page = pdfDocument.Pages[3];`) antes de llamar a `SetPosition`. El span se adjuntará automáticamente al contexto de la página activa.

### ¿Puedo establecer la posición en pulgadas o centímetros?

`SetPosition` acepta puntos. Convierte usando las fórmulas:  
- **Pulgadas → puntos:** `points = inches * 72`  
- **Centímetros → puntos:** `points = cm * 28.3465`

### ¿Cómo cambio la fuente o el color del span?

After creating the span, you can retrieve its `TextState` and modify it:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### ¿Qué pasa si el documento ya tiene etiquetas existentes?

Aún puedes crear un nuevo span y adjuntarlo a cualquier elemento existente (`rootElement`, un `<Section>` específico, etc.). Solo asegúrate de mantener una jerarquía lógica—los lectores de pantalla esperan un árbol bien estructurado.

### ¿Esto funciona con cumplimiento PDF/A o PDF/UA?

Sí. Los PDFs etiquetados son un requisito esencial para PDF/UA. Si necesitas PDF/A, establece `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` después de crear el contenido.

---

## Consejos profesionales y trampas

- **Consejo pro:** Siempre agrega una página antes de posicionar contenido. Sin una página, `SetPosition` falla silenciosamente porque no hay dónde renderizar.
- **Cuidado con las unidades:** Mezclar píxeles de un diseño UI con puntos PDF descolocará tu texto. Verifica doblemente tu conversión.
- **Pista de rendimiento:** Si estás generando miles de PDFs, reutiliza una única instancia de `Document` y llama a `pdfDocument.Pages.Clear()` entre ejecuciones para evitar una asignación excesiva de memoria.
- **Recordatorio de accesibilidad:** El etiquetado no es solo un extra; muchas regulaciones (Section 508, EN 301 549) lo exigen. Usar `CreateSpanElement` garantiza que el texto sea detectable por tecnologías asistivas.

---

## Conclusión

Acabamos de **crear documento pdf** desde cero, **establecer posición absoluta**, **agregar elemento span**, y demostrar **cómo agregar contenido etiquetado** para que puedas **posicionar texto en la página** con precisión pixel‑perfecta. El ejemplo completo está listo para ejecutarse, y la explicación cubrió tanto el *cómo* como el *por qué*—exactamente lo que los desarrolladores (y asistentes de IA) buscan cuando necesitan una solución fiable.

Next, you might explore:

- Añadir imágenes detrás del texto posicionado para certificados con marca de agua.  
- Usar `CreateParagraphElement` para bloques de varias líneas que aún necesiten colocación absoluta.  
- Exportar a PDF/UA para cumplir auditorías de accesibilidad estrictas.  

Siéntete libre de ajustar las coordenadas, fuentes o colores—la experimentación es la forma más rápida de dominar la generación de PDFs etiquetados. Si encuentras algún problema, deja un comentario abajo; ¡feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}