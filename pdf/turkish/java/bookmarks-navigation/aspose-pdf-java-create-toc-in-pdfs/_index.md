---
"date": "2025-04-14"
"description": "Java için Aspose.PDF kullanarak PDF dosyalarınıza İçindekiler eklemeyi öğrenin, belge gezinmesini ve profesyonelliği geliştirin. PDF kullanılabilirliğinizi geliştirmek için bu adım adım kılavuzu izleyin."
"title": "Java için Aspose.PDF Kullanarak PDF'lerde İçindekiler Tablosu (TOC) Oluşturma&#58; Bir Geliştiricinin Kılavuzu"
"url": "/tr/java/bookmarks-navigation/aspose-pdf-java-create-toc-in-pdfs/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Java için Aspose.PDF Kullanarak PDF'lerde İçindekiler Tablosu (TOC) Oluşturma: Geliştiricinin Kılavuzu

## giriiş

Özellikle kapsamlı raporlar veya PDF dosyaları olarak depolanan kitaplarla uğraşırken, düzenli ve kolayca gezilebilen bir belge oluşturmak önemlidir. İçindekiler Tablosu (TOC) olmadan, belirli bölümleri bulmak zahmetli hale gelebilir. Bu kılavuz, PDF'leri yönetmek ve düzenlemek için tasarlanmış güçlü bir kitaplık olan Java için Aspose.PDF kullanarak mevcut PDF belgelerinde bir TOC'nin nasıl oluşturulacağını göstererek bu sorunu çözmenize yardımcı olur.

Bu eğitimde şunları öğreneceksiniz:
- Mevcut bir PDF belgesi nasıl yüklenir
- İçindekiler'e ayrılmış yeni bir sayfa ekleniyor
- İçindekiler bilgilerinin başlıklarla ayarlanması
- Belirli sayfalara bağlı İçindekiler girişleri ekleme

Bu adımları izleyerek PDF'nizin kullanılabilirliğini ve profesyonelliğini artıracaksınız. Başlamadan önce gereken ön koşullara bir göz atalım.

## Ön koşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1. **Gerekli Kütüphaneler**Java için Aspose.PDF'in 25.3 veya sonraki sürümüne ihtiyacınız olacak.
2. **Çevre Kurulumu**:Bağımlılık yönetimi için geliştirme ortamınızın Maven veya Gradle'ı desteklediğinden emin olun.
3. **Bilgi Önkoşulları**: Temel Java programlama bilgisine sahip olmak ve PDF yapılarını anlamak.

## Java için Aspose.PDF Kurulumu

### Kurulum Bilgileri

Java için Aspose.PDF'yi kullanmak için projenize bağımlılık olarak ekleyin:

**Usta:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```

### Lisans Edinimi

Aspose.PDF for Java'yı kullanmadan önce bir lisans edinmelisiniz. Ücretsiz denemeyle başlayabilir veya kütüphanenin tüm özelliklerini değerlendirmek için geçici bir lisans talep edebilirsiniz. Üretim kullanımı için bir lisans satın almayı düşünün.

### Temel Başlatma ve Kurulum

Bağımlılığı ekledikten sonra, kodunuzun başına gerekli sınıfları ekleyerek Aspose.PDF'yi Java projenizde başlatın:

```java
import com.aspose.pdf.Document;
```

## Uygulama Kılavuzu

Bu bölüm, etkili bir İçindekiler tablosu oluşturmanıza yardımcı olmak için her özelliği yönetilebilir adımlara ayırır.

### Özellik 1: Mevcut bir PDF Belgesini Yükle

**Genel bakış**Değiştirmek istediğiniz bir PDF dosyasını yükleyerek başlayın. Bu adım, belgeyi daha fazla düzenleme için başlattığı için önemlidir.

**Uygulama Adımları**

- **Adım 1**: Gerekli sınıfı içe aktarın ve belge dizininizi ayarlayın.
  
```java
import com.aspose.pdf.Document;

String dataDir = "YOUR_DOCUMENT_DIRECTORY";
String sourceFilePath = dataDir + "/source.pdf";
```

- **Adım 2**: PDF belgesini kullanarak yükleyin `Document` sınıf.

```java
// Belgeyi belirtilen yoldan yükleyin
document doc = new Document(sourceFilePath);
```

*Açıklama*: Bu kod parçacığı belirtilen PDF dosyasını açar ve içindekiler tablosu ekleme gibi sonraki işlemler için hazırlar.

### Özellik 2: İçindekiler için Yeni Bir Sayfa Ekle

**Genel bakış**:Belgenizin başına özel bir sayfa eklemek, İçindekiler tablosuna kolayca erişilebilmesini sağlar.

**Uygulama Adımları**

- **Adım 1**: Sayfaları yönetmek için gereken ek sınıfları içe aktarın.
  
```java
import com.aspose.pdf.Page;
```

- **Adım 2**: İçindekiler için başlangıç olarak yeni bir sayfa ekleyin.

```java
Page tocPage = doc.getPages().insert(1);
```

*Açıklama*: Bu komut ilk konuma İçindekiler sayfanız olarak hizmet edecek boş bir sayfa ekler.

### Özellik 3: İçindekiler Bilgilerini Oluşturun ve Ayarlayın

**Genel bakış**:İçindekiler tablonuzun görünürlüğünü ve profesyonelliğini artırmak için bir başlık tanımlayın ve ayarlayın.

**Uygulama Adımları**

- **Adım 1**: Metin düzenleme için gerekli sınıfları içe aktarın.
  
```java
import com.aspose.pdf.TextFragment;
import com.aspose.pdf.FontStyles;
import com.aspose.pdf.TocInfo;
```

- **Adım 2**: Bir tane oluştur `TextFragment` İçindekiler başlığı olarak hizmet etmek için.

```java
TextFragment title = new TextFragment("Table Of Contents");
title.getTextState().setFontSize(20);
title.getTextState().setFontStyle(FontStyles.Bold);

TocInfo tocInfo = new TocInfo();
tocInfo.setTitle(title);
tocPage.setTocInfo(tocInfo);
```

*Açıklama*: Bu kod parçacığı bir `TextFragment` İçindekiler başlığı için ve onu belirgin hale getirmek için stil uygular.

### Özellik 4: Belgeye İçindekiler Girişleri Ekleme

**Genel bakış**: İçindekiler tablonuzu belge içindeki farklı bölümlere veya sayfalara giden bağlantılarla doldurun.

**Uygulama Adımları**

- **Adım 1**: Başlık oluşturmak için gerekli sınıfları içe aktarın.
  
```java
import com.aspose.pdf.Heading;
import com.aspose.pdf.TextSegment;
```

- **Adım 2**: Tanımlanmış başlıklar arasında dolaşın ve oluşturun `Heading` Bağlantılı nesneler.

```java
String[] titles = {"First page\

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}