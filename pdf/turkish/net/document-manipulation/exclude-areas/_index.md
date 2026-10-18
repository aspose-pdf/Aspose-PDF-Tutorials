---
title: Aspose.Pdf for .NET kullanarak belirli alanları yok sayarak PDF'leri karşılaştırın
weight: 201
limit:
description: Aspose.Pdf for .NET kullanarak PDF'leri yan yana karşılaştırmayı ve seçilen bölgeleri yok saymayı öğrenin.
keywords: [Aspose.Pdf for .NET, pdf comparison, exclude areas pdf, ignore regions pdf diff, side-by-side pdf comparison, pdf diff highlighting]
url: /net/document-manipulation/exclude-areas/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET kullanarak PDF'leri yan yana karşılaştırmayı ve
    seçilen bölgeleri yok saymayı öğrenin.
  headline: Aspose.Pdf for .NET kullanarak belirli alanları yok sayarak PDF'leri karşılaştırın
  type: TechArticle
- description: Aspose.Pdf for .NET kullanarak PDF'leri yan yana karşılaştırmayı ve
    seçilen bölgeleri yok saymayı öğrenin.
  name: Aspose.Pdf for .NET kullanarak belirli alanları yok sayarak PDF'leri karşılaştırın
  steps:
  - name: İki kaynak PDF'nin ve çıktı diff PDF'nin dosya yollarını tanımlayın.
    text: İki kaynak PDF'nin ve çıktı diff PDF'nin dosya yollarını tanımlayın.
  - name: Her iki kaynak PDF dosyasının da mevcut olduğunu kontrol edin ve biri eksikse
      hata mesajı vererek işlemi durdurun.
    text: Her iki kaynak PDF dosyasının da mevcut olduğunu kontrol edin ve biri eksikse
      hata mesajı vererek işlemi durdurun.
  - name: İlk PDF'de yok sayılacak dikdörtgen alanı içeren bir dizi oluşturun.
    text: İlk PDF'de yok sayılacak dikdörtgen alanı içeren bir dizi oluşturun.
  - name: İkinci PDF'de yok sayılacak dikdörtgen alanı içeren bir dizi oluşturun.
    text: İkinci PDF'de yok sayılacak dikdörtgen alanı içeren bir dizi oluşturun.
  - name: Yan yana karşılaştırmayı yapılandırın, yok sayma alanı dizilerini ilgili
      özelliklere atayın.
    text: Yan yana karşılaştırmayı yapılandırın, yok sayma alanı dizilerini ilgili
      özelliklere atayın.
  - name: Her iki PDF'yi yükleyin ve yan yana karşılaştırmayı çalıştırın, belirtilen
      yolda diff dosyasını oluşturun.
    text: Her iki PDF'yi yükleyin ve yan yana karşılaştırmayı çalıştırın, belirtilen
      yolda diff dosyasını oluşturun.
  - name: Karşılaştırmanın tamamlandığını ve diff PDF'nin nerede kaydedildiğini belirten
      bir onay mesajı yazdırın.
    text: Karşılaştırmanın tamamlandığını ve diff PDF'nin nerede kaydedildiğini belirten
      bir onay mesajı yazdırın.
  type: HowTo
- questions:
  - answer: Koordinatlar, sayfa alt‑sol köşesinden başlayan bir orijine sahip olan
      point biriminde (inç başına 1/72) ölçülür; bu yüzden ilk iki sayı alt‑sol X/Y,
      son iki sayı ise üst‑sağ X/Y'dir.
    question: Yok sayma bölgelerini tanımlarken `Rectangle` değerleri hangi koordinat
      sistemini kullanır?
  - answer: Evet – `ExcludeAreas1` (veya `ExcludeAreas2`) dizisine birden fazla `Aspose.Pdf.Rectangle`
      nesnesi sağlayın; her dikdörtgen karşılaştırma sırasında bağımsız olarak dışlanacaktır.
    question: Aynı belgede birden fazla dikdörtgen alanı yok sayabilir miyim?
  - answer: Hayır. `ExcludeAreas1` birinci PDF'ye, `ExcludeAreas2` ise ikinci PDF'ye
      uygulanır; böylece her belge için farklı koordinatlar belirtebilirsiniz.
    question: Yok sayma dikdörtgenlerinin her iki PDF'de de aynı olması gerekir mi?
  - answer: Aspose.Pdf, tamamen sayfa dışına düşen dikdörtgenleri sessizce yok sayar;
      bunların karşılaştırma sonucuna etkisi yoktur.
    question: Bir dikdörtgen sayfa sınırlarının dışına tanımlanırsa ne olur?
  - answer: '`ExcludeAreas` dizileri sayfa başına uygulanır, bu yüzden `SideBySidePdfComparer.Compare`
      metodunu çağırmadan önce aynı `Rectangle` nesnesini her sayfanın koleksiyonuna
      eklemeniz gerekir (ör. `pdf.Pages` üzerinden döngü kurup diziyi atayın).'
    question: Bir PDF'nin her sayfasında aynı bölgeyi nasıl dışarıda bırakabilirim?
  type: FAQPage
images:
- /net/document-manipulation/exclude-areas/og-image.png
og_title: PDF'leri Karşılaştırırken Bölgeleri Yok Sayın
og_description: Yan yana PDF karşılaştırmasında seçilen alanları nasıl atlayıp temiz bir diff PDF elde edeceğinizi görün.
og_image_alt: Aspose.Pdf for .NET kullanarak dışarıda bırakılan dikdörtgen bölgelerle yan yana PDF karşılaştırmasını gösteren rehber
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET kullanarak belirli alanları yok sayarak PDF'leri karşılaştırın
Bu öğreticide, Aspose.Pdf for .NET ile iki PDF belgesini yan yana karşılaştırırken belirli dikdörtgen bölgeleri analizden hariç tutmayı gösterir. Her dosyada dışlama alanları tanımlanarak oluşturulan diff PDF, yalnızca önemli değişiklikleri vurgular ve ilgili farklara odaklanmayı kolaylaştırır.

---

{{< tutorial-widget sourcePath="pdf/net/document-manipulation/exclude-areas" >}}


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

**Q: Yok sayma bölgelerini tanımlarken `Rectangle` değerleri hangi koordinat sistemini kullanır?**  
A: Koordinatlar, sayfa alt‑sol köşesinden başlayan bir orijine sahip olan point biriminde (inç başına 1/72) ölçülür; bu yüzden ilk iki sayı alt‑sol X/Y, son iki sayı ise üst‑sağ X/Y'dir.

**Q: Aynı belgede birden fazla dikdörtgen alanı yok sayabilir miyim?**  
A: Evet – `ExcludeAreas1` (veya `ExcludeAreas2`) dizisine birden fazla `Aspose.Pdf.Rectangle` nesnesi sağlayın; her dikdörtgen karşılaştırma sırasında bağımsız olarak dışlanacaktır.

**Q: Yok sayma dikdörtgenlerinin her iki PDF'de de aynı olması gerekir mi?**  
A: Hayır. `ExcludeAreas1` birinci PDF'ye, `ExcludeAreas2` ise ikinci PDF'ye uygulanır; böylece her belge için farklı koordinatlar belirtebilirsiniz.

**Q: Bir dikdörtgen sayfa sınırlarının dışına tanımlanırsa ne olur?**  
A: Aspose.Pdf, tamamen sayfa dışına düşen dikdörtgenleri sessizce yok sayar; bunların karşılaştırma sonucuna etkisi yoktur.

**Q: Bir PDF'nin her sayfasında aynı bölgeyi nasıl dışarıda bırakabilirim?**  
A: `ExcludeAreas` dizileri sayfa başına uygulanır, bu yüzden `SideBySidePdfComparer.Compare` metodunu çağırmadan önce aynı `Rectangle` nesnesini her sayfanın koleksiyonuna eklemeniz gerekir (ör. `pdf.Pages` üzerinden döngü kurup diziyi atayın).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}