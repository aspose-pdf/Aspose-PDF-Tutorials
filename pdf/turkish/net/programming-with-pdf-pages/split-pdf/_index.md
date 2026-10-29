---
title: Aspose.Pdf for .NET Kullanarak PDF'i Onuncu Sayfadan Sonra Böl
weight: 360
limit:
description: Aspose.Pdf for .NET ile bir PDF belgesini onuncu sayfadan hemen sonra bölmek için adım adım kod.
keywords: [pdf split, Aspose.Pdf for .NET, split PDF after page, extract pages from PDF, c# pdf split, pdf pagination]
url: /net/programming-with-pdf-pages/split-pdf/
date: '2026-10-14'
lastmod: '2026-10-14'
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Aspose.Pdf for .NET ile bir PDF belgesini onuncu sayfadan hemen sonra
    bölmek için adım adım kod.
  headline: Aspose.Pdf for .NET Kullanarak PDF'i Onuncu Sayfadan Sonra Böl
  type: TechArticle
- description: Aspose.Pdf for .NET ile bir PDF belgesini onuncu sayfadan hemen sonra
    bölmek için adım adım kod.
  name: Aspose.Pdf for .NET Kullanarak PDF'i Onuncu Sayfadan Sonra Böl
  steps:
  - name: Üst bilgi yorumları örneğin amacını açıklar, tam kodun taşındığını belirtir
      ve güncel kaynağa bir bağlantı sağlar.
    text: Üst bilgi yorumları örneğin amacını açıklar, tam kodun taşındığını belirtir
      ve güncel kaynağa bir bağlantı sağlar.
  - name: Stub satırı hiçbir işlem yapmaz ve yalnızca orijinal URL'nin çalışır durumda
      kalmasını sağlamak için vardır.
    text: Stub satırı hiçbir işlem yapmaz ve yalnızca orijinal URL'nin çalışır durumda
      kalmasını sağlamak için vardır.
  type: HowTo
- questions:
  - answer: Aspose.Pdf bir hata vermez; `Split` yöntemi sadece yeni bir bölüm başlatmak
      için onuncu sayfadan sonra sayfa olmadığı için orijinal belgeyi değişmeden döndürür.
    question: Kaynak PDF on sayfadan daha az sayfaya sahipse ne olur?
  - answer: '`PdfDocument.Split(pageNumber)` metodunu bir `PdfDocument` örneği üzerinde
      çağırırsınız, `pageNumber` olarak `10` geçirerek iki ayrı belge oluşturursunuz.'
    question: PDF'i onuncu sayfada bölmek için hangi sınıf ve yöntem kullanılır?
  - answer: Evet, Aspose.Pdf sonuçtaki bölünmüş belgelerde tüm sayfa‑düzeyi nesneleri
      (yer imleri, açıklamalar, form alanları vb.) korur ve bunları kaynak oldukları
      sayfalara bağlı tutar.
    question: Yer imleri, açıklamalar ve form alanları bölündükten sonra orijinal
      sayfalarında kalır mı?
  - answer: '`Split` metodunu çağırdıktan sonra iki `PdfDocument` nesnesi elde edersiniz;
      birincisine `Save("FirstPart.pdf")`, ikincisine `Save("SecondPart.pdf")` çağırarak
      kendiniz farklı dosya adları sağlamalısınız.'
    question: Bölünme ile oluşturulan iki parçanın çıktı dosyalarını nasıl adlandırmalıyım?
  type: FAQPage
images:
- /net/programming-with-pdf-pages/split-pdf/og-image.png
og_title: Sayfa 10'dan sonra PDF'i böl
og_description: Aspose.Pdf for .NET kullanarak bir PDF'i sayfa 10'da bölmek için hızlı öğretici.
og_image_alt: Aspose.Pdf for .NET kullanarak bir PDF'i onuncu sayfadan sonra nasıl bölüneceğini gösteren rehber
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Pdf for .NET Kullanarak PDF'i Onuncu Sayfadan Sonra Böl
Bir PDF'i ayrı belgelere bölmek dağıtım ve işleme sürecini basitleştirebilir. Bu öğretici, Aspose.Pdf for .NET kullanarak bir PDF'i onuncu sayfadan hemen sonra bölmeyi, iki ayrı dosya oluşturmayı adım adım gösterir. İlk on sayfayı ve kalan sayfaları birkaç satır C# kodu ile çıkarmak için adım adım kodu izleyin.

---

{{< tutorial-widget sourcePath="pdf/net/programming-with-pdf-pages/split-pdf" >}}


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

**Q: Kaynak PDF on sayfadan daha az sayfaya sahipse ne olur?**  
A: Aspose.Pdf bir hata vermez; `Split` yöntemi sadece yeni bir bölüm başlatmak için onuncu sayfadan sonra sayfa olmadığı için orijinal belgeyi değişmeden döndürür.

**Q: PDF'i onuncu sayfada bölmek için hangi sınıf ve yöntem kullanılır?**  
A: `PdfDocument.Split(pageNumber)` metodunu bir `PdfDocument` örneği üzerinde çağırırsınız, `pageNumber` olarak `10` geçirerek iki ayrı belge oluşturursunuz.

**Q: Yer imleri, açıklamalar ve form alanları bölündükten sonra orijinal sayfalarında kalır mı?**  
A: Evet, Aspose.Pdf sonuçtaki bölünmüş belgelerde tüm sayfa‑düzeyi nesneleri (yer imleri, açıklamalar, form alanları vb.) korur ve bunları kaynak oldukları sayfalara bağlı tutar.

**Q: Bölünme ile oluşturulan iki parçanın çıktı dosyalarını nasıl adlandırmalıyım?**  
A: `Split` metodunu çağırdıktan sonra iki `PdfDocument` nesnesi elde edersiniz; birincisine `Save("FirstPart.pdf")`, ikincisine `Save("SecondPart.pdf")` çağırarak kendiniz farklı dosya adları sağlamalısınız.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}


{{< blocks/products/products-backtop-button >}}