---
"date": "2025-04-10"
"description": "TrueType (TTF) ve Web Açık Yazı Tipi Biçimi'ndeki (WOFF) yazı tiplerini koruyarak Aspose.PDF for .NET kullanarak PDF'leri HTML'ye nasıl dönüştüreceğinizi öğrenin. Kod örnekleriyle adım adım kılavuz."
"title": "PDF'yi Aspose.PDF for .NET ile HTML'ye dönüştürün&#58; TTF ve WOFF Formatlarındaki Yazı Tiplerini Koruyun"
"url": "/tr/net/conversion-export/convert-pdf-html-aspose-net-truetype-woff/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# PDF'yi Aspose.PDF for .NET ile HTML'ye dönüştürün: TTF ve WOFF Formatlarındaki Yazı Tiplerini Koruyun

## giriiş
PDF belgelerinizi HTML'ye dönüştürürken orijinal düzeni ve yazı tipi bütünlüğünü korumakta zorluk mu çekiyorsunuz? PDF'leri yazı tiplerini koruyarak dönüştürmek zor olabilir, ancak olmak zorunda değil. **.NET için Aspose.PDF**yazı tiplerinin TrueType (TTF) veya Web Open Font Format (WOFF) olarak korunduğundan emin olarak PDF dosyalarını zahmetsizce HTML formatına dönüştürebilirsiniz. Bu kılavuz sizi adım adım süreçte yönlendirecektir.

Bu eğitimde şunları ele alacağız:
- PDF'leri HTML'ye dönüştürürken yazı tipleri TTF olarak nasıl kaydedilir
- Yazı tiplerini WOFF olarak kaydetmek için dönüştürmenizi yapılandırma
- Dönüştürme sırasında tüm formatlardaki yazı tiplerini kaydetme

Bu makalenin sonunda, Aspose.PDF for .NET'i kullanarak font dönüşümlerini etkili bir şekilde yönetme konusunda kapsamlı bir anlayışa sahip olacaksınız. Başlamadan önce gereken ön koşullara bir göz atalım.

## Ön koşullar
PDF'leri Aspose.PDF ile HTML'ye dönüştürmeye başlamadan önce, şu gereksinimleri karşıladığınızdan emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
- **.NET için Aspose.PDF**: Bu kütüphane .NET uygulamalarında PDF dosyalarının işlenmesi için gereklidir.
- **.NET Framework veya .NET Core/5+**: Geliştirme ortamınızın bu çerçeveleri desteklediğinden emin olun.

### Çevre Kurulum Gereksinimleri
Geliştirme ortamınızın (örneğin, Visual Studio) Aspose.PDF kitaplığıyla çalışacak şekilde ayarlandığından emin olun. Şunlara ihtiyacınız olacak:
- .NET Framework veya .NET Core/5+'da oluşturulmuş bir proje
- Kütüphaneleri yüklemek için NuGet Paket Yöneticisine erişim

### Bilgi Önkoşulları
C# konusunda temel bir anlayışa ve .NET'te dosya işleme konusunda aşinalığa sahip olmak faydalı olacaktır.

## Aspose.PDF'yi .NET için Kurma
Başlamak için Aspose.PDF kütüphanesini yüklemeniz gerekir. Bunu farklı paket yöneticileri aracılığıyla yapabilirsiniz:

**.NET Komut Satırı Arayüzü:**
```bash
dotnet add package Aspose.PDF
```

**Paket Yöneticisi Konsolu:**
```powershell
Install-Package Aspose.PDF
```

**NuGet Paket Yöneticisi Kullanıcı Arayüzü:**
"Aspose.PDF" dosyasını arayın ve en son sürümü yükleyin.

### Lisans Edinimi
Geçici bir lisans edinebilir veya Aspose'dan tam bir lisans satın alabilirsiniz. Ücretsiz deneme, tüm özellikleri kısıtlama olmadan keşfetmenizi sağlar ve bu da onu ilk değerlendirmeler için ideal hale getirir. Ortamınızı bir lisansla nasıl kuracağınız aşağıda açıklanmıştır:
1. Bir talepte bulunun [geçici lisans](https://purchase.aspose.com/temporary-license/).
2. Herhangi bir işlem yapmadan önce aşağıdaki kod parçacığını kullanarak lisansı uygulamanıza uygulayın:

```csharp
Aspose.Pdf.License license = new Aspose.Pdf.License();
license.SetLicense("Path to your License File");
```

## Uygulama Kılavuzu
Uygulamayı üç temel özelliğe ayıralım: yazı tiplerini TTF, WOFF ve tüm formatlarda kaydetme.

### Yazı Tiplerini TTF Olarak Kaydet
**Genel bakış**
Bu özellik, PDF belgesini HTML'ye dönüştürürken yazı tiplerini TrueType Format'ta (TTF) kaydetmenize olanak tanır. Bu, dönüştürme sırasında yazı tiplerinizin görsel bütünlüğünün korunmasını sağlar.

#### Adım Adım Uygulama
1. **Belgeyi ve Seçenekleri Başlat:**
   Aspose.PDF'i kullanarak PDF belgenizi yükleyerek başlayın `Document` sınıf ve kurulum `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   string outFile = Path.GetFullPath(dataDir + "/36192_out.html");
   Document doc = new Document(dataDir + "/input.pdf");

   HtmlSaveOptions saveOptions = new HtmlSaveOptions();
   ```

2. **Kaydetme Seçeneklerini Yapılandırın:**
   Düzeni korumak için gerekli seçenekleri ayarlayın ve yazı tipi kaydetme modunu belirtin.

   ```csharp
   saveOptions.FixedLayout = true; // Orijinal PDF düzenini koru
   saveOptions.SplitIntoPages = false; // Birden fazla HTML dosyasına bölmeyin
   saveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsTTF;
   ```

3. **Çıktı Dizinini Hazırla:**
   Bağlantılı yazı tipi dosyalarını depolamak için çıkış dizininin hazır olduğundan emin olun.

   ```csharp
   string linkedFilesFolder = Path.GetDirectoryName(outFile) + "/36192_files";
   if (Directory.Exists(linkedFilesFolder))
   {
       Directory.Delete(linkedFilesFolder, true); // Mevcut dosyaları temizle
   }
   ```

4. **Belgeyi Kaydedin:**
   Son olarak belgenizi belirtilen seçeneklerle kaydedin.

   ```csharp
doc.Save(çıkanDosya, kaydetmeSeçenekleri);
```

### Save Fonts as WOFF
**Overview**
Configuring Aspose.PDF to save fonts in Web Open Font Format (WOFF) is beneficial for web optimization, reducing font file sizes while maintaining quality.

#### Step-by-Step Implementation
1. **Configure Save Options:**
   Initialize `HtmlSaveOptions` and set the font saving mode to WOFF.

   ```csharp
   HtmlSaveOptions woffSaveOptions = new HtmlSaveOptions();
   woffSaveOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.AlwaysSaveAsWOFF;
   ```

2. **Kaydetme Seçeneklerini Uygula:**
   Belgenizi kaydederken TTF yöntemine benzer şekilde bu seçenekleri kullanın.

### Tüm Formatlarda Yazı Tiplerini Kaydet
**Genel bakış**
Maksimum uyumluluk ve esnekliği sağlamak için, dönüştürme sırasında yazı tiplerini tüm kullanılabilir biçimlerde kaydetmek isteyebilirsiniz.

#### Adım Adım Uygulama
1. **Belgeyi ve Seçenekleri Başlat:**
   PDF belgesini yükleyin ve yapılandırın `HtmlSaveOptions`.

   ```csharp
   string dataDir = "YOUR_DOCUMENT_DIRECTORY";
   Document doc = new Document(dataDir + "/input.pdf");
   HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
   ```

2. **Kaydetme Seçeneklerini Yapılandırın:**
   Tüm yazı tiplerini kaydetmek ve düzeni korumak için seçenekleri ayarlayın.

   ```csharp
   htmlOptions.FixedLayout = true;
   htmlOptions.RasterImagesSavingMode = HtmlSaveOptions.RasterImagesSavingModes.AsExternalPngFilesReferencedViaSvg;
   htmlOptions.FontSavingMode = HtmlSaveOptions.FontSavingModes.SaveInAllFormats;
   ```

3. **Belgeyi Kaydedin:**
   Belgenizi bu ayarlarla kaydedin.

   ```csharp
doc.Save(dataDir + "/ThreeSetFonts_out.html", htmlSeçenekleri);
```

## Practical Applications
Converting PDFs to HTML with font preservation has numerous real-world applications:
1. **Web Publishing**: Ensure that documents retain their original styling when published online.
2. **Content Portability**: Easily move content between desktop and web environments without loss of formatting.
3. **Document Archiving**: Maintain document integrity during long-term storage or migration.

Integration possibilities include embedding these conversions into CMS systems, automated reporting tools, or digital libraries for seamless font management across platforms.

## Performance Considerations
When using Aspose.PDF for .NET, consider the following tips to optimize performance:
- **Memory Management**: Dispose of objects properly and utilize `using` statements where applicable.
- **Batch Processing**: Process documents in batches if dealing with large volumes to prevent memory overflow.
- **Resource Optimization**: Configure options like image compression and font subsetting to reduce file sizes.

## Conclusion
We've explored how to convert PDFs to HTML while preserving fonts using Aspose.PDF for .NET. Whether saving fonts as TTF, WOFF, or all formats, these techniques ensure your documents maintain their original design and readability in web environments. 

For further exploration, consider diving into Aspose's extensive documentation or experimenting with additional conversion features offered by the library.

## FAQ Section
1. **What are the benefits of converting PDFs to HTML using Aspose.PDF?**
   - Maintains document layout and font integrity.
   - Facilitates web publishing and content portability.
2. **Can I convert large PDF files efficiently with Aspose.PDF?**
   - Yes, by optimizing memory usage and processing in batches.
3. **How do I handle licensing for Aspose.PDF?**
   - Obtain a temporary or full license from the [Aspose website](https://purchase.aspose.com/buy).
4. **Is it possible to customize font settings during conversion?**
   - Yes, through various `HtmlSaveOptions`.
5. **What are some common issues when converting PDFs and how can I address them?**
   - Common issues include missing fonts or layout discrepancies. Adjusting save options and ensuring proper licensing can help mitigate these problems.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}