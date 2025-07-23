# 📚 Dassault Systèmes Doküman Ayıklama ve Yapılandırılmış Veri Elde Etme Projesi

## 🎯 Projenin Amacı
Bu proje, **Dassault Systèmes** platformunda yer alan **yardım, eğitim ve bakım dökümanlarını** (HEP) derleyerek, bunları başlık–içerik yapısına göre ayrıştırmak ve yapılandırılmış bir veri seti oluşturmaktır. Amaç; NLP projelerinde kullanılabilecek anlamlı bir dokümantasyon kaynağı elde etmektir.

## 🧾 Kullanılan Yöntemler

### 1️⃣ PDF Tabanlı İşleme (`model_pdf.ipynb`)
- Platformda yer alan içeriklerin büyük kısmı PDF formatında sunulmaktadır.
- PDF dosyaları manuel olarak indirilmiş, `pdfplumber` kütüphanesi ile işlenmiştir.
- Başlıklar ve içerikler yazı tipi büyüklüğü ve renk değerine göre ayrıştırılmıştır.
- Her başlık, ait olduğu üst başlıkla birlikte gösterilmiştir.  
  **Örnek:**  
Portfolio Planning > 3DConfigurator



### 2️⃣ Web Scraping Tabanlı İşleme (`model.ipynb`)
- PDF olarak sunulmayan bazı içerikler yalnızca HTML formatında bulunmaktadır.
- Bu kısımlar için `selenium` tabanlı scraping yaklaşımı kullanılmıştır.
- Sayfa üzerindeki breadcrumb (konum yolu) ve içerik bölümleri otomatik olarak yakalanmıştır.

> 📌 Web scraping işlemi, sayfa yapısının dinamikliği nedeniyle sınırlı olarak kullanılmış, çoğu veri PDF üzerinden alınmıştır.

## 📥 Veri Toplama Süreci
Proje başlangıcında sayfaları otomatik olarak gezip veri çeken bir scraping otomasyonu uygulanmıştır. Ancak sitenin yapısı bu tür otomasyona uygun olmadığından süreç yavaş ilerlemiş ve eksik veri alınmıştır.  
Bu nedenle, içerikler doğrudan PDF olarak manuel şekilde toplanmıştır. Bu yöntem hem daha hızlı hem de daha eksiksiz sonuç vermiştir.

## 🧠 Veri Yapısının Oluşturulması
Toplanan PDF'ler üzerinde `pdfplumber` ile başlıklar ve içerikler ayrıştırılarak yapılandırılmış bir veri seti oluşturulmuştur:
- Her başlık hem kendi adını hem de ait olduğu üst başlığı içerecek şekilde yapılandırılmıştır.
- Örnek: `Portfolio Planning > 3DConfigurator`
- Başlık–içerik eşleşmeleri, yazı tipi rengi ve büyüklüğüne göre belirlenmiştir.
- Başlıklar arası kalan metin blokları, o başlığa ait `content` alanı olarak eklenmiştir.
- Link barındıran (örn. içindekiler tablosu) başlıklar atlanmıştır.

## ❌ Temizlik Kuralları
- NaN veya yalnızca boşluk içeren içerikler temizlenmiştir.
- Aynı başlık ve içerikten oluşan tekrar eden satırlar ayıklanmıştır.

## 📊 Veri Seti Yapısı

Çıkarılan veri, `final_data.csv` dosyası olarak saklanmıştır. Her satır bir başlık–içerik çiftini temsil eder:

| title                         | content       |
|------------------------------|---------------|
| Portfolio Planning>3DConfigurator | ...metin... |
| Mechanical Design>Part Design | ...metin... |

Veri seti, NLP modelleri, belge sınıflandırıcıları veya arama sistemleri gibi projelerde kullanılmaya uygundur.

## 📈 Proje Sonucu

- Toplam **📄 57376 adet başlık (topic)** çıkarılmıştır.
- Bu başlıklar ve içerikleri, platform dökümantasyonunun büyük bölümünü kapsamaktadır.
- PDF ve HTML kaynakların birlikte işlendiği **hibrit veri elde etme yöntemi** başarıyla uygulanmıştır.

## ⚙️ Gereksinimler

- Python 3.x
- `pdfplumber`
- `pandas`
- (opsiyonel) `selenium` – yalnızca scraping işlemi için gereklidir

## 🗣️ Notlar
- Proje, tam otomasyon yerine manuel PDF toplama ile daha hızlı ve kapsamlı veri elde edilmesini sağlamıştır.
- Web sayfasının dinamik yapısı otomasyonu zorlaştırdığından scraping yalnızca PDF ile alınamayan içerikler için uygulanmıştır.


