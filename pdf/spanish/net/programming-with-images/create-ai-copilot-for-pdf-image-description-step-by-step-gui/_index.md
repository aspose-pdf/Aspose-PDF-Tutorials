---
category: general
date: 2026-08-04
description: Crea AI Copilot para generar descripciones de imágenes en archivos PDF.
  Aprende a configurar las opciones de imagen de OpenAI y extraer descripciones de
  imágenes de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: es
lastmod: 2026-08-04
og_description: Crea un copiloto de IA para generar descripciones de imágenes para
  archivos PDF. Este tutorial te muestra cómo configurar las opciones de imagen de
  OpenAI, ejecutar el copiloto y extraer la descripción de la imagen en C#.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: Crea un copiloto de IA para la descripción de imágenes PDF – guía completa
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create AI Copilot to generate image description for PDF files. Learn
    how to configure OpenAI image options and extract image description efficiently.
  headline: Create AI Copilot for PDF image description – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Pdf.AI
- C#
- PDF processing
title: Crea un copiloto de IA para la descripción de imágenes en PDF – guía paso a
  paso
url: /es/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear AI Copilot para descripción de imágenes en PDF – guía completa

Si necesitas **crear AI Copilot** que escriba automáticamente descripciones para imágenes incrustadas en un PDF, esta guía te muestra exactamente cómo hacerlo. Aprenderás a configurar las opciones de imagen de OpenAI, ejecutar el copilot y **extraer la descripción de la imagen** sin salir de tu proyecto C#.

Generar contenido textual para imágenes de PDF es un requisito común para accesibilidad, indexación de contenido e informes automatizados. Al final de este tutorial tendrás un componente reutilizable que **genera descripciones de imágenes** para cualquier documento PDF que le indiques.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior instalado  
* Una licencia de Aspose.Pdf.AI (o una prueba gratuita)  
* Una clave API de OpenAI que el cliente Aspose pueda usar  
* Visual Studio 2022 (o cualquier IDE que soporte C#)  

No se requieren paquetes NuGet adicionales más allá de `Aspose.Pdf.AI`.

## Paso 1: Configurar el cliente Aspose.Pdf.AI

El primer paso es instanciar el cliente de IA con tus datos de autenticación. El cliente maneja la comunicación con el servicio OpenAI tras bambalinas.

```csharp
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

// Replace with your actual credentials
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    // Optional: set a custom endpoint if you use Azure OpenAI
    // Endpoint = "https://my-openai-instance.openai.azure.com/"
});
```

**Por qué es importante:** El `AiClient` encapsula todas las configuraciones a nivel de solicitud (clave API, tiempo de espera, política de reintentos). Crearlo una vez y reutilizarlo en múltiples instancias del copilot reduce la sobrecarga y garantiza una autenticación consistente.

## Paso 2: Crear un Copilot de Descripción de Imagen

Ahora creas el **AI copilot** que leerá el PDF y producirá una descripción para cada imagen. El método de fábrica `CreateImageDescriptionCopilot` acepta el cliente y un conjunto de opciones que definen cómo se genera la descripción.

```csharp
// Configure OpenAI image options – this is where you control model, temperature, etc.
var imageOptions = OpenAIImageDescriptionOptions.Create()
    .WithModel("gpt-4o-mini")           // Choose a model that balances cost and quality
    .WithTemperature(0.7)               // Controls creativity; 0 = deterministic
    .WithMaxTokens(150);                // Maximum length of each description

// Point the copilot at the PDF you want to process
var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
    client,
    imageOptions.WithDocument(@"C:\Reports\AnnualReport.pdf"));
```

**Por qué es importante:**  
* `OpenAIImageDescriptionOptions` (las **opciones de imagen de OpenAI**) te permiten afinar el modelo de lenguaje. Ajustar la temperatura o el modelo puede mejorar la relevancia para diagramas técnicos versus fotos naturales.  
* Especificar la ruta del documento indica al copilot qué PDF escanear. El copilot extrae cada imagen raster, la envía al modelo y devuelve una descripción legible por humanos.

## Paso 3: Recuperar la descripción generada de forma asíncrona

El copilot funciona de manera asíncrona porque puede necesitar subir varios megabytes de datos de imagen y esperar la respuesta del modelo. Usa `await` para asegurarte de que la llamada se complete antes de acceder al resultado.

```csharp
try
{
    // Get a dictionary where the key is the page number and the value is the description
    var descriptionMap = await imgCopilot.GetDescriptionAsync();

    // Example: iterate over each image description
    foreach (var entry in descriptionMap)
    {
        Console.WriteLine($"Page {entry.Key}: {entry.Value}");
    }
}
catch (AiException ex)
{
    Console.Error.WriteLine($"AI service error: {ex.Message}");
}
```

**Por qué es importante:** El método devuelve un `Dictionary<int, string>` que asigna cada página (o índice de imagen) a su descripción. Manejar `AiException` te permite mostrar errores de red o de cuota en lugar de que la aplicación se bloquee.

## Paso 4: Mostrar o almacenar la descripción

Puedes escribir las descripciones en la consola, en un archivo de registro o incrustarlas de nuevo en el PDF como texto alternativo para accesibilidad. A continuación, un ejemplo rápido que escribe la salida en un archivo JSON para su consumo posterior.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Por qué es importante:** Almacenar la salida como JSON preserva la asociación entre cada página y su descripción, facilitando que procesos posteriores (indexación de búsqueda, renderizado UI, etc.) consuman los datos.

## Manejo de múltiples imágenes por página

Si una página contiene varias imágenes, el copilot devuelve una descripción concatenada separada por saltos de línea. Para dividirlas, inspecciona el resultado bruto y separa por `\n\n` (doble salto de línea). Aquí tienes un método auxiliar:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

Luego puedes iterar sobre cada descripción de imagen individual y almacenarlas por separado si lo necesitas.

## Caso límite: PDFs grandes y gestión de tiempo de espera

Procesar un PDF de más de 100 MB puede superar los tiempos de espera HTTP predeterminados. Ajusta la configuración de tiempo de espera del cliente cuando crees el `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

Incrementar el tiempo de espera evita terminaciones prematuras mientras el servicio procesa muchas imágenes de alta resolución.

## Consejo profesional: Cachear resultados para reducir costos

OpenAI cobra por token, y la descripción de imágenes puede ser repetitiva entre versiones del mismo informe. Cachea la salida JSON y reutilízala cuando el hash del PDF coincida con un archivo procesado previamente. Esta práctica ahorra dinero y acelera ejecuciones posteriores.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

Guarda el hash junto al archivo JSON; si el hash coincide en una ejecución posterior, omite la llamada a IA.

## Ejemplo completo ejecutable

Juntando todo, aquí tienes una aplicación de consola autocontenida que puedes pegar en un nuevo proyecto .NET.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Threading.Tasks;
using Aspose.Pdf.AI;
using Aspose.Pdf.AI.Models;

class Program
{
    static async Task Main()
    {
        // 1️⃣ Initialize AI client
        var client = new AiClient(new AiClientOptions
        {
            ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
            Timeout = TimeSpan.FromMinutes(5)
        });

        // 2️⃣ Configure OpenAI image options and create copilot
        var imageOptions = OpenAIImageDescriptionOptions.Create()
            .WithModel("gpt-4o-mini")
            .WithTemperature(0.7)
            .WithMaxTokens(150);

        string pdfPath = @"C:\Reports\AnnualReport.pdf";

        var imgCopilot = AICopilotFactory.CreateImageDescriptionCopilot(
            client,
            imageOptions.WithDocument(pdfPath));

        // 3️⃣ Retrieve descriptions
        Dictionary<int, string> descriptionMap;
        try
        {
            descriptionMap = await imgCopilot.GetDescriptionAsync();
        }
        catch (AiException ex)
        {
            Console.Error.WriteLine($"Error from AI service: {ex.Message}");
            return;
        }

        // 4️⃣ Output results
        foreach (var entry in descriptionMap)
        {
            Console.WriteLine($"Page {entry.Key}:");
            Console.WriteLine(entry.Value);
            Console.WriteLine(new string('-', 40));
        }

        // 5️⃣ Save to JSON for later use
        string json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = Path.ChangeExtension(pdfPath, ".descriptions.json");
        await File.WriteAllTextAsync(jsonPath, json);
        Console.WriteLine($"Descriptions saved to {jsonPath}");
    }
}
```

**Salida esperada (truncada)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

El programa lee `AnnualReport.pdf`, crea un **AI copilot** y escribe un archivo JSON que asigna cada página a su descripción generada.

## Preguntas frecuentes

* **¿Esto funciona con PDFs encriptados?**  
  Sí, pero debes proporcionar la contraseña al crear el copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **¿Puedo limitar el procesamiento a páginas específicas?**  
  Usa `imageOptions.WithPageRange(1, 10)` para restringir el copilot a las páginas 1‑10.

* **¿Qué pasa si una imagen contiene texto?**  
  El modelo intenta describir el contenido visual; para extracción de texto tipo OCR deberías usar `CreateTextExtractionCopilot` en su lugar.

## Conclusión

Ahora sabes cómo **crear AI Copilot** que **genera descripciones de imágenes** para archivos PDF, configurar **opciones de imagen de OpenAI** y **extraer descripciones de imágenes** programáticamente en C#. El ejemplo completo demuestra buenas prácticas como manejo async, gestión de errores y cacheado de resultados.

A continuación, podrías explorar:

* Añadir las descripciones generadas de nuevo al PDF como texto alternativo para mejorar la accesibilidad (`PdfDocument` → `PdfImage.AlternativeText`).  
* Usar el mismo patrón de copilot para **generar informes PDF con descripción de imágenes** en procesamiento por lotes.  
* Experimentar con diferentes modelos de OpenAI o configuraciones de temperatura para afinar el estilo de la descripción.

¡Siéntete libre de adaptar el código, experimentar con documentos más grandes e integrar la salida en tu canal de indexación. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear PDF con imagen etiquetada en Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Crear PDF con imagen etiquetada](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Crear imagen PDF etiquetada en .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}