---
category: general
date: 2026-11-16
description: Aspose.PDF를 사용하여 C#에서 PDF를 PDF/X‑1A로 변환하고 사용자 정의 ICC 프로파일을 추가하세요. 신뢰할
  수 있는 인쇄 출력을 위해 단계별 가이드를 따라보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert pdf to pdf/x-1a
- add icc profile
- set custom icc profile
language: ko
lastmod: 2026-11-16
og_description: PDF를 PDF/X‑1A로 변환하고 C#에서 사용자 정의 ICC 프로파일을 삽입합니다. 이 가이드는 전체 Aspose.PDF
  코드와 모범 사례 팁을 보여줍니다.
og_image_alt: Screenshot of C# code that converts a PDF to PDF/X‑1A while attaching
  an ICC profile
og_title: PDF를 PDF/X‑1A로 변환하고 C#에서 사용자 정의 ICC 프로파일을 삽입하기
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  headline: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  type: TechArticle
- description: Convert PDF to PDF/X‑1A and add a custom ICC profile in C# using Aspose.PDF.
    Follow this step‑by‑step guide for reliable printing output.
  name: Convert PDF to PDF/X‑1A and add a custom ICC profile in C#
  steps:
  - name: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
    text: '**Set PDF/X‑1A conformance** – required for print‑ready files.'
  - name: '**Attach the custom ICC profile** – guarantees color fidelity.'
    text: '**Attach the custom ICC profile** – guarantees color fidelity.'
  - name: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
    text: '**Choose how to reference the profile** – either by file name or via an
      `OutputIntent`.'
  type: HowTo
tags:
- PDF conversion
- C#
- Aspose.PDF
title: PDF를 PDF/X‑1A로 변환하고 C#에서 사용자 정의 ICC 프로파일을 추가
url: /ko/net/printing-rendering/convert-pdf-to-pdf-x-1a-and-add-a-custom-icc-profile-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 PDF를 PDF/X‑1A로 변환하고 사용자 정의 ICC 프로파일 추가하기

PDF를 **PDF/X‑1A로 변환**해야 하는 경우, 이 가이드는 동시에 사용자 정의 ICC 프로파일을 삽입하는 방법을 보여줍니다. 인쇄소에서는 모든 색상이 ICC 프로파일로 정의되어 인쇄 시 예기치 않은 색상 차이를 방지하기 때문에 PDF/X‑1A 준수를 요구하는 경우가 많습니다. 이 문서에서는 Aspose.PDF for .NET을 사용하여 **ICC 프로파일 추가** 및 **사용자 정의 ICC 프로파일 설정**을 위한 정확한 코드를 배우고, 일반적인 함정을 피하는 팁도 제공합니다.

이 튜토리얼은 라이브러리 설치부터 출력 PDF 검증까지 모든 과정을 다룹니다. 별도의 외부 문서는 필요하지 않으며, 최종 프로그램을 복사하고 파일 경로만 조정한 뒤 실행하면 됩니다.

## 사전 요구 사항

* .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 작동합니다)
* Visual Studio 2022 (또는 C# IDE)
* Aspose.PDF for .NET 라이선스 또는 임시 평가 키
* 변환하려는 원본 PDF
* 인쇄 워크플로와 일치하는 ICC 프로파일 파일(예: `FOGRA39.icc`)

You can install Aspose.PDF via NuGet:

```bash
dotnet add package Aspose.Pdf
```

## 단계 1: Aspose.PDF for .NET 설치

NuGet 패키지는 `Aspose.Pdf` 네임스페이스와 **PDF를 PDF/X‑1A로 변환**에 사용할 `PdfFormatConversionOptions` 클래스를 제공합니다. 명령이 완료되면 패키지가 프로젝트 참조에 추가됩니다.

> **Pro tip:** 평가판 라이선스를 사용하는 경우, `Main` 시작 부분에 `License license = new License(); license.SetLicense("Aspose.Pdf.lic");` 를 호출하여 평가 워터마크가 표시되지 않도록 하세요.

## 단계 2: 원본 PDF 로드

변환하려는 PDF를 로드합니다. `Document` 클래스가 파일을 메모리로 읽어들여 변환 준비를 합니다.

```csharp
using System;
using System.IO;
using Aspose.Pdf;

class PdfX1AConverter
{
    static void Main()
    {
        // Path to the original PDF
        string sourcePdfPath = Path.Combine("YOUR_DIRECTORY", "input.pdf");

        // Load the PDF document
        Document pdfDocument = new Document(sourcePdfPath);
```

`Document` 객체는 페이지, 폰트, 리소스를 포함한 전체 PDF를 나타냅니다. 문서를 메모리에 유지하면 변환이 빠르게 수행됩니다.

## 단계 3: PDF를 PDF/X‑1A로 변환하고 ICC 프로파일을 추가하기 위한 변환 옵션 구성

이 단계에서는 세 가지 작업을 수행합니다:

1. **PDF/X‑1A 준수 설정** – 인쇄 준비 파일에 필요합니다.
2. **사용자 정의 ICC 프로파일 첨부** – 색상 정확성을 보장합니다.
3. **프로파일 참조 방식 선택** – 파일 이름으로 지정하거나 `OutputIntent`를 통해 지정합니다.

```csharp
        // -----------------------------------------------------------------
        // 3.1 Create conversion options and request PDF/X‑1A conformance
        // -----------------------------------------------------------------
        PdfFormatConversionOptions conversionOptions = new PdfFormatConversionOptions
        {
            // Enforce PDF/X‑1A:2001 compliance
            PdfXConformance = PdfXConformance.PdfX1A2001
        };

        // -----------------------------------------------------------------
        // 3.2 Path to the ICC profile you want to embed
        // -----------------------------------------------------------------
        string iccProfilePath = Path.Combine("YOUR_DIRECTORY", "FOGRA39.icc");

        // -----------------------------------------------------------------
        // 3.3 Option A – set the profile file name directly (simplest)
        // -----------------------------------------------------------------
        conversionOptions.IccProfileFileName = iccProfilePath;

        // -----------------------------------------------------------------
        // 3.4 Option B – set the profile via an OutputIntent (more control)
        // -----------------------------------------------------------------
        OutputIntent outputIntent = new OutputIntent
        {
            DestinationOutputProfile = new FileStreamSource(iccProfilePath)
        };
        conversionOptions.OutputIntents = new[] { outputIntent };

        // You can use either Option A or Option B. Both effectively
        // **set custom ICC profile** for the PDF/X‑1A output.
```

**ICC 프로파일을 설정하는 이유:** PDF/X‑1A는 색상 공간을 정의하는 단일 출력 인텐트를 요구합니다. `FOGRA39.icc`를 첨부하면 하위 장치가 색상을 정확히 해석하도록 지정합니다.

**옵션 A와 B 선택:**  
*옵션 A*는 간결하며 대부분의 상황에 적합합니다.  
*옵션 B*는 전체 `OutputIntent` 객체에 접근할 수 있어 필요에 따라 추가 메타데이터(예: `Info` 사전)를 추가할 수 있습니다.

## 단계 4: 변환 수행 및 결과 검증

Now run the conversion and write the PDF/X‑1A file to disk.

```csharp
        // -----------------------------------------------------------------
        // 4.1 Destination path for the PDF/X‑1A file
        // -----------------------------------------------------------------
        string outputPdfPath = Path.Combine("YOUR_DIRECTORY", "output_pdfx1.pdf");

        // -----------------------------------------------------------------
        // 4.2 Convert and save
        // -----------------------------------------------------------------
        pdfDocument.Convert(conversionOptions, outputPdfPath);

        Console.WriteLine($"PDF/X‑1A file saved to: {outputPdfPath}");
    }
}
```

`Convert`가 완료되면 `output_pdfx1.pdf`는 PDF/X‑1A:2001 표준을 준수하며 임베드된 ICC 프로파일을 포함합니다. **veraPDF** 또는 **Adobe Acrobat Preflight**와 같은 도구로 준수 여부를 확인할 수 있습니다.

> **Pro tip:** 변환 후 명령줄에서 `veraPDF`를 실행하세요:  
> `verapdf --format text output_pdfx1.pdf` – 위반 사항을 텍스트 형태로 나열합니다.

## 일반적인 함정 및 모범 사례

| 문제 | 발생 원인 | 예방 방법 |
|-------|----------------|-----------------|
| **ICC 파일 누락** | 경로가 잘못되어 `FileNotFoundException` 발생 | `Path.Combine`을 사용하고 할당 전에 `File.Exists`로 확인 |
| **잘못된 색상 공간** | 원본 PDF는 CMYK인데 ICC 프로파일은 RGB | 원본 색상 공간에 맞는 ICC 프로파일을 선택하거나, 임베드하기 전에 색상을 변환 |
| **PDF 버전 불일치** | PDF/X‑1A는 PDF 1.3을 요구하지만 최신 PDF에는 지원되지 않는 기능이 포함될 수 있음 | Aspose.PDF가 자동으로 다운그레이드하지만 필요하면 `PdfFormatConversionOptions`에서 `PdfVersion`을 설정 |
| **라이선스 미적용** | 출력에 평가 워터마크가 표시됨 | `Main` 시작 부분에서 라이선스 파일을 로드 |

### 예외 상황: 이미 ICC 프로파일이 포함된 PDF 변환

원본 PDF에 이미 출력 인텐트가 있는 경우, Aspose.PDF는 제공한 인텐트로 교체합니다. 이는 인쇄 제작에 일반적으로 바람직하지만, 원래 인텐트를 유지해야 한다면 기존 `Document.OutputIntents` 컬렉션을 먼저 읽고 필요에 따라 병합하십시오.

## 전체 실행 가능한 예제

아래는 새 콘솔 프로젝트에 붙여넣을 수 있는 전체 프로그램입니다. `YOUR_DIRECTORY`를 `input.pdf`와 `FOGRA39.icc`가 위치한 실제 폴더 경로로 교체하세요.



## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 소개한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [ICC 프로파일을 삽입하고 Aspose.Pdf로 PDF를 PDF/X‑1로 변환](/pdf/english/net/document-conversion/how-to-embed-icc-profile-and-convert-pdf-to-pdf-x-1-with-asp/)
- [PDF/X‑1A 변환 시 ICC 프로파일 설정 – 완전한 C# 가이드](/pdf/english/net/document-conversion/set-icc-profile-in-pdf-x-1a-conversion-complete-c-guide/)
- [ICC 프로파일을 추가하고 PDF를 PDF/X‑4로 변환 – C# 가이드](/pdf/english/net/document-conversion/add-icc-profile-and-convert-pdf-to-pdf-x-4-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}