---
category: general
date: 2026-10-26
description: Aspose.PDF for C# kullanarak boş PDF sözlüğü oluşturmayı ve PDF kaynaklarını
  düzenlemeyi öğrenin. Tam kod örneğiyle adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create empty PDF dictionary
- edit PDF resources
- Aspose.PDF C#
- PDF manipulation C#
- PDF graphics state
language: tr
lastmod: 2026-10-26
og_description: Aspose.PDF for C# ile boş PDF sözlüğü oluşturun ve PDF kaynaklarını
  düzenleyin. PDF'lerde grafik durumlarını değiştirmek için bu kapsamlı öğreticiyi
  izleyin.
og_image_alt: Screenshot showing creation of empty PDF dictionary in Aspose.PDF
og_title: Boş PDF sözlüğü oluşturun ve C#'ta PDF kaynaklarını düzenleyin – Aspose.PDF
  rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  headline: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  type: TechArticle
- description: Learn to create empty PDF dictionary and edit PDF resources using Aspose.PDF
    for C#. Step‑by‑step guide with full code example.
  name: How to create empty PDF dictionary and edit PDF resources with Aspose.PDF
    in C#
  steps:
  - name: Populate the graphics state entries
    text: 'Add the standard keys:'
  - name: Register the new graphics state in the resource dictionary
    text: Give the state a name (`GS0`) and add it to the `ExtGState` dictionary that
      lives inside the page resources.
  - name: Expected output
    text: 'Running the program prints:'
  type: HowTo
tags:
- Aspose.PDF
- C#
- PDF
title: Aspose.PDF ile C#'ta boş PDF sözlüğü oluşturma ve PDF kaynaklarını düzenleme
url: /tr/net/programming-with-document/how-to-create-empty-pdf-dictionary-and-edit-pdf-resources-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.PDF ile C#’ta boş PDF sözlüğü oluşturma ve PDF kaynaklarını düzenleme

Eğer bir **boş PDF sözlüğü oluşturmak** ve ardından **PDF kaynaklarını düzenlemek** istiyorsanız, bu kılavuz tam adımları gösterir. Mevcut bir PDF’in ilk sayfasına özel bir grafik durumu ekleyen tam, çalıştırılabilir bir örnek göreceksiniz.

Düşük‑seviye PDF nesneleriyle çalışmak göz korkutucu olabilir, ancak Aspose.PDF sözlük manipülasyonu için net bir API sunar. Bu öğreticinin sonunda her işlemin neden önemli olduğunu ve kodu diğer kaynak türleri için nasıl uyarlayabileceğinizi anlayacaksınız.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 (veya daha yeni bir sürüm).
* **Aspose.PDF for .NET** lisanslı bir kopya – ücretsiz deneme sürümü test için yeterlidir.
* Visual Studio 2022 gibi bir IDE.
* Kod içinde referans verebileceğiniz bir klasörde bulunan `input.pdf` adlı bir PDF dosyası.

`Aspose.Pdf` dışındaki ek NuGet paketlerine ihtiyaç yoktur.

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol projesi oluşturun ve Aspose.PDF paketini ekleyin:

```bash
dotnet new console -n PdfDictionaryDemo
cd PdfDictionaryDemo
dotnet add package Aspose.Pdf
```

`Program.cs` dosyasında kullanacağınız ad alanlarını içe aktarın:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;
```

Bu içe aktarmalar, **boş PDF sözlüğü oluşturmak** nesnelerini ve mevcut kaynak sözlüklerini değiştirebilmenizi sağlayan `Document`, `DictionaryEditor` ve COS (Canonical Object Structure) sınıflarını ortaya çıkarır.

## Adım 2: PDF dosyalarını içeren klasörü tanımlayın

`input.pdf` dosyasının bulunduğu dizini belirtin. Mutlak bir yol kullanmak, program farklı bir çalışma dizininden çalıştığında belirsizliği ortadan kaldırır.

```csharp
// Step 1: Define the folder that contains the PDF files
string dataDir = @"C:\PdfDemo\";
```

`C:\PdfDemo\` kısmını kendi makinenizdeki yol ile değiştirin. Yolu bir değişkende tutmak, hem giriş hem de çıkış dosyaları için yeniden kullanımı kolaylaştırır.

## Adım 3: Kaynak PDF belgesini açın

PDF’i bir `using` bloğu içinde yükleyin; böylece dosya tutamağı otomatik olarak serbest bırakılır.

```csharp
// Step 2: Open the source PDF document
using (var pdfDocument = new Document(dataDir + "input.pdf"))
{
    // The rest of the workflow lives inside this block
}
```

Belgeyi açmak, sayfa koleksiyonuna, kaynak sözlüklerine ve düşük‑seviye COS nesnelerine erişim sağlar.

## Adım 4: İlk sayfayı ve onun kaynak sözlüğünü alın

İlk sayfa `1` ile indekslenir (PDF sayfaları 1‑tabanlıdır). Sayfanın `Resources` sözlüğünü alın ve güvenli düzenleme için bir `DictionaryEditor` ile sarmalayın.

```csharp
// Step 3: Access the first page and its resource dictionary
var firstPage = pdfDocument.Pages[1];
var resourcesEditor = new DictionaryEditor(firstPage.Resources);
```

`DictionaryEditor`, temel COS yapısını soyutlayarak PDF’i bozmadan girişleri okumanıza veya oluşturmanıza olanak tanır.

## Adım 5: Yeni bir grafik durumu için **boş PDF sözlüğü oluşturun**

Bir grafik durumu şeffaflık, karışım modu ve diğer çizim parametrelerini kontrol eder. Özel bir durum eklemek için önce boş bir sözlük, ardından gerekli girişlerle doldurmanız gerekir.

```csharp
// Step 4: Retrieve the ExtGState dictionary and add a new graphics state
var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

// Create an empty dictionary that will hold the graphics state parameters
var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
```

`CreateEmptyDictionary` çağrısı, **boş PDF sözlüğü oluşturma** nesnelerinin çekirdeğidir. Aynı belgeye ait bir COS sözlüğü döndürür, böylece çapraz referans bütünlüğü korunur.

### Grafik durumu girişlerini doldurun

Standart anahtarları ekleyin:

* `CA` – çizgi alfa sabiti (aralık 0 – 1).
* `ca` – dolgu alfa sabiti.
* `BM` – karışım modu adı.

```csharp
var graphicsStateEntries = new[]
{
    new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
    new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
    new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
};

foreach (var entry in graphicsStateEntries)
    newGraphicsState.Add(entry);
```

Her giriş, az önce oluşturduğunuz boş sözlüğe eklenir. Tanımı ekleme döngüsünden ayırmak, kodun okunabilirliğini artırır ve ileride ek anahtarlar eklemeyi kolaylaştırır.

### Yeni grafik durumunu kaynak sözlüğüne kaydedin

Duruma bir isim verin (`GS0`) ve sayfa kaynakları içinde bulunan `ExtGState` sözlüğüne ekleyin.

```csharp
// Name the new graphics state "GS0"
extGStateDict.Add("GS0", newGraphicsState);
```

Artık sayfanın kaynak sözlüğü, içerik akışlarına daha sonra uygulayabileceğiniz özel grafik durumuna bir referans içeriyor.

## Adım 6: Güncellenen PDF’i kaydedin

Son olarak, değiştirilmiş belgeyi yeni bir dosyaya yazın. Orijinali bozulmadan bırakmak, değişiklikleri doğrulamanıza yardımcı olur.

```csharp
// Step 5: Save the updated PDF
pdfDocument.Save(dataDir + "output.pdf");
```

`output.pdf` dosyasını grafik durumu incelemesini destekleyen bir görüntüleyicide (ör. Adobe Acrobat Pro) açtığınızda, `ExtGState` sözlüğünün `GS0` adlı bir giriş içerdiğini göreceksiniz.

## Tam kaynak kodu

Tüm parçaları bir araya getirdiğinizde bağımsız bir program elde edersiniz:

```csharp
using System;
using System.Collections.Generic;
using Aspose.Pdf;
using Aspose.Pdf.Cos;

class Program
{
    static void Main()
    {
        // Step 1: Define the folder that contains the PDF files
        string dataDir = @"C:\PdfDemo\"; // adjust to your environment

        // Step 2: Open the source PDF document
        using (var pdfDocument = new Document(dataDir + "input.pdf"))
        {
            // Step 3: Access the first page and its resource dictionary
            var firstPage = pdfDocument.Pages[1];
            var resourcesEditor = new DictionaryEditor(firstPage.Resources);

            // Step 4: Retrieve the ExtGState dictionary and add a new graphics state
            var extGStateDict = resourcesEditor["ExtGState"].ToCosPdfDictionary();

            // **Create empty PDF dictionary** for the new graphics state
            var newGraphicsState = CosPdfDictionary.CreateEmptyDictionary(pdfDocument);
            var graphicsStateEntries = new[]
            {
                new KeyValuePair<string, ICosPdfPrimitive>("CA", new CosPdfNumber(1)),
                new KeyValuePair<string, ICosPdfPrimitive>("ca", new CosPdfNumber(0.5)),
                new KeyValuePair<string, ICosPdfPrimitive>("BM", new CosPdfName("Normal"))
            };

            foreach (var entry in graphicsStateEntries)
                newGraphicsState.Add(entry);

            // Register the new graphics state as "GS0"
            extGStateDict.Add("GS0", newGraphicsState);

            // Step 5: Save the updated PDF
            pdfDocument.Save(dataDir + "output.pdf");
        }

        Console.WriteLine("PDF updated successfully.");
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda şu satırları görürsünüz:

```
PDF updated successfully.
```

ve aynı klasörde `output.pdf` oluşturulur. Dosyayı açtığınızda **Resources → ExtGState → GS0** altında, belirlediğiniz parametrelerle yeni bir giriş bulunur.

## Yaygın varyasyonlar ve kenar durumları

| Durum | Kodu nasıl uyarlamalısınız |
|-----------|-----------------------|
| **Birden fazla sayfa** aynı grafik durumunu gerektiriyor | Sözlüğü bir kez oluşturun, ardından aynı `GS0` referansını her sayfanın `ExtGState` sözlüğüne ekleyin. |
| **Farklı karışım modu** (ör. `Multiply`) | `CosPdfName("Normal")` değerini `CosPdfName("Multiply")` ile değiştirin. |
| **Mevcut ExtGState sözlüğü yok** | `resourcesEditor["ExtGState"]` erişmeden önce `resourcesEditor.ContainsKey("ExtGState")` kontrol edin. Yoksa yeni bir boş sözlük oluşturup `firstPage.Resources` içine ekleyin. |
| **Büyük PDF’ler** bellek baskısı oluşturuyor | Sayfaları akış olarak yükleyen `PdfDocument.Load` aşırı yüklemesini kullanın veya `using` bloğu içinde sayfaları tek tek işleyin. |
| **Diğer kaynakları düzenleme ihtiyacı** (fontlar, XObject’ler) | `resourcesEditor` aramasındaki `"ExtGState"` ifadesini `"Font"` veya `"XObject"` ile değiştirin, ardından boş bir sözlük oluşturup doldurma desenini aynı şekilde izleyin. |

Bu varyasyonlar, aynı **boş PDF sözlüğü oluşturma** deseninin **PDF kaynaklarını düzenleme** ihtiyacınız olan her tür kaynak için nasıl uygulanabileceğini gösterir.

## Profesyonel ipuçları

* **Sonucu doğrulayın** – kaydettikten sonra PDF’i ham kaynak sözlüğünü gösteren bir araçta (ör. PDF‑Box’un `PDFDebugger`ı) açın ve girişin gerçekten var olduğunu kontrol edin.
* **Sözlükleri yeniden kullanın** – aynı grafik durumunu birçok sayfaya ekliyorsanız, sözlüğü bir değişkende tutup referans verin; her seferinde yeniden oluşturmayın.
* **Sürüm uyumluluğu** – kod Aspose.PDF 23.12 ve üzeri sürümlerle çalışır. Daha eski sürümler `CosDictionary` yerine `CosPdfDictionary` kullanmanızı gerektirebilir.

## Sonuç

Artık Aspose.PDF for C# kullanarak **boş PDF sözlüğü oluşturma** nesnelerini ve **PDF kaynaklarını düzenleme** işlemlerini nasıl yapacağınızı biliyorsunuz. Bu öğreticide bir belgeyi açma, sayfanın kaynak sözlüğüne erişme, özel bir grafik durumu oluşturma, kaydetme ve sonucu doğrulama adımlarını ele aldık. Bundan sonra diğer kaynak türleriyle deney yapabilir, birden çok grafik durumu birleştirebilir veya bu tekniği daha büyük bir PDF işleme hattına entegre edebilirsiniz.

---

*Daha fazlasını keşfetmeye hazır mısınız? İçerik akışına özel bir **ExtGState** ekleyin ya da yeni fontları gömmek için **Font** sözlüğünü manipüle edin. İkisi de aynı boş sözlük oluşturma ve PDF kaynaklarını düzenleme desenini izler.*


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları denemeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Edit PDF Resource Dictionary with Aspose.PDF – C# Guide](/pdf/english/net/programming-with-operators/edit-pdf-resource-dictionary-with-aspose-pdf-c-guide/)
- [Create custom graphics state in PDF using Aspose.Pdf](/pdf/english/net/programming-with-operators/create-custom-graphics-state-in-pdf-using-aspose-pdf/)
- [How to create empty graphics state in a PDF with C#](/pdf/english/net/programming-with-operators/how-to-create-empty-graphics-state-in-a-pdf-with-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}