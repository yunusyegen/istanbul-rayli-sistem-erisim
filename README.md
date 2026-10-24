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
  - Alt problem 3 (H1): saçılım grafiği ve korelasyon katsayısı
  - Alt problem 4 (H2): iki yakanın ortalama ve medyanlarının karşılaştırılması, kutu grafiği
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
- "toplu taşıma erişilebilirliği ilçe"
- "public transport accessibility equity"
- "metro accessibility population"

| Kaynak (yazar, yıl) | Problem | Veri | Yöntem | Temel bulgu | Sınırlılık | Projeme katkısı |
|---|---|---|---|---|---|---|
| | | | | | | |
| | | | | | | |
| | | | | | | |

Tablo doldukça buraya kısa bir özet paragrafı yazılacak. Kaynakların künyeleri
[`rapor/kaynaklar.bib`](rapor/kaynaklar.bib) dosyasında BibTeX biçiminde tutuluyor.

## 11. Klasör yapısı

```
istanbul-rayli-sistem-erisim/
├── README.md     proje özeti ve günlüğü
├── veri/         veri kaynakları, indirme talimatı, işlenmiş tablolar
├── analiz/       Google Colab not defteri
├── rapor/        LaTeX rapor ve kaynakça
└── sunum/        sunum dosyaları
```

## 12. Hedef çıktı (MVP)

39 ilçe için 100.000 kişiye düşen istasyon sayısını gösteren bir tablo ve bir sütun grafiği.

## 13. Proje günlüğü

| Hafta | Yaptıklarım |
|---|---|
| 1 | Konu seçildi, ders planı ve değerlendirme ölçütleri incelendi |
| 2 | Git ve VS Code kuruldu, GitHub hesabı hazırlandı, problem cümlesi ve hipotezler yazıldı |
| 3 | Veri kaynakları belirlendi, literatür taramasına başlandı |
| 4 | GitHub deposu kuruldu, README yazıldı, Issue'lar ve Kanban panosu hazırlandı |
