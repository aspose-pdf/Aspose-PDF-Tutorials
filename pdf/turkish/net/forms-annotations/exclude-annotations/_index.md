---
title: Aspose.Pdf for .NET ile Açıklamaları Hariç Tutan Yan Yana PDF Karşılaştırması
weight: 101
limit:
description: Aspose.Pdf for .NET kullanarak PDF'leri karşılaştırmak ve açıklama alanlarını hariç tutmak için adım adım rehber.
keywords: [pdf comparison, exclude annotations, Aspose.Pdf for .NET, side by side comparison, annotation bounding boxes, diff pdf]
url: /net/forms-annotations/exclude-annotations/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET kullanarak PDF'leri karşılaştırmak ve açıklama
    alanlarını hariç tutmak için adım adım rehber.
  headline: Aspose.Pdf for .NET ile Açıklamaları Hariç Tutan Yan Yana PDF Karşılaştırması
  type: TechArticle
- description: Aspose.Pdf for .NET kullanarak PDF'leri karşılaştırmak ve açıklama
    alanlarını hariç tutmak için adım adım rehber.
  name: Aspose.Pdf for .NET ile Açıklamaları Hariç Tutan Yan Yana PDF Karşılaştırması
  steps:
  - name: Birincil PDF, ikincil PDF ve çıktı diff PDF'si için dosya yollarını tanımlayın.
    text: Birincil PDF, ikincil PDF ve çıktı diff PDF'si için dosya yollarını tanımlayın.
  - name: Her iki giriş PDF dosyasının da mevcut olduğunu kontrol edin ve biri eksikse
      bir hata mesajı ile işlemi durdurun.
    text: Her iki giriş PDF dosyasının da mevcut olduğunu kontrol edin ve biri eksikse
      bir hata mesajı ile işlemi durdurun.
  - name: İki PDF dosyasını Document nesneleri (pdfA ve pdfB) olarak bir using bloğu
      içinde açın, böylece otomatik olarak imha edilirler.
    text: İki PDF dosyasını Document nesneleri (pdfA ve pdfB) olarak bir using bloğu
      içinde açın, böylece otomatik olarak imha edilirler.
  - name: pdfA içindeki her açıklamanın sınırlayıcı dikdörtgenlerini toplayın ve ignoredRectsA
      içinde saklayın.
    text: pdfA içindeki her açıklamanın sınırlayıcı dikdörtgenlerini toplayın ve ignoredRectsA
      içinde saklayın.
  - name: pdfB içindeki her açıklamanın sınırlayıcı dikdörtgenlerini toplayın ve ignoredRectsB
      içinde saklayın.
    text: pdfB içindeki her açıklamanın sınırlayıcı dikdörtgenlerini toplayın ve ignoredRectsB
      içinde saklayın.
  - name: Bir SideBySideComparisonOptions nesnesi oluşturun ve önceden toplanmış açıklama
      dikdörtgenlerini ExcludeAreas1 ve ExcludeAreas2'ye atayın; böylece bu bölgeler
      karşılaştırma sırasında yok sayılır.
    text: Bir SideBySideComparisonOptions nesnesi oluşturun ve önceden toplanmış açıklama
      dikdörtgenlerini ExcludeAreas1 ve ExcludeAreas2'ye atayın; böylece bu bölgeler
      karşılaştırma sırasında yok sayılır.
  - name: İki Document nesnesi ve yapılandırılmış seçenekleri kullanarak yan yana
      PDF karşılaştırmasını çalıştırın, sonucu outputPdf'ye yazın.
    text: İki Document nesnesi ve yapılandırılmış seçenekleri kullanarak yan yana
      PDF karşılaştırmasını çalıştırın, sonucu outputPdf'ye yazın.
  - name: Document nesnelerini imha edin ve using bloğundan çıkın.
    text: Document nesnelerini imha edin ve using bloğundan çıkın.
  - name: Karşılaştırmanın tamamlandığını ve diff PDF'nin nerede kaydedildiğini belirten
      bir onay mesajı yazdırın.
    text: Karşılaştırmanın tamamlandığını ve diff PDF'nin nerede kaydedildiğini belirten
      bir onay mesajı yazdırın.
  type: HowTo
- questions:
  - answer: Evet. Kod, ilgili `ignoredRects` listesine hiçbir dikdörtgen eklemez,
      bu yüzden `ExcludeAreas1`/`ExcludeAreas2` boş bir dizi alır ve karşılaştırıcı
      tüm sayfayı işler.
    question: Bir PDF sayfasında açıklama yoksa ne olur – karşılaştırma hâlâ çalışır
      mı?
  - answer: '`ExcludeAreas1` (veya `ExcludeAreas2`) özelliğini toplanmış dikdörtgenlere
      ayarlayın ve diğer özelliği boş bir dizi olarak bırakın; karşılaştırıcı yalnızca
      belirtilen belgedeki bölgeleri yok sayar.'
    question: Diff içinde diğer belgenin açıklamaları korunurken sadece bir belgeden
      açıklamaları hariç tutabilir miyim?
  - answer: Üst üste gelen dikdörtgenler karşılaştırıcı tarafından dahili olarak birleştirilir,
      böylece üst üste gelen açıklama sınırları çift sayım olmadan güvenli bir şekilde
      hariç tutulur.
    question: Üst üste gelen açıklama dikdörtgenleri `ExcludeAreas` ile ilgili herhangi
      bir sorun yaratır mı?
  - answer: Evet, `compareOpts.ExcludeTables = true;` olarak ayarlayın – bu bayrak
      `ExcludeAreas1`/`ExcludeAreas2` ile birlikte çalışarak tablo bölgelerini de
      yok sayar.
    question: Aynı seçenek nesnesi kullanılarak açıklamalara ek olarak tabloları da
      hariç tutmanın bir yolu var mı?
  - answer: Kod, listeye eklemeden önce `if (a != null && a.Rect != null)` kontrolünü
      yapar, bu yüzden null dikdörtgenler basitçe atlanır ve hiçbir istisna fırlatılmaz.
    question: Bir açıklamanın `Rect` özelliği null ise – kod bir istisna fırlatır
      mı?
  type: FAQPage
images:
- /net/forms-annotations/exclude-annotations/og-image.png
og_title: Açıklamalarsız PDF'leri Karşılaştır
og_description: Tüm açıklama işaretlerini atlayan yan yana bir PDF diff'i çalıştırın.
og_image_alt: Aspose.Pdf for .NET kullanarak açıklama bölgelerini hariç tutan yan yana PDF karşılaştırmasını gösteren rehber
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET ile Açıklamaları Hariç Tutan Yan Yana PDF Karşılaştırması
Bu öğretici, Aspose.Pdf for .NET kullanarak iki PDF dosyasını herhangi bir açıklama içeriğini yok sayarak nasıl karşılaştıracağınızı gösterir. Her belgeden tüm açıklamaların sınırlama kutularını çıkarır, bu bölgeleri SideBySideComparisonOptions'a aktarır ve ardından yan yana bir karşılaştırma çalıştırır. Sonuç, yalnızca açıklama dışı değişiklikleri vurgulayan bir diff PDF'dir.

---

{{< tutorial-widget sourcePath="pdf/net/forms-annotations/exclude-annotations" >}}


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/pf/tutorial-page-section >}}
## Installation Instructions
1. Download Aspose.Pdf for .NET:
   Get the latest version from the [Aspose Downloads page](https://releases.aspose.com/pdf/net/).

2. Install via NuGet:
   - Open your Visual Studio project.
   - Navigate to the NuGet Package Manager (Tools > NuGet Package Manager > Manage NuGet Packages for Solution).
   - Search for "Aspose.Pdf" and click Install.

3. Add Namespace References:
   Add the following namespace at the top of your code file:
   ```csharp
   using Aspose.Pdf;
   using Aspose.Pdf.Devices;
   using Aspose.Pdf.Operators;
   ```

4. Apply License (Optional):
   To use the full version, [apply a license](https://purchase.aspose.com/temporary-license/) or use a [free trial](https://releases.aspose.com/).

## Also See
[Aspose.Pdf for .NET Documentation](https://docs.aspose.com/pdf/net/)
[Aspose.Pdf for .NET References](https://reference.aspose.com/pdf/net/)

## Frequently asked questions

**Q: Bir PDF sayfasında açıklama yoksa ne olur – karşılaştırma hâlâ çalışır mı?**  
A: Evet. Kod, ilgili `ignoredRects` listesine hiçbir dikdörtgen eklemez, bu yüzden `ExcludeAreas1`/`ExcludeAreas2` boş bir dizi alır ve karşılaştırıcı tüm sayfayı işler.

**Q: Diff içinde diğer belgenin açıklamaları korunurken sadece bir belgeden açıklamaları hariç tutabilir miyim?**  
A: `ExcludeAreas1` (veya `ExcludeAreas2`) özelliğini toplanmış dikdörtgenlere ayarlayın ve diğer özelliği boş bir dizi olarak bırakın; karşılaştırıcı yalnızca belirtilen belgedeki bölgeleri yok sayar.

**Q: Üst üste gelen açıklama dikdörtgenleri `ExcludeAreas` ile ilgili herhangi bir sorun yaratır mı?**  
A: Üst üste gelen dikdörtgenler karşılaştırıcı tarafından dahili olarak birleştirilir, böylece üst üste gelen açıklama sınırları çift sayım olmadan güvenli bir şekilde hariç tutulur.

**Q: Aynı seçenek nesnesi kullanılarak açıklamalara ek olarak tabloları da hariç tutmanın bir yolu var mı?**  
A: Evet, `compareOpts.ExcludeTables = true;` olarak ayarlayın – bu bayrak `ExcludeAreas1`/`ExcludeAreas2` ile birlikte çalışarak tablo bölgelerini de yok sayar.

**Q: Bir açıklamanın `Rect` özelliği null ise – kod bir istisna fırlatır mı?**  
A: Kod, listeye eklemeden önce `if (a != null && a.Rect != null)` kontrolünü yapar, bu yüzden null dikdörtgenler basitçe atlanır ve hiçbir istisna fırlatılmaz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}