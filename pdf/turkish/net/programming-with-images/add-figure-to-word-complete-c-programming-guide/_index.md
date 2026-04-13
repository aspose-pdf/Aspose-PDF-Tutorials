---
category: general
date: 2026-04-12
description: C# ile Word’e hızlıca şekil ekleyin. Word’de şekli nasıl konumlandıracağınızı,
  docx dosyasına nasıl ekleyeceğinizi ve gelişmiş düzen için özel XML eklemeyi öğrenin.
draft: false
keywords:
- add figure to word
- position figure in word
- insert figure into docx
- how to add custom xml
- how to position shape word
language: tr
og_description: C# ile Word’e hızlıca şekil ekleyin. Word’de şekli nasıl konumlandıracağınızı,
  docx dosyasına şekil eklemeyi ve gelişmiş düzen için özel XML eklemeyi öğrenin.
og_title: Word'e Şekil Ekle – Tam C# Programlama Rehberi
tags:
- C#
- Word Automation
- Document Generation
title: Word'e Şekil Ekle – Tam C# Programlama Rehberi
url: /tr/net/programming-with-images/add-figure-to-word-complete-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word'e Şekil Ekle – Tam C# Programlama Rehberi

Ever needed to **add figure to Word** but weren’t sure where to start? You’re not alone. In many office‑automation projects the missing piece is a nicely placed picture or diagram that lives inside a custom XML part. This guide shows you exactly how to **position figure in Word**, insert the figure into a *.docx* file, and even tweak the underlying custom XML so the shape behaves like any native Word object.

Word'e **add figure to Word** eklemeniz gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz. Birçok ofis‑otomasyon projesinde eksik parça, özel bir XML bölümünün içinde yer alan güzel konumlandırılmış bir resim veya diyagramdır. Bu rehber, **position figure in Word**'ın tam olarak nasıl yapılacağını, şekli bir *.docx* dosyasına eklemeyi ve hatta alttaki özel XML'i şeklin yerel bir Word nesnesi gibi davranmasını sağlayacak şekilde ayarlamayı gösterir.

We’ll walk through a real‑world example using the GemBox.Document library (free for small files, commercial for larger workloads). By the end you’ll have a self‑contained, runnable program that drops a figure at coordinates X = 50, Y = 200 inside a tagged‑content container. No vague “see the docs” shortcuts—just clear code, why it works, and tips you can copy straight into your own project.

GemBox.Document kütüphanesini (küçük dosyalar için ücretsiz, daha büyük işler için ticari) kullanarak gerçek bir örnek üzerinden ilerleyeceğiz. Sonunda, X = 50, Y = 200 koordinatlarında bir etiketli‑içerik konteyneri içinde şekil yerleştiren, bağımsız ve çalıştırılabilir bir programınız olacak. Belirsiz “belgelere bak” kısayolları yok—sadece net kod, neden çalıştığı ve kendi projenize doğrudan kopyalayabileceğiniz ipuçları.

## Gereksinimler

- .NET 6.0 veya daha yenisi (kod .NET Core 3.1 ile de derlenir)
- **GemBox.Document** NuGet paketi (`Install-Package GemBox.Document`)
- Başlangıç Word dosyası (`input.docx`) zaten şeklin görünmesini istediğiniz özel XML etiketini içeriyor
- Temel C# bilgisi (her satırın neden önemli olduğunu göreceksiniz)

> **Pro tip:** Önceden etiketlenmiş bir belgeniz yoksa, Word'de bir *Content Control* → *XML Mapping Pane* → özel bir XML bölümü eşleştirerek oluşturabilirsiniz. Kütüphane bu kontrolü `TaggedContent` olarak ele alır.

## Adım 1 – Kaynak Belgeyi Yükle

İlk yaptığımız şey mevcut *.docx* dosyasını açmaktır. `Document`, tüm GemBox işlemlerinin giriş noktasıdır.

```csharp
using GemBox.Document;
using System.Drawing;

// Set the license key (free version uses a limited license key)
ComponentInfo.SetLicense("FREE-LIMITED-KEY");

// Step 1: Load the source document
Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
```

*Why?* Loading the file gives us access to its internal parts, including any custom XML containers. Without this, we couldn’t locate the `TaggedContent` node that will hold our figure.

*Why?* Dosyayı yüklemek, özel XML konteynerleri dahil iç bölümlerine erişmemizi sağlar. Bunu yapmazsak, şeklimizi tutacak `TaggedContent` düğümünü bulamazdık.

## Adım 2 – Etiketli İçeriğe Eriş (Özel XML Konteyneri)

Özel XML, Word'de bir *content control* içinde depolanır. GemBox bunu `TaggedContent` olarak sunar.

```csharp
// Step 2: Access the document's tagged content (the container for custom XML)
TaggedContent taggedContent = doc.TaggedContent;
```

If the document has multiple tagged sections, `TaggedContent` returns the **first** one. You can also enumerate `doc.TaggedContents` to pick a specific tag by name.

Belge birden fazla etiketli bölüm içeriyorsa, `TaggedContent` **ilk** olanı döndürür. Ayrıca `doc.TaggedContents` üzerinden döngü yaparak isimle belirli bir etiketi seçebilirsiniz.

## Adım 3 – Şekil Öğesini Oluştur

`FigureElement`, Word tarafından *shape* olarak kabul edilen bir resim, grafik veya herhangi bir görsel nesneyi temsil eder. Bunu etiketli konteyner içinde oluşturacağız.

```csharp
// Step 3: Create a new figure element that will be placed inside the tagged content
FigureElement figure = taggedContent.CreateFigureElement();
```

*Why create a figure here?* By attaching it to the custom XML node, Word knows the figure belongs to that logical section, which is crucial for later editing or content‑control‑based workflows.

*Neden burada bir şekil oluşturuyoruz?* Bunu özel XML düğümüne ekleyerek, Word şeklin o mantıksal bölüme ait olduğunu bilir; bu, sonraki düzenlemeler veya content‑control‑tabanlı iş akışları için kritiktir.

## Adım 4 – Şekli Tam Olarak Konumlandır

Word, konumlandırma için puan (1 pt ≈ 1/72 in) kullanır. `PointF` yapısı X/Y koordinatlarını kolayca ayarlamamızı sağlar.

```csharp
// Step 4: Position the figure at the desired coordinates (X = 50, Y = 200)
figure.Position = new PointF(50, 200);
```

> **How to position shape word:** `Position` özelliği, ilk değerin yatay kayma (sol) ve ikinci değerin sayfa kenar boşluğuna göre dikey kayma (üst) olduğu bir `PointF` alır. Yerleşimi ince ayarlamak için bu sayıları değiştirin.

## Adım 5 – Şekli Etiketli İçerik Ağacına Ekle

Şimdi şekli özel XML ağacının kök öğesine ekliyoruz. Bu, şekli fiziksel olarak Word belgesine ekler.

```csharp
// Step 5: Insert the figure into the root element of the tagged content tree
taggedContent.RootElement.AppendChild(figure);
```

At this point the figure lives inside the document, but it doesn’t have an image source yet. Let’s add a simple PNG from disk.

Bu noktada şekil belgede yer alıyor, ancak henüz bir resim kaynağı yok. Diskten basit bir PNG ekleyelim.

```csharp
// Optional: Load an image and assign it to the figure
using (var imageStream = System.IO.File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
{
    figure.Image = new Image(imageStream);
}
```

## Adım 6 – Değiştirilen Belgeyi Kaydet

Son olarak, değişiklikleri yeni bir *.docx* dosyasına yazıyoruz.

```csharp
// Step 6: Save the updated document
doc.Save(@"YOUR_DIRECTORY\output.docx");
```

When you open `output.docx` in Word, you’ll see the picture positioned exactly at (50, 200) inside the custom‑XML block you targeted.

`output.docx` dosyasını Word'de açtığınızda, hedeflediğiniz özel‑XML bloğu içinde resmin tam olarak (50, 200) konumunda olduğunu göreceksiniz.

### Tam Çalışan Örnek

```csharp
using GemBox.Document;
using System.Drawing;
using System.IO;

class Program
{
    static void Main()
    {
        // License (free version)
        ComponentInfo.SetLicense("FREE-LIMITED-KEY");

        // Load the source DOCX
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // Access the first tagged content container
        TaggedContent taggedContent = doc.TaggedContent;

        // Create a new figure element
        FigureElement figure = taggedContent.CreateFigureElement();

        // Position the figure (X = 50 pt, Y = 200 pt)
        figure.Position = new PointF(50, 200);

        // Load an image file and assign it
        using (FileStream fs = File.OpenRead(@"YOUR_DIRECTORY\sample.png"))
        {
            figure.Image = new Image(fs);
        }

        // Append the figure to the custom XML root
        taggedContent.RootElement.AppendChild(figure);

        // Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

**Expected result:** Opening `output.docx` shows the PNG placed exactly where you specified, nested inside the custom XML part. If you inspect the document’s XML (`.docx` → unzip → `word/document.xml`), you’ll see a `<w:pict>` element with the correct `<v:shape>` coordinates.

**Beklenen sonuç:** `output.docx` dosyasını açtığınızda, PNG'nin tam olarak belirttiğiniz yerde, özel XML bölümünün içinde yer aldığını görürsünüz. Belgenin XML'ini incelerseniz (`.docx` → unzip → `word/document.xml`), doğru `<v:shape>` koordinatlarına sahip bir `<w:pict>` öğesi göreceksiniz.

## Yaygın Sorular & Kenar Durumları

### Belgenin birden fazla etiketli bölümü varsa ne olur?

Etiket adına göre döngü yapmak ve seçmek için `doc.TaggedContents` kullanın:

```csharp
TaggedContent myTag = doc.TaggedContents.First(tc => tc.TagName == "MyCustomTag");
```

### Şekle bir başlık nasıl eklenir?

```csharp
figure.Caption = new CaptionElement("Figure 1 – Sample Diagram");
```

### Bu, Word 2010 ve sonrası için çalışır mı?

Evet. GemBox.Document, Open XML standardını hedefler; bu, Word 2007 + (2010, 2013, 2016, 2019 ve Microsoft 365 dahil) ile uyumludur.

### Şekli döndürmem gerekirse ne yapmalıyım?

```csharp
figure.Rotation = 45; // degrees
```

### Raster görüntü yerine vektör grafik nasıl eklenir?

```csharp
figure.Image = new Image(@"YOUR_DIRECTORY\vector.svg");
```

## Pro İpuçları & Tuzaklar

- **Dosya yolları:** Özellikle Windows dışı platformlarda sabit ayraçlardan kaçınmak için `Path.Combine` kullanın.
- **Lisans sınırlamaları:** Ücretsiz GemBox lisansı belge boyutunu 20 KB ile sınırlar. Daha büyük dosyalar için ticari bir anahtar satın alın.
- **Performans:** Toplu işleme için tek bir `Document` örneğini yeniden kullanmak bellek yükünü büyük ölçüde azaltır.
- **Şekil taşması:** Şeklin boyutları sayfa kenar boşluklarını aşarsa, Word onu kırpar. `figure.Width` ve `figure.Height` değerlerini buna göre ayarlayın.

## Sonuç

Artık **Word'e şekil ekleme**, **Word'de şekli konumlandırma** ve şeklin yerel bir öğe gibi davranması için alttaki özel XML'i nasıl manipüle edeceğinizi biliyorsunuz. Tam, çalıştırılabilir örnek, belgeyi yüklemeden, bir `FigureElement` oluşturmaya, koordinatlarını ayarlamaya, bir resim eklemeye ve son olarak güncellenmiş *.docx* dosyasını kaydetmeye kadar her adımı gösterir.

Şimdi, **insert figure into docx** ifadesini kullanarak birden fazla şekil ekleyerek, döngülerle veya anlık grafikler oluşturarak deneyler yapın. Ayrıca daha zengin içerik kontrolleri için **how to add custom xml** keşfedebilir veya tablolar ve başlıklarda **how to position shape word** öğrenebilirsiniz. Olanaklar sınırsızdır ve burada temelleri öğrendiğinize göre Word belgelerini bir profesyonel gibi otomatikleştirmeye hazırsınız.

Kodlamanın tadını çıkarın ve herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}