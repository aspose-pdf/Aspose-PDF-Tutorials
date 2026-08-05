---
category: general
date: 2026-08-04
description: PDF 파일의 이미지 설명을 생성하는 AI 코파일럿을 만들세요. OpenAI 이미지 옵션을 설정하고 이미지 설명을 효율적으로
  추출하는 방법을 배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create AI copilot
- generate image description
- image description PDF
- OpenAI image options
- extract image description
language: ko
lastmod: 2026-08-04
og_description: PDF 파일에 대한 이미지 설명을 생성하는 AI 코파일럿을 만듭니다. 이 튜토리얼에서는 OpenAI 이미지 옵션을 구성하고,
  코파일럿을 실행하며, C#에서 이미지 설명을 추출하는 방법을 보여줍니다.
og_image_alt: Screenshot of C# code that creates an AI copilot for PDF image description
og_title: PDF 이미지 설명을 위한 AI 코파일럿 만들기 – 완전 가이드
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
title: PDF 이미지 설명을 위한 AI 코파일럿 만들기 – 단계별 가이드
url: /ko/net/programming-with-images/create-ai-copilot-for-pdf-image-description-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF 이미지 설명을 위한 AI Copilot 만들기 – 완전 가이드

PDF에 포함된 이미지를 자동으로 설명하는 **AI Copilot**을 만들어야 한다면, 이 가이드는 정확한 구현 방법을 보여줍니다. OpenAI 이미지 옵션을 설정하고, Copilot을 실행하며, **이미지 설명을 추출**하는 과정을 C# 프로젝트 안에서 그대로 진행할 수 있습니다.

PDF 이미지에 대한 텍스트 콘텐츠를 생성하는 것은 접근성, 콘텐츠 색인화, 자동 보고서 작성 등에 흔히 요구되는 작업입니다. 이 튜토리얼을 마치면 원하는 PDF 문서에 대해 **이미지 설명을 생성**하는 재사용 가능한 컴포넌트를 얻게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 이상 설치  
* Aspose.Pdf.AI 라이선스(또는 무료 체험)  
* Aspose 클라이언트가 사용할 수 있는 OpenAI API 키  
* Visual Studio 2022(또는 C#을 지원하는 IDE)  

`Aspose.Pdf.AI` 외에 추가 NuGet 패키지는 필요하지 않습니다.

## Step 1: Set up the Aspose.Pdf.AI client

첫 번째 단계는 인증 정보를 사용해 AI 클라이언트를 인스턴스화하는 것입니다. 클라이언트는 백그라운드에서 OpenAI 서비스와의 통신을 담당합니다.

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

**Why this matters:** `AiClient`는 모든 요청 수준 설정(API 키, 타임아웃, 재시도 정책)을 캡슐화합니다. 한 번 생성해 여러 Copilot 인스턴스에서 재사용하면 오버헤드가 감소하고 인증이 일관됩니다.

## Step 2: Create an Image Description Copilot

이제 **AI copilot**을 만들어 PDF를 읽고 각 이미지에 대한 설명을 생성합니다. `CreateImageDescriptionCopilot` 팩터리 메서드는 클라이언트와 설명 생성 방식을 정의하는 옵션 집합을 받습니다.

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

**Why this matters:**  
* `OpenAIImageDescriptionOptions`(**OpenAI 이미지 옵션**)을 통해 언어 모델을 미세 조정할 수 있습니다. 온도값이나 모델을 조정하면 기술 도면과 자연 사진에 대한 관련성을 높일 수 있습니다.  
* 문서 경로를 지정하면 Copilot이 어떤 PDF를 스캔할지 알 수 있습니다. Copilot은 모든 래스터 이미지를 추출해 모델에 전달하고, 사람이 읽을 수 있는 설명을 반환합니다.

## Step 3: Retrieve the generated description asynchronously

Copilot은 이미지 데이터를 몇 메가바이트씩 업로드하고 모델 응답을 기다릴 수 있기 때문에 비동기로 동작합니다. `await`를 사용해 결과에 접근하기 전에 호출이 완료되도록 합니다.

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

**Why this matters:** 메서드는 각 페이지(또는 이미지 인덱스)와 설명을 매핑한 `Dictionary<int, string>`을 반환합니다. `AiException`을 처리하면 네트워크 오류나 할당량 초과 오류를 애플리케이션이 중단되지 않게 표시할 수 있습니다.

## Step 4: Display or store the description

설명을 콘솔, 로그 파일에 기록하거나 접근성을 위해 PDF에 alt‑text로 삽입할 수 있습니다. 아래 예시는 출력을 JSON 파일에 저장해 나중에 활용하는 방법을 보여줍니다.

```csharp
using System.Text.Json;

// Serialize the map to JSON
var json = JsonSerializer.Serialize(descriptionMap, new JsonSerializerOptions { WriteIndented = true });
File.WriteAllText(@"C:\Reports\ImageDescriptions.json", json);

Console.WriteLine("Image descriptions saved to ImageDescriptions.json");
```

**Why this matters:** JSON 형태로 저장하면 각 페이지와 설명 간의 연관성을 보존할 수 있어, 검색 색인, UI 렌더링 등 후속 프로세스가 데이터를 쉽게 소비할 수 있습니다.

## Handling multiple images per page

한 페이지에 여러 이미지가 포함된 경우, Copilot은 줄바꿈으로 구분된 연결된 설명을 반환합니다. 이를 분리하려면 원시 결과를 검사하고 `\n\n`(두 개의 개행)으로 split하면 됩니다. 아래는 헬퍼 메서드 예시입니다.

```csharp
static IEnumerable<string> SplitDescriptions(string combined)
{
    return combined.Split(new[] { "\n\n" }, StringSplitOptions.RemoveEmptyEntries);
}
```

필요에 따라 각 이미지 설명을 개별적으로 반복 처리하고 별도로 저장할 수 있습니다.

## Edge case: Large PDFs and timeout management

용량이 100 MB를 초과하는 PDF를 처리하면 기본 HTTP 타임아웃을 초과할 수 있습니다. `AiClient`를 생성할 때 클라이언트의 타임아웃 설정을 조정하세요.

```csharp
var client = new AiClient(new AiClientOptions
{
    ApiKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY"),
    Timeout = TimeSpan.FromMinutes(5)   // Increase timeout for heavy workloads
});
```

타임아웃을 늘리면 서비스가 고해상도 이미지를 많이 처리하는 동안 조기 종료되는 것을 방지할 수 있습니다.

## Pro tip: Cache results to reduce cost

OpenAI는 토큰당 요금을 부과하며, 동일 보고서의 여러 버전에서 이미지 설명이 반복될 수 있습니다. JSON 출력 결과를 캐시하고 PDF 해시가 이전에 처리한 파일과 일치하면 재사용하세요. 이 방법은 비용을 절감하고 후속 실행 속도를 높입니다.

```csharp
static string ComputeFileHash(string path)
{
    using var sha256 = System.Security.Cryptography.SHA256.Create();
    using var stream = File.OpenRead(path);
    var hash = sha256.ComputeHash(stream);
    return Convert.ToHexString(hash);
}
```

해시 값을 JSON 파일과 함께 저장하고, 이후 실행 시 해시가 일치하면 AI 호출을 건너뛰면 됩니다.

## Full runnable example

모든 내용을 하나로 합치면, 새 .NET 프로젝트에 붙여넣을 수 있는 독립 실행형 콘솔 애플리케이션이 됩니다.

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

프로그램은 `AnnualReport.pdf`를 읽고 **AI copilot**을 생성한 뒤, 각 페이지와 생성된 설명을 매핑한 JSON 파일을 작성합니다.

## Common questions

* **암호화된 PDF에서도 작동하나요?**  
  네, Copilot을 만들 때 비밀번호를 제공하면 됩니다:  
  `imageOptions.WithPassword("mySecret")`.

* **특정 페이지만 처리하도록 제한할 수 있나요?**  
  `imageOptions.WithPageRange(1, 10)`을 사용해 Copilot이 1‑10 페이지만 처리하도록 제한할 수 있습니다.

* **이미지에 텍스트가 포함된 경우는 어떻게 하나요?**  
  모델은 시각적 내용을 설명하려고 시도합니다; OCR 스타일 텍스트 추출이 필요하면 `CreateTextExtractionCopilot`을 사용하세요.

## Conclusion

이제 **AI Copilot**을 만들어 PDF 파일에 대한 **이미지 설명을 생성**하고, **OpenAI 이미지 옵션**을 구성하며, C#에서 **이미지 설명을 추출**하는 방법을 알게 되었습니다. 전체 예제는 비동기 처리, 오류 관리, 결과 캐싱과 같은 모범 사례를 보여줍니다.

다음 단계로 고려해볼 내용:

* 생성된 설명을 PDF에 alt‑text로 삽입해 접근성을 향상시키기 (`PdfDocument` → `PdfImage.AlternativeText`).  
* 동일한 Copilot 패턴을 사용해 배치 처리용 **이미지 설명 PDF** 보고서를 생성하기.  
* 다양한 OpenAI 모델이나 온도 설정을 실험해 설명 스타일을 미세 조정하기.

코드를 자유롭게 수정하고, 더 큰 문서로 실험해 보며, 출력 결과를 색인 파이프라인에 통합해 보세요. 즐거운 코딩 되세요!


## What Should You Learn Next?


다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 설명과 완전한 코드 예제를 포함하고 있어 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색하는 데 도움이 됩니다.

- [Create Pdf With Tagged Image In Java](/pdf/hindi/java/pdf-structure-elements/create-pdf-with-tagged-image-in-java/)
- [Create Pdf With Tagged Image](/pdf/hindi/net/programming-with-tagged-pdf/create-pdf-with-tagged-image/)
- [Create Tagged Pdf Image Dotnet](/pdf/hindi/net/images-graphics/create-tagged-pdf-image-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}