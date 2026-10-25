# İstanbul'da İlçelerin Raylı Sistem Erişimi

Araştırma Yöntem ve Teknikleri dersi dönem projesi (2026-2027 Güz).

Yunus Yeğen, Marmara Üniversitesi, Bilgisayar Programcılığı (uzaktan öğretim), 1. sınıf.
Proje bireyseldir, ekip arkadaşım yok.

## 1. Konu ve problem durumu

İstanbul'da metro, tramvay ve banliyö hatları her yıl biraz daha uzuyor. Ama bu hatlar şehre eşit
dağılmıyor. Bazı ilçelerde onlarca istasyon varken bazı ilçelerde hiç istasyon yok. Raylı sistem
trafiğe takılmadan işe, okula ve hastaneye gitmeyi kolaylaştırdığı için bir ilçede istasyon olup
olmaması orada yaşayanlar için fark yaratıyor. Buna rağmen istasyonların ilçelere dağılımının
nüfusla ne kadar uyumlu olduğu çoğunlukla tahminle konuşuluyor. İBB ve TÜİK verilerini açık
yayımladığı için bu soru tahminle değil sayılarla incelenebilir. Bu projede istasyonların ilçelere
dağılımını ilçe nüfusuyla karşılaştırıyorum.

## 2. Problem cümlesi ve alt problemler

**Problem cümlesi:** İstanbul'da raylı sistem istasyonlarının ilçelere dağılımı, ilçelerin nüfusu
ile orantılı mıdır?

**Alt problemler:**

1. İstanbul'un 39 ilçesinde kaç raylı sistem istasyonu var ve 100.000 kişiye kaç istasyon düşüyor?
2. Raylı sisteme erişimi en yüksek ve en düşük olan ilçeler hangileri?
3. İlçe nüfusu ile istasyon sayısı arasında ilişki var mı?
4. 100.000 kişiye düşen istasyon sayısı Avrupa ve Anadolu yakasına göre değişiyor mu?

## 3. Amaç ve önem

**Amaç:** Bu araştırmanın amacı, İstanbul'daki raylı sistem istasyonlarının ilçelere dağılımını
incelemek ve bu dağılımı ilçe nüfusu ve yaka ile karşılaştırmaktır.

**Önem:** Bulgular, nüfusuna göre raylı sistem erişimi düşük kalan ilçeleri gösterebilir. Bu da yeni
hat planlaması üzerine yapılan tartışmalara küçük bir katkı sağlayabilir.

## 4. Değişkenler ve işlevsel tanımları

| Değişken | Türü | İşlevsel tanım | Birim |
|---|---|---|---|
| İstasyon sayısı | Sayısal | İBB istasyon veri setinde o ilçeye kayıtlı, birbirinden farklı istasyonların sayısı | adet |
| İlçe nüfusu | Sayısal | TÜİK ADNKS 2025 sonuçlarına göre ilçenin toplam nüfusu | kişi |
| 100.000 kişiye düşen istasyon | Sayısal | (istasyon sayısı / ilçe nüfusu) x 100.000 | adet |
| Yaka | Kategorik | İlçenin bulunduğu yaka | Avrupa / Anadolu |

İstasyon sayısı için not: İBB veri setinde aynı istasyon çok sayıda satırda tekrar ediyor. Ayrıca
bazı istasyonlar `Sirkeci-1`, `Sirkeci-2` ya da `MAHMUTBEY M7 HOL 1` gibi girişlere göre ayrı ayrı
yazılmış. Bunların hepsi tek istasyon olarak sayılıyor. Nasıl saydığım `analiz/analiz.ipynb`
dosyasında adım adım yazıyor.

## 5. Hipotezler

**H1 (yönlü):** İlçe nüfusu arttıkça istasyon sayısı artar.
**H0:** İlçe nüfusu ile istasyon sayısı arasında ilişki yoktur.

**H2 (yönsüz):** 100.000 kişiye düşen istasyon sayısı Avrupa ve Anadolu yakası arasında farklıdır.
**H0:** 100.000 kişiye düşen istasyon sayısı iki yaka arasında farklı değildir.

## 6. Sayıltılar

- İBB'nin yayımladığı istasyon ve ilçe bilgilerinin doğru kaydedildiği varsayılmıştır.
- TÜİK nüfus verilerinin ilçelerin gerçek nüfusunu yansıttığı varsayılmıştır.
- Bir ilçedeki istasyon sayısının, o ilçede yaşayanların raylı sisteme erişimi hakkında fikir
  verdiği varsayılmıştır.

## 7. Sınırlılıklar

- Araştırma İstanbul'un 39 ilçesi ve 2025 yılı verisiyle sınırlıdır.
- İBB veri setinde Kocaeli sınırlarındaki Gebze, Darıca ve Çayırova istasyonları da var. Bunlar
  İstanbul ilçesi olmadığı için analiz dışında bırakıldı.
- İBB verisinde 13 istasyon birden fazla ilçeye kayıtlı görünüyor. Bunları şimdilik veride en
  çok geçtikleri ilçeye saydım. Hepsinin listesi analiz not defterinde yazıyor. Bu 13 istasyonu
  İBB hat haritasından tek tek kontrol edip gerekirse düzelteceğim.
- İstasyon sayısı, kişinin istasyona ne kadar yürüdüğünü ve seferlerin ne sıklıkta geçtiğini
  ölçmez. Bir ilçenin kenarındaki istasyon, ilçenin her yerine yakın demek değildir.
- Veri setinde teleferik, füniküler, Tünel ve nostaljik tramvay da raylı sistem olarak geçiyor.
  Bunlar şehir içi ulaşımda metro kadar kullanılmasa da sayıma dahil edildi.
- Metrobüs raylı sistem olmadığı için kapsam dışıdır.
- Veri setinin kapsadığı tarihten sonra açılan istasyonlar araştırmaya dahil değildir.

## 8. Yöntem

- **Araştırma türü:** Nicel, ikincil veri analizi (açık veri)
- **Evren:** İstanbul'un 39 ilçesi. Evrenin tamamı incelendiği için örneklem seçilmedi (tam sayım).
- **Analiz:**
  - Alt problem 1 ve 2: betimsel istatistik (ortalama, medyan, en büyük ve en küçük değer) ve
    sütun grafiği
  - Alt problem 3 (H1): saçılım grafiği, Pearson ve Spearman korelasyon katsayısı
  - Alt problem 4 (H2): iki yakanın ortalama ve medyanlarının karşılaştırılması, kutu grafiği ve
    Mann-Whitney U testi. Bu test, grup sayıları küçük olduğunda ve veri normal dağılmadığında
    kullanılıyor; burada birçok ilçede değer sıfır olduğu için veri normal dağılmıyor
- **Araçlar:** Google Colab (Python), GitHub, Overleaf, Zotero

**Yöntemin gerekçesi:** Araştırma sorusu iki sayısal değişken arasındaki ilişkiyi (nüfus ve istasyon
sayısı) ve iki grup arasındaki farkı (Avrupa ve Anadolu yakası) soruyor. Bu yüzden korelasyon ve
grup karşılaştırması uygun. Veriyi kendim toplamak yerine açık veri kullanıyorum, çünkü 39 ilçedeki
bütün istasyonları tek tek saymak bir dönemde mümkün değil ve İBB zaten bu kaydı tutuyor. Yöntem,
literatür taraması ilerledikçe değişebilir.

## 9. Veri setleri

| Veri | Kaynak | Lisans |
|---|---|---|
| Raylı sistem istasyonları (istasyon adı, hat, ilçe) | İBB Açık Veri Portalı | İBB Açık Veri Lisansı |
| İlçe nüfusları (2025) | TÜİK, Adrese Dayalı Nüfus Kayıt Sistemi | Resmî istatistik |

Dosyaların nereden indirildiği ve hangi sütunların kullanıldığı [`veri/README.md`](veri/README.md)
dosyasında yazıyor. Ham veri dosyaları boyutları büyük olduğu için depoya yüklenmedi, indirme
talimatı verildi.

## 10. Literatür taraması

Kaynakları Google Akademik, DergiPark, TR Dizin ve YÖK Ulusal Tez Merkezi üzerinden arıyorum.
Okuduğum her kaynağı aşağıdaki tabloya ekliyorum.

Kullandığım arama ifadeleri:
- "raylı sistem erişilebilirlik İstanbul"
- "toplu taşıma erişilebilirlik analizi İstanbul metro istasyon nüfus"
- "public transport accessibility equity"
- "metro station accessibility equity population district"

### Okuma listesi

Aşağıdaki kaynakları buldum ve künyelerini yayıncı sayfasından doğruladım. Okudukça aşağıdaki
karşılaştırma tablosuna işliyorum.

1. Öztaşkın, D. ve Levend, S. (2023). Toplu Taşıma Duraklarının Erişilebilirliği: İstanbul Örneği.
   *Türk Uzaktan Algılama ve CBS Dergisi*, 4(2), 301-318.
   [doi:10.48123/rsgis.1299707](https://doi.org/10.48123/rsgis.1299707)
   Projeme en yakın kaynak. İstanbul'da duraklara yürüme mesafesiyle erişimi ölçüyor.

2. Gökçe, B. (2024). Büyüyen Raylı Toplu Taşıma Sistem Ağında Hatlar ve İstasyonlar: İstanbul
   Örneği. *METU Journal of the Faculty of Architecture*, 41(1), 1-21.
   [doi:10.4305/METU.JFA.2024.1.1](https://doi.org/10.4305/METU.JFA.2024.1.1)
   İstanbul raylı sistem ağını istasyon düzeyinde inceliyor.

3. Cihan, U. ve Üstündağ, K. İ. (2025). A Sustainable Accessibility Approach in Transportation
   Planning: The Case of Istanbul. *Planlama Dergisi*, 35(3), 343-363.
   [doi:10.14744/planlama.2025.90958](https://doi.org/10.14744/planlama.2025.90958)
   İstanbul'da toplu taşımayla işe erişimi ve mekânsal eşitliği ölçüyor.

4. Zhu, J. ve Rui, X. (2025). Spatiotemporal Dynamics and Multi-Scale Equity Evaluation of Urban
   Rail Accessibility: Evidence from Hangzhou. *ISPRS International Journal of Geo-Information*,
   14(9), 361. [doi:10.3390/ijgi14090361](https://doi.org/10.3390/ijgi14090361)
   Raylı sistem erişiminin eşit dağılıp dağılmadığını Gini katsayısı ve Lorenz eğrisiyle ölçüyor.

5. Li, D., Zang, H., Guan, Z. ve Yu, D. (2025). Study on Spatial Distribution and Inequity of Rail
   Transit Travel Accessibility under Multi-modal Traveling: A Case Study of Beijing.
   *Scientific Reports*, 15(1), 15823.
   [doi:10.1038/s41598-025-97066-4](https://doi.org/10.1038/s41598-025-97066-4)
   Pekin'de raylı sistem erişimini ilçe düzeyinde karşılaştırıyor.

6. Alp, G. (2022). *İstanbul'da Raylı Sistem Yatırımlarının Kentin Gelişimi ve Arazi Kullanımı
   Üzerindeki Etkileri: Arnavutköy İlçesi Örneği* (Yüksek lisans tezi). İstanbul Sabahattin Zaim
   Üniversitesi.
   [Açık erişim kaydı](https://openaccess.izu.edu.tr/entities/publication/4440f75d-8ca7-4ba2-bbe1-4f5e23334672)
   Tek bir ilçe üzerinden raylı sistem yatırımının etkisini ele alıyor.

### Karşılaştırma tablosu

| Kaynak | Problem | Veri | Yöntem | Temel bulgu | Sınırlılık | Projeme katkısı |
|---|---|---|---|---|---|---|
| Öztaşkın ve Levend (2023) | İstanbul'da duraklara erişim yeterli mi? | İBB durak ve hat verisi, 2020 bina nüfus verisi | CBS, ArcGIS servis alanı analizi, 5/10/15 dk yürüme | Raylı sisteme 5 dk'da ulaşan nüfus %2,88. Avrupa yakası Anadolu'dan daha iyi | Sefer sıklığı, maliyet ve konfor ölçülmemiş | Yaka farkını benim gibi soruyor, erişimi farklı ölçüyor. Sefer sıklığı sınırlılığı benimkiyle aynı |
| Gökçe (2024) | Ağa eklenen istasyonun yolcu sayısına katkısı neye bağlı? | 186 istasyon, 5 yıl (2013-2022), 745 gözlem, 1 km'deki nüfus ve işyeri | Rastgele etkiler panel veri regresyonu | Nüfus %1 artınca yolcu %0,10 artıyor, işyeri iki kat etkili. Avrupa yakası anlamsız (t=0,68) | Panel veride yıl bazlı eksikler model kalitesini etkiliyor | H1 ve H2 sonuçlarımı destekliyor. İstanbul dışı Marmaray istasyonlarını dışlaması benim temizliğimle aynı |
| Cihan ve Üstündağ (2025) | Toplu taşımayla istihdama erişim adil mi? | 1307 TAZ, 2022 istihdam verisi, 2040 senaryosu, İUAP anketleri | Kümülatif olanaklar yöntemi, 30/60/90 dk eşik, CBS | 60 dk'da erişim %24,41'den %32,55'e çıkıyor. 30 dk'da en düşük değer hiç değişmiyor | Bütün olanaklar eşit ağırlıklı sayılıyor | Merkez ilçelerin (Fatih, Şişli, Beşiktaş, Kadıköy) yüksek çıkması benim tablomla aynı |
| Zhu ve Rui (2025) | Metro ağı büyürken erişim eşit dağılıyor mu? | Hangzhou, 2019 ve 2023 metro ağı, yol ağı, nüfus dağılımı | Ağ tabanlı tampon azalma modeli, Gini katsayısı, Lorenz eğrisi, Moran's I | TAZ ölçeğinde Gini 0,56'dan 0,425'e düşmüş ama grid ölçeğinde 0,404'te kalmış | Ayrı sınırlılık bölümü yok. Tek şehir, iki yıl. Endeks merkezi alanları kayırıyor | Eşitsizliği tek sayıyla ölçmenin yolunu gösteriyor: Gini ve Lorenz. Sonraki aşamada ekleyeceğim |
| Li ve ark. (2025) | İstasyon erişimi ile nüfus yoğunluğu uyuşuyor mu? | Pekin 6. Çevre Yolu içi, Gaode Map API, dört ulaşım türü, nüfus verisi | Gauss tabanlı 2SFCA, Gini katsayısı, IPA | Merkez ve alt merkezlerde erişim yüksek. Erişim en adaletsiz yürüyerek ve toplu taşımayla | Nüfus grupları (yaş, cinsiyet) ayrılmamış, trafik yoğunluğu ve banliyöler kapsam dışı | Erişimi alt bölge düzeyinde karşılaştırıyor. Merkez-çeper farkı benim bulgumla aynı yönde |
| Alp (2022) | Raylı sistem yatırımı ilçeyi nasıl dönüştürür? | Arnavutköy planlama belgeleri, nüfus verileri, Halkalı-Havalimanı hattı proje bilgileri | Nitel durum incelemesi, belge analizi | Ulaşım yatırımı ile arazi kullanımı ve gayrimenkul değeri arasında güçlü bağ var | Tek ilçe, henüz açılmamış hat, sayısal ölçüm yok | Benim 39 ilçelik yüzeysel bakışımın tersi: tek ilçeye derinlemesine bakıyor, tamamlayıcı |

Her kaynağın daha ayrıntılı notu [`rapor/okuma_notlari.md`](rapor/okuma_notlari.md) dosyasında.
Künyeler [`rapor/kaynaklar.bib`](rapor/kaynaklar.bib) dosyasında BibTeX biçiminde tutuluyor.

### Literatürün özeti

Okuduğum altı kaynak, raylı sistem erişiminin kent içinde eşit dağılmadığının hem İstanbul'da hem
başka şehirlerde tekrar tekrar bulunan bir sonuç olduğunu gösteriyor. İstanbul'u inceleyen üç
çalışmanın üçü de merkez ilçelerin çeper ilçelerden belirgin biçimde iyi durumda olduğunu buluyor.
Cihan ve Üstündağ (2025) Fatih, Şişli, Beşiktaş ve Kadıköy'ü sürekli yüksek skorlu ilçeler olarak
sayıyor; benim 100.000 kişiye düşen istasyon sıralamamda da bu ilçeler üst sıralarda çıktı.

Nüfusla ilişki konusunda Gökçe'nin (2024) bulgusu benim açımdan en önemlisi. İstasyon çevresindeki
nüfusun %1 artması yolcu sayısını yalnızca %0,10 artırıyor, işyeri sayısı ise iki kat etkili.
Yazarın kendi ifadesiyle nüfusla paralel bir yolcu artışı yok. Aynı çalışmada Avrupa yakasında olmak
da anlamlı bir fark yaratmıyor. Bu iki sonuç benim bulgularımla aynı yönde: ben de nüfus ile istasyon
sayısı arasında anlamlı bir ilişki ve iki yaka arasında anlamlı bir fark bulamadım.

Yöntem açısından en çok Zhu ve Rui (2025) ile Li ve ark. (2025) işime yarıyor. İkisi de eşitsizliği
Gini katsayısıyla tek bir sayıya indiriyor. Benim 100.000 kişiye düşen istasyon sayım 39 ilçeye
yayılmış bir dağılım olduğu için aynı hesabı yapabilirim. Bunu projenin sonraki aşamasına
ekleyeceğim.

Kaynakların ortak bir sınırlılığı var ve bu benimkiyle örtüşüyor: hiçbiri sefer sıklığını, bilet
maliyetini ve yolculuk konforunu hesaba katmıyor. Öztaşkın ve Levend (2023) bunu açıkça gelecek
çalışmalara bırakıyor. Yani "ilçede istasyon var" demek "o ilçede yaşayan herkes raylı sisteme
erişebiliyor" demek değil. Benim ölçütüm de bunu ölçmüyor ve sınırlılıklar bölümünde bunu yazdım.

## 11. İlk bulgular

Aşağıdaki sayılar [`analiz/analiz.ipynb`](analiz/analiz.ipynb) not defterinin çıktısıdır. Tam tablo
[`veri/islenmis/ilce_erisim.csv`](veri/islenmis/ilce_erisim.csv) dosyasında duruyor.

**Uyarı:** Bunlar ön bulgu. Sınırlılıklar bölümünde yazdığım 13 istasyonun ilçesini haritadan
kontrol edince birkaç ilçenin sayısı değişebilir.

| | Değer |
|---|---|
| Analize giren istasyon sayısı | 304 |
| Hiç istasyonu olmayan ilçe sayısı | 10 |
| 100.000 kişiye düşen istasyon, ortalama | 2,07 |
| 100.000 kişiye düşen istasyon, medyan | 1,67 |
| En yüksek | Fatih, 12,22 |
| En düşük | 10 ilçede 0,00 |

Hiç istasyonu olmayan ilçeler: Adalar, Avcılar, Beykoz, Beylikdüzü, Büyükçekmece, Esenyurt,
Silivri, Sultanbeyli, Şile ve Çatalca.

![İlçelere göre raylı sistem erişimi](rapor/sekiller/sekil1_ilce_erisim.png)

**Alt problem 3 (H1):** Nüfus ile istasyon sayısı arasında Spearman korelasyonu r = 0,285 ve
p = 0,079 çıktı. p değeri 0,05'ten büyük olduğu için H0 reddedilemedi.

**Alt problem 4 (H2):** Avrupa yakasının medyanı 2,02, Anadolu yakasının 0,87. Mann-Whitney U
testinde U = 228,0 ve p = 0,121 çıktı. Fark anlamlı değil, H0 reddedilemedi.

Bu iki sonucun ayrıntılı yorumu ve literatürle karşılaştırması #9, #10 ve #11 numaralı Issue'larda
yapılacak.

## 12. Klasör yapısı

```
istanbul-rayli-sistem-erisim/
├── README.md               proje özeti, bulgular ve günlük
├── veri/
│   ├── README.md           veri kaynakları ve indirme talimatı
│   ├── ilce_nufus.csv      39 ilçenin yakası ve TÜİK nüfusu
│   ├── ham/                indirilen ham dosyalar (depoya yüklenmiyor)
│   └── islenmis/           ilce_erisim.csv
├── analiz/
│   └── analiz.ipynb        Google Colab not defteri
├── rapor/
│   ├── kaynaklar.bib       BibTeX künyeleri
│   ├── okuma_notlari.md    kaynak okuma kartları
│   └── sekiller/           grafikler
└── sunum/                  sunum dosyaları
```

## 13. Hedef çıktı (MVP)

39 ilçe için 100.000 kişiye düşen istasyon sayısını gösteren bir tablo ve bir sütun grafiği.

## 14. Proje günlüğü

| Hafta | Yaptıklarım |
|---|---|
| 1 | Konu seçildi, ders planı ve değerlendirme ölçütleri incelendi |
| 2 | Git ve VS Code kuruldu, GitHub hesabı hazırlandı, problem cümlesi ve hipotezler yazıldı |
| 3 | Veri kaynakları belirlendi, İBB ve TÜİK dosyaları indirildi |
| 4 | GitHub deposu kuruldu, README yazıldı, veri temizlendi ve ilk analiz yapıldı, 15 Issue ile Kanban panosu hazırlandı, 6 kaynak okunup literatür tablosu dolduruldu |

## 15. Proje yönetimi

İşleri GitHub Issue'larına böldüm. Her Issue'nun bir kabul kriteri listesi, bir konu etiketi
(Veri, Analiz, Literatür, Doküman) ve bir öncelik etiketi (Must, Should, Could) var.

İşleri Kanban panosunda takip ediyorum. Panonun sütunları: Backlog, To Do, In Progress,
Review/Test, Done. In Progress sütununda aynı anda en fazla 2 kart tutuyorum (WIP limiti), çünkü
aynı anda çok işe başlayınca hiçbiri bitmiyor.

**Pano:** https://github.com/users/yunusyegen/projects/2

### Sprint 1

**Hedef:** 13 şüpheli istasyonun ilçesi kesinleşsin ve literatür tablosunda en az 5 okunmuş kaynak
olsun.

**Süre:** 1 hafta

| Issue | İş | Öncelik |
|---|---|---|
| #6 | Birden fazla ilçeye kayıtlı 13 istasyonu haritadan kontrol et | Must |
| #7 | En az 5 güvenilir kaynak bul, oku ve literatür tablosunu doldur | Must |
| #8 | Kaynakları Zotero'ya ekle ve kaynaklar.bib dosyasını üret | Must |
| #9 | Betimsel istatistikleri yorumla (alt problem 1 ve 2) | Must |

**Bitti sayılma koşulu (Definition of Done):** İş depoya commit edildi, Issue'daki kabul
kriterlerinin hepsi işaretlendi, not defteri baştan sona hatasız çalışıyor ve değişiklik README'ye
yansıtıldı.

## 16. Yapay zekâ kullanım beyanı

Bu projede yapay zekâ aracı olarak Claude (Anthropic) kullandım. Dersin kuralı gereği hangi işte
kullandığımı ayrıntılı yazıyorum.

**Yapay zekâyı kullandığım yerler:**

- README.md ve veri/README.md dosyalarının yazılması ve düzenlenmesi
- Analiz not defterindeki Python kodunun yazılması
- İBB veri setinde aynı istasyonun birden çok adla geçtiğinin fark edilmesi ve bunu düzelten
  temizleme kodunun yazılması
- Literatür taramasında kaynak adaylarının aranması ve bulunan kaynakların künyelerinin Crossref
  ile yayıncı sayfaları üzerinden doğrulanması
- Okuduğum kaynakların karşılaştırma tablosuna ve okuma notlarına aktarılmasında taslak metin

**Kendi yaptıklarım:**

- Konunun, problem cümlesinin, alt problemlerin, değişkenlerin ve hipotezlerin belirlenmesi
- Veri setlerinin İBB ve TÜİK portallarından indirilmesi
- Kaynakların tam metinlerinin okunması ve tablodaki bilgilerin kaynakla karşılaştırılarak
  kontrol edilmesi
- Analiz çıktılarının ve tablodaki sayıların kontrol edilmesi
- Bulguların yorumlanması

Yapay zekâ bir kaynak olmadığı için kaynakçada yer almıyor ve metinde ona atıf yapılmadı.
Kaynakçadaki bütün künyeleri DOI veya yayıncı sayfası üzerinden ayrıca doğruladım.
