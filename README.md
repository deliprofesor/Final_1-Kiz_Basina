# ✈️ Havayolu Yolcu Memnuniyeti Analizi  

![image](https://github.com/user-attachments/assets/160774c7-84f8-4188-8dbb-c5b3d22d235c)

## Final Projesi – Veri Ön İşleme & Keşifsel Veri Analizi (EDA)

Bu proje, bir havayolu şirketinin yolcu verileri üzerinden müşteri memnuniyetini etkileyen faktörlerin belirlenmesi amacıyla yapılmıştır. Çalışma kapsamında veri seti detaylı bir şekilde analiz edilerek, memnuniyet düzeyine etki eden demografik ve seyahat odaklı değişkenler incelenmiştir.

---

##  Proje Amacı

Projenin temel amacı, yolcu memnuniyetini etkileyen değişkenleri anlamak ve bu doğrultuda havayolu şirketine stratejik içgörüler sunmaktır.  

Bu kapsamda:

- Veriyi tanıma  
- Eksik ve aykırı değer analizi  
- Sayısal ve kategorik değişkenlerin incelenmesi  
- Segmentasyon analizi  

gibi temel **Keşifsel Veri Analizi (Exploratory Data Analysis - EDA)** adımları gerçekleştirilmiştir.

---

##  Kullanılan Kütüphaneler

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

##  Veri Seti Seçimi ve Tanımı

Proje için seçilen veri seti `train.csv`, toplam **103.904 satır** ve **25 sütundan** oluşmaktadır.  
Veri seti, yolcu demografik bilgileri, uçuş tipi, hizmet kalitesi değerlendirmeleri, uçuş gecikmeleri ve hedef değişken olan memnuniyet (`satisfaction`) bilgisini içermektedir.

- **Hangi faktörlerin memnun veya memnuniyetsiz yolcularla yüksek korelasyona sahip olduğu,**
- **Yolcu memnuniyetinin bu faktörler temelinde tahmin edilip edilemeyeceğidir.**

## Veri Seti Özellikleri

| Özellik                       | Açıklama                                                          |
|------------------------------|------------------------------------------------------------------|
| **Gender (Cinsiyet)**         | Yolcuların cinsiyeti (Kadın, Erkek)                             |
| **Customer Type (Müşteri Türü)** | Müşteri türü (Sadık müşteri, Sadık olmayan müşteri)            |
| **Age (Yaş)**                 | Yolcuların gerçek yaşı                                           |
| **Type of Travel (Seyahat Türü)** | Uçuş amacı (Kişisel seyahat, İş seyahati)                     |
| **Class (Sınıf)**             | Yolcunun uçtuğu sınıf (Business, Ekonomi, Ekonomi Plus)          |
| **Flight Distance (Uçuş Mesafesi)** | Yolculuğun uçuş mesafesi                                    |
| **Inflight wifi service (Uçuş içi wifi hizmeti)** | Wifi hizmeti memnuniyet seviyesi (0: Uygulanamaz; 1-5 arası) |
| **Departure/Arrival time convenient (Kalkış/Varış zamanı uygunluğu)** | Zaman uygunluğu memnuniyeti                    |
| **Ease of Online booking (Online rezervasyon kolaylığı)** | Online rezervasyon memnuniyeti                   |
| **Gate location (Kapı konumu)** | Kapı konumu memnuniyeti                                      |
| **Food and drink (Yiyecek ve içecek)** | Yiyecek ve içecek memnuniyeti                             |
| **Online boarding (Online biniş)** | Online biniş memnuniyeti                                   |
| **Seat comfort (Koltuk konforu)** | Koltuk konforu memnuniyeti                                  |
| **Inflight entertainment (Uçuş içi eğlence)** | Uçuş içi eğlence memnuniyeti                             |
| **On-board service (Uçuş içi servis)** | Uçuş içi servis memnuniyeti                               |
| **Leg room service (Bacak mesafesi servisi)** | Bacak mesafesi memnuniyeti                              |
| **Baggage handling (Bagaj işlemleri)** | Bagaj işlemleri memnuniyeti                               |
| **Check-in service (Check-in servisi)** | Check-in servisi memnuniyeti                              |
| **Inflight service (Uçuş içi hizmet)** | Uçuş içi hizmet memnuniyeti                               |
| **Cleanliness (Temizlik)**    | Temizlik memnuniyeti                                           |
| **Departure Delay in Minutes (Kalkış gecikmesi dakika olarak)** | Kalkış gecikme süresi (dakika)                    |
| **Arrival Delay in Minutes (Varış gecikmesi dakika olarak)** | Varış gecikme süresi (dakika)                      |
| **Satisfaction (Memnuniyet)** | Havayolu memnuniyet seviyesi (Memnun, Nötr, Memnuniyetsiz)      |


## İstatistiksel Özet – Sayısal Değişkenler

Sayısal değişkenler üzerinden merkezi eğilim (ortalama, medyan), dağılım (standart sapma), minimum ve maksimum gibi temel istatistikler aşağıda sunulmuştur.


Korelasyon Matrisi Analizi
Aşağıda uçuş deneyimi verisindeki değişkenlerin korelasyon ilişkileri incelenmiştir. Korelasyon katsayısı [-1, 1] aralığında olup, 1 mükemmel pozitif, -1 mükemmel negatif ilişkiyi ifade eder.

![image](https://github.com/user-attachments/assets/ca5c265a-b6bb-449c-a148-bfa79e2cba6e)

Öne Çıkan Bulgular
Departure Delay in Minutes ile Arrival Delay in Minutes arasında çok yüksek pozitif korelasyon bulunmaktadır: 0.96.

Bu, kalkış gecikmesinin varış gecikmesini doğrudan etkilediğini göstermektedir.
Inflight wifi service ile aşağıdaki değişkenler arasında güçlü pozitif ilişkiler vardır:

Ease of Online booking (0.72)
Departure/Arrival time convenient (0.34)
Gate location (0.34)
Hizmet kalitesi değişkenleri arasında yüksek korelasyonlar görülmektedir:

Food and drink ↔ Seat comfort: 0.57
Food and drink ↔ Inflight entertainment: 0.62
Food and drink ↔ Cleanliness: 0.66
Seat comfort ↔ Inflight entertainment: 0.61
Inflight entertainment ↔ Cleanliness: 0.69
Age ve Flight Distance arasında zayıf pozitif bir korelasyon vardır: 0.10.

Yaş ile hizmet kalitesi veya gecikme değişkenleri arasında anlamlı bir ilişki gözlemlenmemiştir.

Genel Değerlendirme
Hizmet kalitesi unsurları birbiriyle pozitif ilişki göstermektedir, bu da yolcuların genel memnuniyetini yansıtabilir.
Gecikmeler (kalkış ve varış) birbirine oldukça bağlıdır.
Online hizmetlere ilişkin değişkenler (wifi, online rezervasyon kolaylığı, gate konumu) birbirleriyle ilişkilidir.
Yaş ve uçuş mesafesi, diğer değişkenlerden nispeten bağımsızdır.

## Eksik Değer Analizi
Veri setindeki eksik değerler aşağıda sayısal ve yüzdesel olarak özetlenmiştir. Eksik verinin yalnızca bir sütunda ve düşük oranla (yaklaşık %0.30) bulunduğu görülmektedir.
Veri setinde yalnızca Arrival Delay in Minutes değişkeninde eksik gözlemler bulunmaktadır. Toplam 310 eksik değer, tüm veri setinin yaklaşık %0.3’üne karşılık gelmektedir.

Bu değişken, uçuş memnuniyeti açısından doğrudan etkili olan bir özelliktir. Eksik verilerin doğrudan silinmesi, potansiyel bilgi kaybına ve bazı gruplarda temsil eksikliğine neden olabilir. Bu nedenle silmek yerine anlamlı bir şekilde doldurulması tercih edilmiştir.

Seçilen Yöntem: Segment Bazlı Medyan ile Doldurma
Eksik veriler, yolcunun seyahat tipi (Type of Travel) ve uçuş sınıfı (Class) bilgileri dikkate alınarak segmentlere ayrılmış, her grup için medyan gecikme süresi hesaplanarak eksik değerler bu şekilde doldurulmuştur.

Bu yöntem sayesinde:

Her müşteri segmenti için karakteristik bir gecikme süresi korunmuş olur.
Aykırı değerlerin etkisi en aza indirilir (çünkü medyan kullanılmıştır).
Gecikme ile memnuniyet arasındaki ilişki korunmuş olur.

Doldurma öncesi eksik değer sayısı: 310
Doldurma sonrası eksik değer sayısı: 0

### Eksik Değerler Doldurulmuş Yeni Veri Seti (train_filled)

Orijinal veri seti (`train`) korunarak, eksik değerleri doldurulmuş yeni bir kopya (`train_filled`) oluşturulmuştur.

Bu yaklaşım sayesinde:
- Orijinal veri üzerinde herhangi bir değişiklik yapılmaz,
- Eksik değerlerin doldurulmasının veri yapısına etkisi açıkça karşılaştırılabilir,
- Görselleştirme ve analizlerde kafa karışıklığı önlenmiş olur.

## Aykırı Değer (Outlier) Analizi

Aykırı değerler, veri analizinde model performansını ve istatistiksel sonuçları bozabileceği için dikkatle incelenmelidir.  
Bu bölümde:
- Boxplot grafiklerle görsel analiz yapıldı.
- IQR yöntemiyle sayısal olarak aykırı değerler belirlendi.


### Aykırı Değer Analizi (IQR Yöntemi)

![image](https://github.com/user-attachments/assets/ad110545-feed-4db5-a1f1-b5799300e8bd)

Sayısal değişkenlerde aykırı değer analizi, IQR (Interquartile Range) yöntemine göre gerçekleştirilmiştir. Aşağıdaki tabloda, her değişken için aykırı değer sayısı ve toplam veri içindeki oranı yer almaktadır:

| Değişken                     | Toplam Gözlem | Aykırı Değer Sayısı | Aykırı Oranı (%) |
|-----------------------------|----------------|----------------------|------------------|
| **Age**                     | 103,904        | 0                    | 0.00%            |
| **Flight Distance**         | 103,904        | 2,291                | 2.20%            |
| **Departure Delay (Min.)**  | 103,904        | 14,529               | 13.98%           |
| **Arrival Delay (Min.)**    | 103,904        | 13,954               | 13.43%           |

####  Yorumlar:
- **Age** değişkeninde aykırı değer bulunmamaktadır, bu değişken oldukça dengeli bir dağılıma sahiptir.
- **Flight Distance** için %2.2 oranında aykırı gözlem mevcuttur, bu oran kabul edilebilir düzeydedir.
- **Departure Delay** ve **Arrival Delay** değişkenlerinde ise yaklaşık **%14 civarında yüksek oranlarda aykırı değer** mevcuttur.

Bu durum, uçuş gecikmelerinin bazı uçuşlarda çok ekstrem değerlere ulaşabildiğini göstermektedir. Ancak bu aykırı değerler, veri girişi hatası değil, uçuşların doğasında olan yüksek gecikmeler olabilir. Bu nedenle bu değerler doğrudan silinmemelidir.

### Gözlemler (Boxplot Yorumu)

- `Age` değişkeni genelde normal dağılmış, çok az aykırı değer var.
- `Flight Distance` değişkeninde özellikle 3000 km ve üzeri mesafelerde aykırılıklar var.
- `Departure` ve `Arrival Delay` değişkenlerinde **çok sayıda yüksek gecikme** outlier olarak görülmektedir.

### Aykırı Değerlerle Ne Yapılmalı?

- `Flight Distance`: Üst limitteki outlier’lar uçuş çeşitliliğini temsil ediyor olabilir, silinmesi önerilmez.
- `Delay` (gecikme): Çok büyük değerler (>1000 dakika) aykırı olabilir, fakat uçuş iptali/aksama gibi önemli durumları da temsil ediyor olabilir.

**Yöntem önerisi:**
- Aykırı değerleri silmek yerine, `is_outlier` gibi bir işaretleyici sütun eklemek.
- Model eğitiminde outlier’lar için özel önlem almak.

##  Görselleştirme

Veri görselleştirme, değişkenlerin dağılımını ve değişkenler arası ilişkileri keşfetmek için kritik öneme sahiptir.  



Bu bölümde:

- Sayısal değişkenlerin histogram ve yoğunluk grafikleri (KDE)
  
  ![image](https://github.com/user-attachments/assets/9c011056-0f16-4a98-bb80-54c73f5fad43)
  
- Kategorik değişkenlerin sütun ve pasta grafikleri
  
  ![image](https://github.com/user-attachments/assets/ea5eca30-d610-44c4-b8c2-e21e606eafc1)


## Memnuniyetsiz Yolcuların Analizi

Uçuş deneyimi verilerinde **"neutral or dissatisfied"** olarak işaretlenmiş yolcular analiz edilmiştir.  
Amacımız, bu yolcuların neden memnun olmadığını tespit etmek ve hizmet kalitesine dair iyileştirme yapılabilecek noktaları belirlemektir.

Analiz kapsamında şu adımlar izlenmiştir:

- Memnuniyetsiz yolcuların hizmet kalite puanları ile memnun yolcuların puanları karşılaştırılmıştır.
- Gecikme süreleri incelenmiş, logaritmik dönüşüm ile dağılım daha net şekilde analiz edilmiştir.
- Cinsiyet, müşteri türü, seyahat tipi ve uçuş sınıfı gibi kategorik değişkenlerin memnuniyetsizlikle ilişkisi incelenmiştir.


## Bulgular

###  Hizmet Kalitesi Farkları

Aşağıdaki tabloda, memnun ve memnun olmayan yolcuların hizmet kalitesine verdikleri ortalama puanlar karşılaştırılmıştır:

| Hizmet Kalitesi Özelliği      | Memnun Değil | Memnun | Fark |
|-------------------------------|--------------|--------|------|
| Online boarding               | 2.66         | 4.03   | **1.37** |
| Inflight entertainment        | 2.89         | 3.96   | **1.07** |
| Seat comfort                  | 3.04         | 3.97   | 0.93 |
| On-board service              | 3.02         | 3.86   | 0.84 |
| Leg room service              | 2.99         | 3.82   | 0.83 |
| Cleanliness                   | 2.94         | 3.74   | 0.81 |
| Inflight wifi service         | 2.40         | 3.16   | 0.76 |
| Checkin service               | 3.04         | 3.65   | 0.60 |
| Baggage handling              | 3.38         | 3.97   | 0.59 |
| Inflight service              | 3.39         | 3.97   | 0.58 |
| Food and drink                | 2.96         | 3.52   | 0.56 |

**En belirgin fark**, `Online boarding`, `Inflight entertainment` ve `Seat comfort` değişkenlerinde gözlemlenmiştir.  
Bu hizmet alanlarının iyileştirilmesi, memnuniyetsizlik oranlarını azaltabilir.

###  Kalkış Gecikmeleri

![image](https://github.com/user-attachments/assets/6248a085-ad31-4521-9f48-afc9997eee4d)


Kalkış gecikmesi değişkeni sağa çarpık dağıldığı için logaritmik dönüşüm uygulanmıştır.  
Analiz sonucunda:

- Memnuniyetsiz yolcuların büyük bir kısmı, özellikle **yüksek gecikmelere maruz kalan** yolculardan oluşmaktadır.
- Gecikmeler, dolaylı olarak yolcu deneyimini ve memnuniyetini olumsuz etkilemektedir.

###  Kategorik Özelliklere Göre Dağılım

![image](https://github.com/user-attachments/assets/1ac78308-82e8-41cc-8bc0-1f41b59fe255)

Memnuniyetsiz yolcuların demografik ve seyahat bilgileri şu şekildedir:

- **Müşteri Türü:** Yeni müşteriler, sadık müşterilere kıyasla daha fazla memnuniyetsizlik göstermiştir.
- **Uçuş Sınıfı:** Ekonomi sınıfı yolcular arasında memnuniyetsizlik daha yaygındır.
- **Seyahat Türü:** İş seyahati yapan yolcular, tatil amaçlı seyahat edenlere göre daha yüksek memnuniyetsizlik oranına sahiptir.
- **Cinsiyet:** Memnuniyetsizlik oranı cinsiyetler arasında dengelidir ancak hafif farklar gözlemlenmiştir.

##  Sonuç

Bu analiz, memnuniyetsiz yolcuların büyük ölçüde:

- **düşük hizmet kalitesi puanları verdiği,**
- **yüksek gecikmelere maruz kaldığı** ve
- **özellikle ekonomi sınıfında, iş seyahati yapan ve yeni müşteri grubunda yoğunlaştığı**

göstermektedir.

**Memnuniyetsizlikleri Azaltma Yolları:**

- Online hizmetlerin (boarding, check-in) ve uçak içi konforun iyileştirilmesi,
- Gecikmeleri azaltmaya yönelik operasyonel iyileştirmeler,
- Ekonomi sınıfında sunulan hizmetlerde kalite artışı,

müşteri memnuniyetini artırmak adına kritik önem taşımaktadır.

# Memnuniyet Analizi 

![image](https://github.com/user-attachments/assets/2818514f-0e80-437f-a311-bf2b208b85b0)

Uçuş deneyiminden memnun kalan yolcuların profili detaylı olarak incelenmiştir. Memnuniyet düzeyini artıran hizmet kalitesi faktörleri ve yolcu demografik özellikleri analiz edilmiştir. Özellikle, yolcuların hangi hizmetlerden daha olumlu puanlar verdiği ve gecikmelerin memnuniyet üzerindeki etkisi değerlendirilmiştir.

Analiz sayesinde, yolcu memnuniyetini artırmak için öncelikli iyileştirme alanları belirlenmiş ve güçlü yönler ortaya konmuştur. Bu bilgiler, hava yolu şirketlerinin müşteri deneyimini geliştirmesine ve sadık müşteri kitlesini büyütmesine katkı sağlayacaktır.

###  Kategorik Değişken Dağılımları

![image](https://github.com/user-attachments/assets/305c699d-056f-48b0-aede-387bd326ab44)


| Değişken       | Kategori           | Adet   | Yüzde (%) |
|----------------|--------------------|--------|-----------|
| **Gender**     | Female             | 22,534 | 50.05     |
|                | Male               | 22,491 | 49.95     |
| **Customer Type** | Loyal Customer      | 40,533 | 90.02     |
|                | Disloyal Customer   | 4,492  | 9.98      |
| **Type of Travel** | Business travel     | 41,746 | 92.72     |
|                | Personal Travel     | 3,279  | 7.28      |
| **Class**      | Business           | 34,480 | 76.58     |
|                | Eco                | 8,701  | 19.32     |
|                | Eco Plus            | 1,844  | 4.10      |

**Özet:**

- Memnun yolcular çoğunlukla cinsiyet açısından dengeli (yaklaşık %50-50).
- Sadık müşterilerin memnuniyet oranı oldukça yüksek (%90).
- İş seyahati yapan yolcular ve Business sınıfındaki yolcular memnuniyet oranı en yüksek gruplar.
- Hizmet kalitesi puanları genel olarak yüksek; özellikle online boarding, koltuk konforu ve bagaj işlemleri ön planda.
- Gecikmeler ortalama düşük, ancak maksimum değerlerde aşırı uçlar mevcut.

## Yolcu Profili ve Segmentasyonu

![image](https://github.com/user-attachments/assets/ce1074c5-e656-4bb1-af71-6abaacb74c80)

# Yolcu Segmentasyon Tablosu

Aşağıdaki tablo, yolcuların **Müşteri Türü** (Sadık / Sadık Olmayan), **Cinsiyet**, **Seyahat Türü** (İş / Kişisel), ve **Seyahat Sınıfı** (Business, Eco, Eco Plus) bazında sayılarını göstermektedir.

| Müşteri Türü     | Cinsiyet | Seyahat Türü      | Business | Eco   | Eco Plus |
|------------------|----------|-------------------|----------|-------|----------|
| Sadık Müşteri    | Kadın    | İş Seyahati       | 20,047   | 4,738 | 1,559    |
| Sadık Müşteri    | Kadın    | Kişisel Seyahat   | 1,068    | 13,225| -        |
| Sadık Müşteri    | Erkek    | İş Seyahati       | 20,116   | 4,758 | 1,620    |
| Sadık Müşteri    | Erkek    | Kişisel Seyahat   | 1,078    | -     | -        |
| Sadık Olmayan    | Kadın    | İş Seyahati       | 3,805    | 5,817 | 562      |
| Sadık Olmayan    | Kadın    | Kişisel Seyahat   | 7        | 78    | -        |
| Sadık Olmayan    | Erkek    | İş Seyahati       | 3,540    | 4,944 | 149      |
| Sadık Olmayan    | Erkek    | Kişisel Seyahat   | 4        | -     | -        |

> *Not:* Eksik veya sıfır olan hücreler tabloda boş bırakılmıştır.

![image](https://github.com/user-attachments/assets/e2711ae4-f6ad-4f69-af5a-cc5688522fd3)


### Değerlendirme

- Sadık müşteriler çoğunlukla **iş seyahati** yapan ve **business** veya **eco** sınıfını tercih eden yolculardır.
- Sadık olmayan müşteriler ise özellikle kadınlarda kişisel seyahatlerde **eco** sınıfını daha çok tercih etmektedir.
- Erkek yolcuların iş seyahati ve business sınıfı tercihleri sadık müşteriler arasında oldukça yüksektir.
- Kişisel seyahatlerde sadık olmayan yolcu sayısı oldukça düşük görünmektedir.

## Sonuç ve Stratejik Öneriler

Bu proje kapsamında, bir havayolu şirketine ait **103.904 yolcu verisi** üzerinden veri ön işleme ve **Keşifsel Veri Analizi (EDA)** teknikleri uygulanarak **müşteri memnuniyetini etkileyen temel faktörler** detaylı şekilde ortaya konmuştur.

![image](https://github.com/user-attachments/assets/61f2b6c0-3521-4a8b-9482-ca4901d1b654)


###  Ana Bulgular

#### 1. **Hizmet Kalitesi Memnuniyetin Belirleyicisidir**
- Memnun yolcular, özellikle **online boarding (4.03)**, **uçuş içi eğlence (3.96)** ve **koltuk konforu (3.97)** gibi hizmetlere yüksek puan vermiştir.
- Bu değişkenlerde memnun ve memnun olmayan yolcular arasında **1 puandan fazla fark** gözlenmiştir.
- En yüksek fark `Online boarding` değişkenindedir (**+1.37**).

#### 2. **Gecikmeler Memnuniyetsizlikle Doğrudan İlişkili**
- **Kalkış gecikmesi (`Departure Delay`)**, memnuniyetsiz yolcularda çarpıcı biçimde yüksektir.
- `Departure Delay` ile `Arrival Delay` arasında **%96 pozitif korelasyon** tespit edilmiştir.
- Gecikmeler memnuniyet üzerinde dolaylı ama güçlü bir etkiye sahiptir.

#### 3. **Sadakat ve Seyahat Türü Kritik Segmentleyiciler**
- **Sadık müşterilerde memnuniyet oranı %90**’ın üzerindedir.
- **İş seyahati yapanlar (%92.72)** ve **Business sınıfı yolcular (%76.58)** memnuniyetin en yüksek olduğu gruplardır.
- **Ekonomi sınıfı, kişisel seyahat ve sadık olmayan müşteriler**, memnuniyetsizlik oranı en yüksek segmenttir.

#### 4. **Aykırı Değerler Gecikme Değişkenlerinde Yoğunlaşmıştır**
- `Departure Delay`: **%13.98** aykırı değer oranı  
- `Arrival Delay`: **%13.43** aykırı değer oranı  
- Bu değerler uçuş iptali, rötar gibi operasyonel problemleri yansıtabilir ve analiz dışı bırakılmamalıdır.

#### 5. **Eksik Veriler Segment Bazlı Medyan ile Doldurulmuştur**
- Sadece `Arrival Delay` sütununda %0.30 oranında eksik veri vardır.
- Bu eksik değerler, `Type of Travel` ve `Class` değişkenlerine göre **medyan** ile doldurulmuştur.
- Böylece istatistiksel dengesizlik ve veri kaybı önlenmiştir.

---

### Stratejik Öneriler

####  1. **Hizmet Kalitesine Yatırım**
- `Online boarding`, `entertainment`, `seat comfort` alanlarında iyileştirmeler yapılmalı.
- Dijital uygulamalar, kişiselleştirilmiş hizmetler ve kabin konforu artırılmalı.

####  2. **Gecikmeleri Azaltacak Operasyonel Önlemler**
- Yer hizmetleri, uçuş planlaması ve teknik bakım süreçleri optimize edilmeli.
- KPI takibi ile gecikmeler düzenli olarak izlenmelidir.

#### 3. **Hedef Segmentlere Yönelik Pazarlama**
- Ekonomi sınıfı ve yeni müşterilere sadakat programları, kolay check-in ve promosyonlar sunulmalı.
- Sadık müşteriler için özel ayrıcalıklar devam ettirilmelidir.

#### 4. **Veri Tabanlı Süreç Yönetimi**
- Segment bazlı raporlamalar ve düzenli EDA çalışmaları ile müşteri profili izlenmeli.
- Karar süreçleri veri odaklı hale getirilmelidir.

---

### Genel Değerlendirme

Bu proje, yalnızca bir EDA uygulaması değil, aynı zamanda **müşteri odaklı stratejik kararlar** geliştirmek için sağlam bir temel sunmaktadır.  
Hizmet kalitesi ve zaman yönetimi gibi faktörlerin iyileştirilmesiyle havayolu şirketi;

- **Müşteri memnuniyetini artırabilir,**
- **Sadakat oranlarını yükseltebilir,**
- **Rekabet avantajı elde edebilir.**


