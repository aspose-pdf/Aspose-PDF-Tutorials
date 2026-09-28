---
category: general
date: 2026-09-27
description: PDF belgesi oluşturun ve etkileşimli bir PDF formu oluştururken PDF'ye
  sayfalar ekleyin. PDF'ye TextBox eklemeyi ve Aspose.Pdf ile AcroForm PDF oluşturmayı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf document
- add pages to pdf
- create interactive pdf form
- how to add textbox to pdf
- how to create acroform pdf
language: tr
lastmod: 2026-09-27
og_description: PDF belgesi oluşturun ve etkileşimli bir PDF formu oluştururken PDF'ye
  sayfalar ekleyin. Aspose.Pdf kullanarak PDF'ye TextBox eklemeyi ve AcroForm PDF
  oluşturmayı öğrenmek için bu kılavuzu izleyin.
og_image_alt: Screenshot showing a PDF document with a textbox field on two pages
og_title: Etkileşimli form alanlarıyla PDF belgesi oluşturma – adım adım C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  headline: How to create PDF document with interactive form fields in C#
  type: TechArticle
- description: create PDF document and add pages to PDF while building an interactive
    PDF form. Learn how to add TextBox to PDF and create AcroForm PDF with Aspose.Pdf.
  name: How to create PDF document with interactive form fields in C#
  steps:
  - name: '**Create PDF document** and add the needed pages.'
    text: '**Create PDF document** and add the needed pages.'
  - name: '**Initialize AcroForm** and define a `TextBoxField`.'
    text: '**Initialize AcroForm** and define a `TextBoxField`.'
  - name: '**Add widget annotations** on each page to place the textbox.'
    text: '**Add widget annotations** on each page to place the textbox.'
  - name: '**Save** the document and test the interactive behavior.'
    text: '**Save** the document and test the interactive behavior.'
  type: HowTo
tags:
- Aspose.Pdf
- C#
- PDF forms
title: C#'ta etkileşimli form alanlarıyla PDF belgesi nasıl oluşturulur
url: /tr/net/programming-with-forms/how-to-create-pdf-document-with-interactive-form-fields-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile etkileşimli form alanlarına sahip PDF belgesi nasıl oluşturulur

Birden fazla sayfa ve etkileşimli bir form içeren **PDF belgesi oluşturmanız** gerektiğinde, bu kılavuz tam olarak nasıl yapılacağını gösterir. PDF'e sayfa ekleme, bir AcroForm oluşturma ve her sayfada bir TextBox alanı yerleştirme adımlarını Aspose.Pdf for .NET kullanarak anlatacağız.

Sonuçta, kullanıcıların her iki sayfada da yorum yazabileceği tek bir PDF dosyanız olacak. Harici araçlar yok, sadece birkaç satır C# ve güçlü Aspose.Pdf kütüphanesi.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır)
* Geçerli bir Aspose.Pdf for .NET lisansı veya geçici bir değerlendirme anahtarı
* Visual Studio 2022 (veya C# destekleyen herhangi bir IDE)
* C# sözdizimi ve nesne‑yönelimli kavramlara temel aşinalık

> **İpucu:** Ücretsiz deneme sürümünü kullanıyorsanız, değerlendirme filigranlarından kaçınmak için `License` nesnesini programınızın başında ayarlamayı unutmayın.

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol uygulaması oluşturun ve Aspose.Pdf NuGet paketini ekleyin:

```bash
dotnet new console -n PdfFormDemo
cd PdfFormDemo
dotnet add package Aspose.Pdf
```

`Program.cs` içinde gerekli ad alanlarını içe aktarın:

```csharp
using System;
using Aspose.Pdf;
using Aspose.Pdf.Annotations;
using Aspose.Pdf.Forms;
```

Bu ad alanları, öğreticide ihtiyaç duyulan temel PDF nesneleri, açıklama türleri ve form alanı sınıflarına erişim sağlar.

## Adım 2: PDF belgesi oluşturun ve PDF'e sayfalar ekleyin

İlk işlevsel adım **PDF belgesi oluşturmak** ve ardından **PDF'e sayfalar eklemektir**. Her sayfa aynı TextBox alanını barındıracak.

```csharp
// Initialize a new PDF document
var pdfDocument = new Document();

// Add two blank pages
var firstPage = pdfDocument.Pages.Add();
var secondPage = pdfDocument.Pages.Add();
```

*Neden önemli:*  
`Document` tüm PDF dosyasını temsil eder. Sayfaları açıkça eklemek, form widget'larını yerleştirebileceğiniz bir tuval oluşturur. İhtiyacınız kadar sayfa ekleyebilirsiniz; örnek açıklık sağlamak için iki sayfa kullanır.

## Adım 3: Etkileşimli bir PDF formu (AcroForm) oluşturun

Bir **etkileşimli PDF formu**, `Document` içinde yer alan bir AcroForm nesnesi üzerine inşa edilir. Tek bir `TextBoxField` oluşturacağız ve bu alanı iki sayfada paylaşacağız.

```csharp
// Initialize the AcroForm if it doesn't exist
if (!pdfDocument.AcroForm.IsPresent)
{
    pdfDocument.AcroForm = new AcroForm(pdfDocument);
}

// Create a TextBox field named "Comments"
var textBoxField = new TextBoxField(pdfDocument.AcroForm)
{
    Name = "Comments",
    // Optional: set default appearance (font size, color)
    DefaultAppearance = new DefaultAppearance("Helvetica", 12, Color.Black)
};
```

*Neden önemli:*  
AcroForm konteyneri tüm etkileşimli öğeleri tutar. Tek bir `TextBoxField` oluşturarak, aynı mantıksal alanı birden fazla sayfada yeniden kullanabilir, kullanıcı doldurduğunda verilerin senkron kalmasını sağlayabiliriz.

## Adım 4: PDF'e TextBox ekleme – widget açıklamaları yerleştirme

Bir **widget açıklaması**, bir sayfadaki görsel dikdörtgeni mantıksal form alanına bağlar. Her sayfada bir widget ekleyeceğiz.

```csharp
// Widget on the first page (coordinates: lower‑left X,Y – upper‑right X,Y)
var firstPageWidget = new WidgetAnnotation(
    firstPage,
    new Rectangle(50, 700, 200, 750))
{
    Parent = textBoxField,
    // Optional visual properties
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};

// Widget on the second page, positioned slightly lower
var secondPageWidget = new WidgetAnnotation(
    secondPage,
    new Rectangle(50, 600, 200, 650))
{
    Parent = textBoxField,
    HighlightingMode = HighlightingMode.Invert,
    Border = new Border(BorderStyle.Solid, 1, Color.Black)
};
```

*Neden önemli:*  
`WidgetAnnotation`, metin kutusunun nerede görüneceğini ve nasıl görüneceğini tanımlar. Aynı `Parent` (`textBoxField`) atanarak, iki widget de aynı temel veri alanına referans verir. Kullanıcı bir widget'ta yazdığında diğer sayfada da aynı değer anında görünür.

## Adım 5: PDF'i kaydedin ve sonucu doğrulayın

Son olarak belgeyi diske yazın:

```csharp
// Save the PDF to the output folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.pdf");
pdfDocument.Save(outputPath);

Console.WriteLine($"PDF saved to {outputPath}");
```

`output.pdf` dosyasını Adobe Acrobat Reader’da açtığınızda:

* Belge iki sayfa gösterir.
* Her sayfada “Comments” etiketiyle bir metin kutusu bulunur.
* Her iki sayfadaki metin kutusuna yazılanlar anında birbirini günceller (aynı alan adı paylaşılır).

### Beklenen çıktı ekran görüntüsü

![İki sayfada metin kutulu PDF](https://example.com/pdf-form-screenshot.png "etkileşimli form alanlarına sahip PDF belge oluşturma")

*(Görselin alt metni erişilebilirlik ve SEO için anahtar kelimeyi içerir.)*

## Yaygın varyasyonlar ve kenar durumları

| Durum | Nasıl ele alınır |
|-----------|------------------|
| **İki sayfadan fazla** | Yeni sayfalar için ek `WidgetAnnotation` nesneleri oluşturun, aynı `textBoxField`'ı yeniden kullanın. |
| **Sayfa başına farklı alan adları** | Ayrı `TextBoxField` örnekleri oluşturun (ör. `CommentsPage1`, `CommentsPage2`) ve her widget'a kendi parent'ını atayın. |
| **Çok satırlı metin kutusu** | Widget'ları eklemeden önce `textBoxField.Multiline = true;` satırını ekleyin. |
| **Salt okunur alanlar** | Kullanıcı düzenlemesini önlemek için `textBoxField.ReadOnly = true;` ayarlayın. |
| **Özel yazı tipleri** | Bir `TrueTypeFont` yükleyin ve `textBoxField.DefaultAppearance = new DefaultAppearance(font, 12, Color.Black);` ile atayın. |

Bu varyasyonlar, AcroForm API'sinin ne kadar esnek olduğunu gösterirken temel desenin aynı kalmasını sağlar.

## Adım adım özet (hızlı referans)

1. **PDF belgesi oluştur** ve gerekli sayfaları ekle.  
2. **AcroForm'u başlat** ve bir `TextBoxField` tanımla.  
3. **Widget açıklamaları** ekleyerek metin kutusunu her sayfaya yerleştir.  
4. **Belgeyi kaydet** ve etkileşimli davranışı test et.

## Sonraki adımlar

Artık **PDF'e metin kutusu eklemeyi** ve **AcroForm PDF oluşturmayı** bildiğinize göre formu genişletebilirsiniz:

* `CheckBoxField`, `RadioButtonField` ve `ComboBoxField` kullanarak onay kutuları, radyo düğmeleri veya açılır listeler ekleyin.
* Form verilerini sunucu tarafı işleme için FDF veya XFDF olarak dışa aktarın.
* Alanlara dinamik doğrulama için JavaScript eylemleri uygulayın.

Tam form alanı türleri ve gelişmiş stil seçenekleri için resmi Aspose.Pdf belgelerini keşfedin.

---

*Bu öğreticide **PDF belgesi oluşturma**, **PDF'e sayfa ekleme**, **etkileşimli PDF formu oluşturma**, **PDF'e metin kutusu ekleme** ve **AcroForm PDF oluşturma** konularını kısa, çalıştırılabilir bir örnekle öğrendiniz. Uygulamanızın ihtiyaçlarına göre ek alan türleri ve düzen ayarlarıyla denemeler yapmaktan çekinmeyin.*

## Bir sonraki öğrenmeniz gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose ile PDF Oluşturma – Form Alanı ve Sayfalar Ekleme](/pdf/english/net/programming-with-forms/how-to-create-pdf-with-aspose-add-form-field-and-pages/)
- [PDF'e Metin Kutusu Ekleme – PDF Form Alanı Oluşturma ve Düzenlenmiş PDF Belgesi Kaydetme](/pdf/english/net/programming-with-forms/how-to-add-text-box-pdf-create-pdf-form-field-save-edited-pd/)
- [Aspose ile PDF Belgesi Oluşturma – Sayfa, Metin Kutusu ve Form Ekleme](/pdf/english/net/forms-annotations/create-pdf-document-with-aspose-add-page-text-box-and-form/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}