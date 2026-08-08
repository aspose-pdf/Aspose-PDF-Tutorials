---
category: general
date: 2026-08-04
description: สร้าง AI Copilot เพื่อสร้างคำอธิบายภาพสำหรับไฟล์ PDF เรียนรู้วิธีกำหนดค่าตัวเลือกภาพของ
  OpenAI และสกัดคำอธิบายภาพอย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: th
lastmod: 2026-08-04
og_description: สร้าง AI Copilot เพื่อสร้างคำอธิบายรูปภาพสำหรับไฟล์ PDF บทเรียนนี้จะแสดงวิธีกำหนดค่า
  OpenAI image options, รัน Copilot, และดึงคำอธิบายรูปภาพด้วย C#
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: สร้าง AI Copilot สำหรับการอธิบายภาพใน PDF – คู่มือฉบับสมบูรณ์
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
title: สร้าง AI Copilot สำหรับการอธิบายภาพใน PDF – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง AI Copilot สำหรับการอธิบายภาพใน PDF – คู่มือเต็ม

หากคุณต้องการ **สร้าง AI Copilot** ที่อัตโนมัติเขียนคำอธิบายสำหรับภาพที่ฝังอยู่ใน PDF คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด คุณจะได้เรียนรู้การกำหนดค่า OpenAI image options, เรียกใช้ copilot, และ **ดึงคำอธิบายภาพ** โดยไม่ต้องออกจากโปรเจกต์ C# ของคุณ

การสร้างเนื้อหาข้อความสำหรับภาพใน PDF เป็นความต้องการทั่วไปสำหรับการเข้าถึง, การทำดัชนีเนื้อหา, และการรายงานอัตโนมัติ เมื่อจบบทเรียนนี้คุณจะมีคอมโพเนนต์ที่ใช้ซ้ำได้ซึ่ง **สร้างคำอธิบายภาพ** สำหรับเอกสาร PDF ใด ๆ ที่คุณชี้ไป

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมี:

* .NET 6.0 หรือใหม่กว่า  
* ใบอนุญาต Aspose.Pdf.AI (หรือทดลองใช้ฟรี)  
* คีย์ OpenAI API ที่ไคลเอนต์ Aspose สามารถใช้ได้  
* Visual Studio 2022 (หรือ IDE ใด ๆ ที่รองรับ C#)  

ไม่จำเป็นต้องติดตั้งแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.Pdf.AI`.

## Step 1: Set up the Aspose.Pdf.AI client

ขั้นตอนแรกคือการสร้างอินสแตนซ์ของ AI client ด้วยรายละเอียดการยืนยันตัวตนของคุณ ไคลเอนต์จะจัดการการสื่อสารกับบริการ OpenAI เบื้องหลัง

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

**ทำไมเรื่องนี้ถึงสำคัญ:** `AiClient` รวมการตั้งค่าระดับคำขอทั้งหมด (API key, timeout, retry policy) การสร้างครั้งเดียวและนำไปใช้ซ้ำในหลาย ๆ copilot จะลดภาระและทำให้การยืนยันตัวตนสอดคล้องกัน

## Step 2: Create an Image Description Copilot

ต่อไปคุณจะสร้าง **AI copilot** ที่อ่าน PDF และสร้างคำอธิบายสำหรับแต่ละภาพ วิธีการ `CreateImageDescriptionCopilot` รับไคลเอนต์และชุดตัวเลือกที่กำหนดวิธีการสร้างคำอธิบาย

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

**ทำไมเรื่องนี้ถึงสำคัญ:**  
* `OpenAIImageDescriptionOptions` (the **OpenAI image options**) ให้คุณปรับแต่งโมเดลภาษา การปรับ temperature หรือ model สามารถเพิ่มความเกี่ยวข้องสำหรับแผนภาพเทคนิคเทียบกับภาพธรรมชาติ  
* การระบุเส้นทางเอกสารบอก copilot ว่า PDF ใดต้องสแกน copilot จะดึงภาพ raster ทุกภาพ ส่งไปยังโมเดล และคืนค่าคำอธิบายที่มนุษย์อ่านได้

## Step 3: Retrieve the generated description asynchronously

copilot ทำงานแบบ asynchronous เนื่องจากอาจต้องอัปโหลดข้อมูลภาพหลายเมกะไบต์และรอการตอบกลับจากโมเดล ใช้ `await` เพื่อให้แน่ใจว่าการเรียกเสร็จสิ้นก่อนเข้าถึงผลลัพธ์

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

**ทำไมเรื่องนี้ถึงสำคัญ:** วิธีนี้คืนค่า `Dictionary<int, string>` ที่แมปแต่ละหน้า (หรือดัชนีภาพ) กับคำอธิบายของมัน การจัดการ `AiException` ช่วยให้คุณแสดงข้อผิดพลาดเครือข่ายหรือโควต้าที่เกิดขึ้นแทนการทำแอปพลิเคชันล่ม

## Step 4: Display or store the description

คุณสามารถเขียนคำอธิบายลงคอนโซล, ไฟล์ล็อก, หรือฝังกลับเข้า PDF เป็น alt‑text เพื่อการเข้าถึง ตัวอย่างสั้น ๆ ด้านล่างเขียนผลลัพธ์เป็นไฟล์ JSON เพื่อใช้ต่อในภายหลัง

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**ทำไมเรื่องนี้ถึงสำคัญ:** การเก็บผลลัพธ์เป็น JSON รักษาการเชื่อมโยงระหว่างแต่ละหน้าและคำอธิบาย ทำให้กระบวนการต่อไป (เช่น การทำดัชนีการค้นหา, การแสดง UI ฯลฯ) ใช้งานข้อมูลได้ง่าย

## Handling multiple images per page

หากหน้าหนึ่งมีหลายภาพ copilot จะคืนคำอธิบายที่ต่อเนื่องกันโดยคั่นด้วยการขึ้นบรรทัดใหม่ เพื่อแยกออกให้ตรวจสอบผลลัพธ์ดิบและแยกด้วย `\n\n` (บรรทัดว่างสองบรรทัด) ตัวอย่างเมธอดช่วยเหลือ:

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

จากนั้นคุณสามารถวนลูปผ่านคำอธิบายของแต่ละภาพและจัดเก็บแยกกันได้หากต้องการ

## Edge case: Large PDFs and timeout management

การประมวลผล PDF ที่ใหญ่กว่า 100 MB อาจเกินค่า timeout ของ HTTP เริ่มต้น ปรับค่า timeout ของไคลเอนต์เมื่อสร้าง `AiClient`:

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

การเพิ่ม timeout จะป้องกันการตัดการเชื่อมต่อก่อนที่บริการจะประมวลผลภาพความละเอียดสูงจำนวนมากเสร็จ

## Pro tip: Cache results to reduce cost

OpenAI คิดค่าบริการต่อ token และคำอธิบายภาพอาจซ้ำกันในหลายเวอร์ชันของรายงานเดียวกัน แคชผลลัพธ์ JSON แล้วใช้ซ้ำเมื่อ hash ของ PDF ตรงกับไฟล์ที่เคยประมวลผล การทำเช่นนี้ช่วยประหยัดค่าใช้จ่ายและเร่งความเร็วของการรันครั้งต่อไป

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

เก็บ hash ควบคู่กับไฟล์ JSON; หาก hash ตรงกันในการรันต่อไป ให้ข้ามการเรียก AI

## Full runnable example

รวมทุกอย่างเข้าด้วยกัน นี่คือตัวอย่างแอปคอนโซลที่สามารถคัดลอกไปวางในโปรเจกต์ .NET ใหม่ได้

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

**Expected output (truncated)**

```
Page 2:
A bar chart showing quarterly revenue growth, with blue bars representing Q1–Q4.
----------------------------------------
Page 5:
A high‑resolution photograph of the new manufacturing facility, showing the assembly line in operation.
...
Descriptions saved to C:\Reports\AnnualReport.descriptions.json
```

โปรแกรมอ่าน `AnnualReport.pdf`, สร้าง **AI copilot**, และเขียนไฟล์ JSON ที่แมปแต่ละหน้าไปยังคำอธิบายที่สร้างขึ้น

## Common questions

* **Does this work with encrypted PDFs?**  
  ใช่ แต่คุณต้องระบุรหัสผ่านเมื่อสร้าง copilot:  
  `imageOptions.WithPassword("mySecret")`.

* **Can I limit processing to specific pages?**  
  ใช้ `imageOptions.WithPageRange(1, 10)` เพื่อจำกัด copilot ให้ทำงานเฉพาะหน้า 1‑10.

* **What if an image contains text?**  
  โมเดลพยายามอธิบายเนื้อหาภาพ; หากต้องการดึงข้อความแบบ OCR ควรใช้ `CreateTextExtractionCopilot` แทน.

## Conclusion

คุณได้เรียนรู้วิธี **สร้าง AI Copilot** ที่ **สร้างคำอธิบายภาพ** สำหรับไฟล์ PDF, ตั้งค่า **OpenAI image options**, และ **ดึงคำอธิบายภาพ** อย่างโปรแกรมเมติกใน C# ตัวอย่างเต็มแสดงแนวทางปฏิบัติที่ดีที่สุด เช่น การจัดการ async, การจัดการข้อผิดพลาด, และการแคชผลลัพธ์

ต่อไปคุณอาจสำรวจ:

* เพิ่มคำอธิบายที่สร้างขึ้นกลับเข้า PDF เป็น alt‑text เพื่อปรับปรุงการเข้าถึง (`PdfDocument` → `PdfImage.AlternativeText`).  
* ใช้รูปแบบ copilot เดียวกันเพื่อ **สร้างรายงาน PDF ที่มีคำอธิบายภาพ** สำหรับการประมวลผลเป็นชุด.  
* ทดลองโมเดล OpenAI หรือการตั้งค่า temperature ต่าง ๆ เพื่อปรับสไตล์ของคำอธิบาย

อย่าลังเลที่จะปรับโค้ด, ทดลองกับเอกสารขนาดใหญ่, และรวมผลลัพธ์เข้ากับ pipeline การทำดัชนีของคุณ ขอให้เขียนโค้ดสนุก!

## What Should You Learn Next?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณ

- [สร้าง PDF พร้อมภาพที่มีแท็กใน Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [สร้าง PDF พร้อมภาพที่มีแท็ก](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [สร้างภาพ PDF ที่มีแท็กใน .NET](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}