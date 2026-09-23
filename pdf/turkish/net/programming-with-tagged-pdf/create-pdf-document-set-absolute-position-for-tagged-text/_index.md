---
category: general
date: 2026-03-24
description: PDF belgesi oluşturun ve etiketli metin için mutlak konum ayarlamayı
  öğrenin. Bu öğreticide span öğesinin nasıl ekleneceği, etiketli içeriğin nasıl ekleneceği
  ve metnin sayfada nasıl konumlandırılacağı gösterilmektedir.
draft: false
keywords:
- create pdf document
- set absolute position
- add span element
- how to add tagged
- position text on page
language: tr
og_description: PDF belgesi oluşturun ve etiketli PDF içeriğiyle sayfada mutlak konum
  ayarlamayı, span öğesi eklemeyi ve metni konumlandırmayı anında görün.
og_title: PDF Belgesi Oluştur – Etiketli Metnin Mutlak Konumlandırması
tags:
- Aspose.Pdf
- C#
- PDF Tagging
title: PDF Belgesi Oluştur – Etiketli Metin İçin Mutlak Konum Ayarla
url: /tr/net/programming-with-tagged-pdf/create-pdf-document-set-absolute-position-for-tagged-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Belgesi Oluştur – Etiketli Metin İçin Mutlak Konum Ayarla

Hiç **pdf belge oluştur** ihtiyacı duydunuz mu, içinde erişilebilir, etiketli metin tam istediğiniz konumda yer alıyor? Belki form‑gibi bir PDF oluşturuyorsunuz ve etiketin kesin bir koordinatta durması gerekiyor, ya da bir sertifika üretiyorsunuz ve ismin arka plan görüntüsüyle mükemmel hizalanması lazım.  

Bu rehberde, **etiketli içerik ekleme**, **mutlak konum ayarlama** ve **span öğesi ekleme** konularını gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz, böylece **sayfada metni konumlandır**abilirsiniz tahmin etmeden. Harici referanslar yok—sadece kopyalayıp‑yapıştırabileceğiniz kod ve her satırın “neden”ini açıklayan bilgiler.

## Önkoşullar

- .NET 6+ (veya .NET Framework 4.6+) C# derleyicisi ile  
- NuGet üzerinden kurulan Aspose.Pdf for .NET (yazım zamanı itibarıyla en son sürüm, 23.12)  
- C# sözdizimi hakkında temel aşinalık  

Eğer bunlara sahipseniz, başlayalım.

---

## PDF Belgesi Oluştur – Mutlak Konumu Ayarlama

İlk yaptığımız şey boş bir `Document` nesnesi oluşturmak. Bu nesne tüm PDF dosyasını temsil eder ve bize etiketli‑içerik ağacına erişim sağlar.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Tagged;

// Step 1: Create a new PDF document
using var pdfDocument = new Document();
```

**Neden önemli:**  
`Document` PDF yapısının köküdür. Önce onu oluşturarak görsel öğeler (sayfalar, grafikler) ve mantıksal yapı (etiketler) için bir tuval olduğundan emin oluruz. `using` ifadesi dosyanın düzgün bir şekilde serbest bırakılmasını sağlar, bu da Windows'ta dosya‑tanıtıcı sızıntılarını önler.

## Etiketli İçeriği Etkinleştir (Etiketli Nasıl Eklenir)

Herhangi bir etiketli öğe eklemeden önce, belgenin *etiketli* olarak işaretlenmiş olması gerekir. Aspose.Pdf otomatik olarak bir `TaggedContent` nesnesi oluşturur, ancak bayrağı açmanız gerekir.

```csharp
// Step 2: Mark the document as tagged (required for accessibility)
pdfDocument.TaggedContent = true;
```

**Arka planda ne oluyor?**  
`TaggedContent`'i `true` olarak ayarlamak, PDF okuyucularına dosyanın mantıksal bir yapı ağacı içerdiğini söyler. Bu, ekran okuyucular ve `SetPosition` metodunun bir span öğesi üzerinde doğru çalışması için kritiktir.

## Etiketli‑İçerik Ağacının Kök Öğesini Al

Kök öğe, tüm yapısal etiketlerin (ör. `<Document>`, `<Section>`, `<Span>`) giriş noktasıdır. PDF'nin görünmez “body”si gibi düşünün.

```csharp
// Step 3: Retrieve the root element of the tag tree
var rootElement = pdfDocument.TaggedContent.RootElement;
```

**Neden köke ihtiyacımız var:**  
Tüm sonraki etiketler ağacın bir yerinde eklenmelidir; aksi takdirde erişilebilirlik hiyerarşisinde görünmezler.

## Span Öğesi Ekle – Satır İçi Metin İçin Yapı Taşı

*Span*, PDF'de HTML `<span>` öğesine eşdeğerdir—kısa metin parçalarını tam konumlandırmak istediğinizde mükemmeldir.

```csharp
// Step 4: Create a span element that will hold the text
var spanElement = rootElement.CreateSpanElement();
```

**Tasarım notu:**  
Daha zengin biçimlendirme (kalın, italik, hiperlinkler) gerekiyorsa, span'i bir `<Paragraph>` içinde sarabilir veya daha sonra `TextFragment` nesnelerini kullanabilirsiniz. Mutlak konumlandırma için sade bir span en hafif seçenektir.

## Mutlak Konum Ayarla – X=100, Y=200

Şimdi eğlenceli kısma geliyoruz: span'i sayfada tam bir konuma yerleştirmek. Koordinat sistemi sol‑alt köşeden (0,0) başlar ve puan (1 pt ≈ 1/72 in) kullanır.

```csharp
// Step 5: Position the span at an absolute location (X=100, Y=200)
spanElement.SetPosition(100, 200);
```

**Neden mutlak konumlandırma?**  
Piksel‑tam bir düzen gerektiğinde—sertifikalar, faturalar veya formlar gibi—göreceli akış (sol‑sağ metin gibi) yeterli değildir. `SetPosition` normal metin akışını atlar ve öğeyi belirttiğiniz yerde sabitler.

## Span'e Metin Ekle

Span konumlandırıldıktan sonra gerçek dizeyi ekliyoruz.

```csharp
// Step 6: Add the desired text to the span
spanElement.AddText("Positioned tagged text");
```

**İpucu:**  
Unicode karakterlerine veya sağ‑to‑sol script'lere ihtiyacınız varsa, sadece dizeyi geçirin; Aspose.Pdf kodlamayı otomatik olarak yönetir.

## Span'i Kök Öğeye Ekle

Son olarak span'i belgenin mantıksal ağacına ekliyoruz, böylece final PDF'nin bir parçası olur.

```csharp
// Step 7: Append the span to the root so it becomes part of the PDF structure
rootElement.AppendChild(spanElement);
```

**Bu adımı unutursanız ne olur?**  
Span bellekte var olur ama dosyaya serileştirilmez, bu yüzden metin görünmez ve erişilebilirlik ağacı eksik kalır.

## Tam, Çalıştırılabilir Örnek

Aşağıda bir konsol uygulamasına koyabileceğiniz tam program yer alıyor. Tek sayfalı bir PDF oluşturur, (100, 200) konumunda etiketli bir span ekler ve dosyayı `TaggedPositioned.pdf` olarak kaydeder.

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

**Beklenen çıktı:**  
`TaggedPositioned.pdf` dosyasını herhangi bir görüntüleyicide (Adobe Acrobat, Foxit, vb.) açın. Sol kenardan 100 pt, alt kenardan 200 pt uzaklıkta **“Positioned tagged text”** ifadesini göreceksiniz. *Tags* panelini incelerseniz, belgenin kökünün altında bir `<Span>` öğesi listelenecek, içeriğin doğru şekilde etiketlendiğini onaylayacaktır.

## Yaygın Sorular & Kenar Durumları

### İlk sayfa dışında belirli bir sayfada metin konumlandırmam gerekirse?

İstediğiniz sayfayı ekleyin (`var page = pdfDocument.Pages[3];`) `SetPosition` çağırmadan önce. Span otomatik olarak aktif sayfa bağlamına eklenir.

### Konumu inç ya da santimetre cinsinden ayarlayabilir miyim?

`SetPosition` puan (points) kabul eder. Dönüştürme formülleri:  
- **İnç → puan:** `points = inches * 72`  
- **Santimetre → puan:** `points = cm * 28.3465`

### Span'in yazı tipini veya rengini nasıl değiştiririm?

Span'i oluşturduktan sonra `TextState`'ini alıp değiştirebilirsiniz:

```csharp
var textState = spanElement.TextState;
textState.Font = FontRepository.FindFont("Arial");
textState.FontSize = 12;
textState.ForegroundColor = Color.GetBlack();
```

### Belgenin zaten mevcut etiketleri varsa ne olur?

Yine de yeni bir span oluşturup (`rootElement`, belirli bir `<Section>` vb.) herhangi bir mevcut öğeye ekleyebilirsiniz. Mantıksal hiyerarşiyi koruduğunuzdan emin olun—ekran okuyucular iyi yapılandırılmış bir ağaç bekler.

### Bu PDF/A veya PDF/UA uyumluluğu ile çalışır mı?

Evet. Etiketli PDF'ler PDF/UA için temel bir gereksinimdir. PDF/A ihtiyacınız varsa, içeriği oluşturduktan sonra `pdfDocument.Convert(new PdfAConversionOptions(PdfAStandard.PdfA_1b));` çağırın.

## Profesyonel İpuçları & Tuzaklar

- **Pro tip:** İçeriği konumlandırmadan önce her zaman bir sayfa ekleyin. Sayfa olmadan `SetPosition` sessizce başarısız olur çünkü render edilecek bir yer yoktur.  
- **Birimlere dikkat edin:** UI tasarımından gelen pikselleri PDF puanlarıyla karıştırmak metninizi yanlış konumlandırır. Dönüşümünüzü iki kez kontrol edin.  
- **Performans ipucu:** Binlerce PDF oluşturuyorsanız, tek bir `Document` örneğini yeniden kullanın ve çalıştırmalar arasında `pdfDocument.Pages.Clear()` çağırarak aşırı bellek tahsisinden kaçının.  
- **Erişilebilirlik hatırlatması:** Etiketleme sadece hoş bir özellik değil; birçok düzenleme (Section 508, EN 301 549) bunu zorunlu kılar. `CreateSpanElement` kullanmak, metnin yardımcı teknolojiler tarafından bulunabilir olmasını sağlar.

## Sonuç

Şimdi **pdf belge oluşturduk**, **mutlak konum ayarladık**, **span öğesi ekledik** ve **etiketli içerik eklemenin** nasıl yapılacağını gösterdik, böylece **sayfada metni** piksel‑tam doğrulukla konumlandırabilirsiniz. Tam örnek çalıştırılmaya hazır ve açıklamalar hem *nasıl* hem de *neden* üzerine odaklandı—geliştiricilerin (ve AI asistanlarının) güvenilir bir çözüm aradığında ihtiyaç duyduğu tam bilgi.

Sonraki adımlarda şunları keşfedebilirsiniz:

- Konumlandırılmış metnin arkasına su damgası içeren sertifikalar için görüntüler eklemek.  
- Mutlak konumlandırma gerektiren çok satırlı bloklar için `CreateParagraphElement` kullanmak.  
- Katı erişilebilirlik denetimlerini karşılamak için PDF/UA'ya dışa aktarmak.  

Koordinatları, yazı tiplerini veya renkleri istediğiniz gibi değiştirin—deney yapmak, etiketli PDF oluşturmayı öğrenmenin en hızlı yoludur. Bir sorunla karşılaşırsanız, aşağıya yorum bırakın; iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}