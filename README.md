# İstanbul'da İlçelerin Raylı Sistem Erişimi

Araştırma Yöntem ve Teknikleri dersi dönem projesi (2026-2027 Güz).

Yunus Yeğen, Marmara Üniversitesi, Bilgisayar Programcılığı (uzaktan öğretim), 1. sınıf.
Proje bireyseldir, ekip arkadaşım yok.

[![Colab'da aç](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yunusyegen/istanbul-rayli-sistem-erisim/blob/main/analiz/analiz.ipynb)

Analiz not defteri Colab'da tek tıkla çalışıyor ve veriyi kaynağından kendisi indiriyor
(bkz. 14. Nasıl çalıştırılır).

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

**"Orantılı" ne demek?** Bu soruyu ölçebilmek için kavramı tanımlamam gerekiyor. İstasyonlar nüfusla
tam orantılı dağılsaydı, 100.000 kişiye düşen istasyon sayısı bütün ilçelerde **aynı** olurdu. O
hâlde orantılılığı, bu sayının ilçeler arasında ne kadar değiştiğine bakarak ölçüyorum. Bunun için
değişim katsayısı ve Gini katsayısı kullanıyorum (bkz. 9. Yöntem).

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

| Değişken | Rolü | Türü | İşlevsel tanım | Birim |
|---|---|---|---|---|
| İlçe nüfusu | Bağımsız | Sayısal (oranlı) | TÜİK ADNKS 2025 sonuçlarına göre ilçenin toplam nüfusu | kişi |
| Yaka | Bağımsız | Kategorik (sınıflama) | İlçenin bulunduğu yaka | Avrupa / Anadolu |
| İstasyon sayısı | Bağımlı | Sayısal (oranlı) | İBB istasyon verisinden çıkarılan, koordinatıyla o ilçeye yerleştirilen, birbirinden farklı istasyonların sayısı | adet |
| 100.000 kişiye düşen istasyon | Bağımlı | Sayısal (oranlı) | (istasyon sayısı / ilçe nüfusu) x 100.000 | adet |

İstasyon sayısı için not: İBB veri setinde aynı istasyon çok sayıda satırda tekrar ediyor, bazı
istasyonlar `Sirkeci-1`, `Sirkeci-2` ya da `MAHMUTBEY M7 HOL 1` gibi girişlere göre ayrı ayrı yazılmış
ve ilçe sütunu bazı istasyonlarda hatalı. Bu yüzden istasyonu şöyle tanımladım: adı aynı olan ve
birbirine 1 km'den yakın istasyon kodları tek istasyon sayılıyor. İstasyonun ilçesi ise İBB'nin yazdığı
ilçe değil, koordinatının düştüğü ilçe (sınır boyunda İBB'nin kaydı korunuyor). Ayrıntısı
9. bölümde (Yöntem) özetleniyor ve `analiz/analiz.ipynb` dosyasında adım adım yazıyor.

## 5. Hipotezler

**H1 (yönlü):** İlçe nüfusu arttıkça istasyon sayısı artar.
**H0:** İlçe nüfusu ile istasyon sayısı arasında ilişki yoktur.

**H2 (yönsüz):** 100.000 kişiye düşen istasyon sayısı Avrupa ve Anadolu yakası arasında farklıdır.
**H0:** 100.000 kişiye düşen istasyon sayısı iki yaka arasında farklı değildir.

**H2'yi neden kurdum?** İstanbul'un ilk metro ve tramvay hatları Avrupa yakasında açıldı ve tarihî
merkez, merkezî iş alanı ile havalimanlarının çoğu bu yakada. Raylı sistem yatırımları uzun yıllar
boyunca bu yakada yoğunlaştığı için iki yaka arasında bir fark olmasını bekledim. Yönünü önceden
kestiremediğim için hipotezi yönsüz kurdum.

## 6. Sayıltılar

- İBB'nin yayımladığı istasyon ve ilçe bilgilerinin doğru kaydedildiği varsayılmıştır.
- TÜİK nüfus verilerinin ilçelerin gerçek nüfusunu yansıttığı varsayılmıştır.
- Bir ilçedeki istasyon sayısının, o ilçede yaşayanların raylı sisteme erişimi hakkında fikir
  verdiği varsayılmıştır.

## 7. Sınırlılıklar

- Araştırma İstanbul'un 39 ilçesi ve 2025 yılı verisiyle sınırlıdır.
- İBB veri setinde Kocaeli sınırlarındaki Gebze, Darıca ve Çayırova istasyonları da var (Marmaray'ın
  İstanbul dışında kalan durakları). İstanbul ilçesi olmadıkları için analiz dışında bırakıldı.
- İBB'nin ilçe sütunu bazı istasyonlarda hatalı (örneğin M8'in Ümraniye'deki istasyonları "Maltepe"
  yazılmış). Bu yüzden her istasyonun ilçesini koordinatıyla ilçe sınırlarına karşılaştırarak
  doğruladım ve 17 istasyonun ilçesini düzelttim. Bu doğrulamanın kendi sınırları var:
  - 56 istasyonun koordinatı yok ya da kullanılamıyor (İBB dosyasında koordinat yazımı bozuk,
    bazıları Excel'de tarihe dönüşmüş). Bunlarda İBB'nin ilçe kaydına güvendim.
  - İlçe sınırları resmî değil, OpenStreetMap kaynaklı bir dosyadan geliyor ve birkaç on metre
    sapabilir. Bu yüzden koordinatı İBB'nin ilçesinin sınırına 200 m'den yakın 10 istasyonda
    İBB'nin kaydını korudum.
- Aynı adlı istasyon kodlarını 1 km içindeyse tek istasyon saydım. 1 km ve 200 m benim kararım
  (nedenleri 9. bölümde ve not defterinde). Bunları değiştirince sonucun nasıl değiştiğini
  duyarlılık analizinde gösterdim; Gini ve H2 sonucu kararlı, H1'in p değeri ise 0,05'e yakın ve
  kararlara duyarlı (bkz. 13. İlk bulgular).
- İstasyon sayısı, kişinin istasyona ne kadar yürüdüğünü ve seferlerin ne sıklıkta geçtiğini
  ölçmez. Bir ilçenin kenarındaki istasyon, ilçenin her yerine yakın demek değildir.
- İlçelerin yüzölçümü analize girmiyor. Çatalca ve Silivri gibi çok geniş ve kırsal ilçelerle
  Güngören gibi küçük ve yoğun ilçeler aynı tabloda karşılaştırılıyor. Nüfus yoğunluğu, ilçenin
  kent merkezine uzaklığı ve işyeri sayısı gibi değişkenler sonucu etkiliyor olabilir. Gökçe
  (2024) işyeri sayısının nüfustan iki kat etkili olduğunu bulmuş. Bu değişkenleri eklemek
  dönemin sonraki aşamasına bırakıldı.
- Analiz 39 ilçe üzerinde yapıldığı için gözlem sayısı az. Bu, istatistiksel testlerin zayıf bir
  ilişkiyi yakalama gücünü düşürüyor.
- Veri setinde teleferik, füniküler, Tünel ve nostaljik tramvay da raylı sistem olarak geçiyor.
  Bunlar şehir içi ulaşımda metro kadar kullanılmasa da sayıma dahil edildi; duyarlılık analizinde
  hariç tutarak da denedim.
- Metrobüs raylı sistem olmadığı için kapsam dışıdır.
- Veri setinin kapsadığı tarihten sonra açılan istasyonlar araştırmaya dahil değildir.

## 8. Ekip ve roller

Proje bireyseldir, ekip arkadaşım yok. Bu yüzden bütün görevler bana ait. Görevleri yine de
Issue'lara bölüp Kanban panosunda kendime atadım (bkz. 19. Proje yönetimi).

| Kişi | Rol | Üstlendiği görevler |
|---|---|---|
| Yunus Yeğen | Araştırmacı, veri analisti ve depo sorumlusu | Konunun ve araştırma sorusunun belirlenmesi, İBB ve TÜİK verilerinin indirilmesi, veri temizleme ve analiz, literatür taraması, yorum, README ve GitHub düzeni (Issue'lar, pano) |

## 9. Yöntem

- **Araştırma türü:** Nicel, ikincil veri analizi (açık veri)
- **Evren:** İstanbul'un 39 ilçesi. Evrenin tamamı incelendiği için örneklem seçilmedi (tam sayım).
- **Veri hazırlama (not defterinin 2. ve 3. adımı):**
  1. İBB dosyasındaki yinelenen satırlar ve aynı istasyonun farklı yazımları (`Sirkeci-1`, `HOL 1`
     gibi) tek ada indirgenir. Adı boş iki nostaljik tramvay istasyonu hat adıyla tutulur.
  2. Her istasyon kodunun koordinatı çözülür. Koordinat sütununun yazımı bozuk (`289.335.555.555.556`,
     `29.Eyl`, `29.0` gibi). İlk iki rakamı tam kısım sayıp gerisini ondalık yazarak çözüyorum,
     5 rakamdan kısa ya da tarihe dönüşmüş değerleri kullanmıyorum.
  3. Adı aynı olan ve birbirine 1000 m'den yakın kodlar tek istasyon sayılır. Aynı kompleksin
     salonları birbirine en fazla yaklaşık 560 m uzakta, farklı yerlerdeki aynı adlar en az yaklaşık
     1,2 km uzakta; 1000 m bu boşluğun içinde.
  4. İstasyonun ilçesi, koordinatının ilçe sınırlarında düştüğü ilçedir. Koordinat İBB'nin yazdığı
     ilçenin sınırına 200 m'den yakınsa İBB'nin kaydı korunur. Koordinatı olmayan istasyonlarda
     İBB'nin kaydı kullanılır.
- **Analiz:**
  - Alt problem 1 ve 2: betimsel istatistik (toplam, ortalama, medyan, en büyük ve en küçük değer) ve
    sütun grafiği
  - Problem cümlesinin doğrudan cevabı: değişim katsayısı, Gini katsayısı ve Lorenz eğrisi. Bu
    yöntemi literatürden aldım; Zhu ve Rui (2025) ile Li ve ark. (2025) raylı sistem erişiminin
    eşitliğini tam olarak bu ölçülerle değerlendiriyor
  - Alt problem 3 (H1): saçılım grafiği, Pearson ve Spearman korelasyon katsayısı
  - Alt problem 4 (H2): iki yakanın ortalama ve medyanlarının karşılaştırılması, kutu grafiği ve
    Mann-Whitney U testi. Bu test, grup sayıları küçük olduğunda ve veri normal dağılmadığında
    kullanılıyor; burada birçok ilçede değer sıfır olduğu için veri normal dağılmıyor
  - Duyarlılık analizi: verdiğim kararların (aynı yer yarıçapı, İBB'ye güven payı, koordinat
    kontrolünün hiç yapılmaması, teleferik ve füniküler gibi hatların dahil edilmesi) sonucu ne
    kadar değiştirdiğinin kontrolü, toplam 7 senaryo
- **Araçlar:** Google Colab (Python: pandas, scipy, shapely, matplotlib), GitHub, Overleaf, Zotero

**Yöntemin gerekçesi:** Araştırma sorusu iki sayısal değişken arasındaki ilişkiyi (nüfus ve istasyon
sayısı) ve iki grup arasındaki farkı (Avrupa ve Anadolu yakası) soruyor. Bu yüzden korelasyon ve
grup karşılaştırması uygun. Veriyi kendim toplamak yerine açık veri kullanıyorum, çünkü 39 ilçedeki
bütün istasyonları tek tek saymak bir dönemde mümkün değil ve İBB zaten bu kaydı tutuyor.

**Korelasyon neden tek başına yetmiyor?** Korelasyon "nüfus artarsa istasyon sayısı da artıyor mu?"
sorusunu cevaplıyor. Benim problem cümlem bundan daha güçlü bir şey soruyor: dağılım nüfusla
*orantılı* mı? İkisi aynı değil. Nüfusu 100.000 olan ilçede 10, nüfusu 1.000.000 olan ilçede 11
istasyon olsa korelasyon pozitif çıkar ama dağılım hiç orantılı olmaz. Bu yüzden asıl cevabı Gini
katsayısıyla veriyorum, korelasyonu yardımcı bilgi olarak kullanıyorum.

**Tam sayım ve hipotez testi hakkında bir not:** 39 ilçenin tamamını incelediğim için elimde bir
örneklem değil, evrenin kendisi var. p değeri aslında "bu sonuç örnekleme tesadüfünden doğmuş
olabilir mi?" sorusunu cevaplar; ortada örnekleme olmadığı için bu sorunun burada karşılığı zayıf.
Bu yüzden asıl kanıtım betimsel ölçüler (Gini katsayısı, değişim katsayısı, medyanlar); korelasyon
ve Mann-Whitney U testini bunları destekleyen ikincil bilgi olarak raporluyorum. Testleri,
İstanbul'un 2025'teki durumunu daha geniş bir "büyük şehir ilçeleri" topluluğundan bir kesit kabul
ederek yorumluyorum.

**Anlamlı çıkmaması ne demek değildir:** H0'ın reddedilememesi "ilişki yoktur" anlamına gelmez,
"bu veriyle bir ilişki gösterilemedi" anlamına gelir. 39 ilçe küçük bir sayı olduğu için testin
zayıf bir ilişkiyi yakalama gücü düşük.

Yöntem, literatür taraması ilerledikçe değişebilir.

## 10. Veri setleri

| Veri | Kaynak ve bağlantı | Lisans veya kullanım koşulu |
|---|---|---|
| Raylı sistem istasyonları (adı, hattı, kodu, ilçesi, koordinatı), 2025 | İBB Bilgi İşlem Dairesi Başkanlığı, [Raylı Sistemler İstasyon Bazlı Yolcu ve Yolculuk Sayıları](https://data.ibb.gov.tr/dataset/rayli-sistemler-istasyon-bazli-yolcu-ve-yolculuk-sayilari) | [İBB Açık Veri Lisansı](https://data.ibb.gov.tr/license) |
| İlçe nüfusları (2025) | TÜİK, Adrese Dayalı Nüfus Kayıt Sistemi, [TÜİK Veri Portalı](https://veriportali.tuik.gov.tr) | Kaynak gösterilerek yeniden kullanılabilir, bkz. [TÜİK yasal uyarı](https://www.tuik.gov.tr/Kurumsal/Yasal_Uyari) |
| İlçe sınırları (istasyonların ilçesini doğrulamak için) | [geoBoundaries](https://www.geoboundaries.org/), kaynak veri OpenStreetMap | [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/), © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright) |

Dosyaların nereden indirildiği, hangi sütunların kullanıldığı ve verideki sorunlar
[`veri/README.md`](veri/README.md) dosyasında yazıyor. Ham veri dosyaları büyük olduğu için depoya
yüklenmedi; not defteri bunları kaynağından kendisi indiriyor. İBB sunucusuna ulaşılamazsa kullanılmak üzere, İBB
dosyasının kullandığım altı sütununun satır sayılarıyla özetlenmiş hâli depoda duruyor
([`veri/istasyon_ozet.csv`](veri/istasyon_ozet.csv), 33 KB).

## 11. Etik

Bu araştırma insanlarla değil, kamuya açık ikincil verilerle yapılıyor. Anket yapılmıyor, görüşme
yapılmıyor, bu yüzden katılımcı onamı ve etik kurul izni gerektiren bir durum yok.

- **Kişisel veri yok.** İBB veri setindeki yolcu sayıları istasyon ve gün düzeyinde
  toplulaştırılmış; kimsenin kim olduğu, nereye gittiği yazmıyor. TÜİK verisi de ilçe düzeyinde
  toplam nüfus.
- **Lisanslara uyuluyor.** İBB Açık Veri Lisansı kaynak gösterilmesi şartıyla kopyalamaya ve
  uyarlamaya izin veriyor, TÜİK'in yasal uyarısı kaynak gösterilerek yeniden kullanıma izin veriyor,
  ODbL 1.0 ise © OpenStreetMap contributors atfıyla kullanıma izin veriyor. Üçünün de adı, bağlantısı,
  yılı ve lisansı yukarıdaki tabloda ve [`veri/README.md`](veri/README.md) dosyasında yazıyor. Bu
  çalışma İBB, TÜİK, OpenStreetMap ya da geoBoundaries tarafından onaylanmamıştır.
- **Veri izinsiz yeniden yayımlanmıyor.** Ham dosyalar ve ilçe sınırları depoya yüklenmedi; yerine indirme
  bağlantısı verildi (bkz. [`veri/README.md`](veri/README.md)). Depoda yalnızca İBB dosyasının altı
  sütununun özeti (kopyalamaya ve uyarlamaya kaynak gösterilerek izin veren İBB Açık Veri Lisansı
  kapsamında, 33 KB) ve TÜİK'ten alınan 39 nüfus değeri var.
- **Depoda kişisel bilgi tutulmuyor.** Öğrenci numarası, telefon ve e-posta gibi bilgiler depoya
  konmuyor.
- **Gizli bilgi yok.** Depoda ve Colab not defterinde şifre, API anahtarı ya da erişim anahtarı
  bulunmuyor; not defteri Google Drive'a bağlanmıyor ve hiçbir hesaba giriş yapmıyor. Anahtar gerekirse Colab Secrets kullanılacak.
  Paylaşmadan önce dosyalar, git geçmişi ve not defterinin çıktı hücreleri taranarak bunlar
  doğrulandı.
- **Kaynaklar okunarak kullanılıyor** ve yapay zekâ kullanımı 20. bölümde beyan ediliyor.
- **Sınırlılıklar ve belirsizlikler gizlenmiyor.** Veri temizliğinde verdiğim kararlar ve bunların
  sonuca etkisi duyarlılık analiziyle açıkça gösteriliyor.

## 12. Literatür taraması

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
| Zhu ve Rui (2025) | Metro ağı büyürken erişim eşit dağılıyor mu? | Hangzhou, 2019 ve 2023 metro ağı, yol ağı, nüfus dağılımı | Ağ tabanlı tampon azalma modeli, Gini katsayısı, Lorenz eğrisi, Moran's I | TAZ ölçeğinde Gini 0,56'dan 0,425'e düşmüş ama grid ölçeğinde 0,404'te kalmış | Ayrı sınırlılık bölümü yok. Tek şehir, iki yıl. Endeks merkezi alanları kayırıyor | Eşitsizliği tek sayıyla ölçmenin yolunu gösteriyor: Gini ve Lorenz. Kendi verime uyguladım (Gini = 0,500) |
| Li ve ark. (2025) | İstasyon erişimi ile nüfus yoğunluğu uyuşuyor mu? | Pekin 6. Çevre Yolu içi, Gaode Map API, dört ulaşım türü, nüfus verisi | Gauss tabanlı 2SFCA, Gini katsayısı, IPA | Merkez ve alt merkezlerde erişim yüksek. Erişim en adaletsiz yürüyerek ve toplu taşımayla | Nüfus grupları (yaş, cinsiyet) ayrılmamış, trafik yoğunluğu ve banliyöler kapsam dışı | Erişimi alt bölge düzeyinde karşılaştırıyor. Merkez-çeper farkı benim bulgumla aynı yönde |
| Alp (2022) | Raylı sistem yatırımı ilçeyi nasıl dönüştürür? | Arnavutköy planlama belgeleri, nüfus verileri, Halkalı-Havalimanı hattı proje bilgileri | Nitel durum incelemesi, belge analizi | Ulaşım yatırımı ile arazi kullanımı ve gayrimenkul değeri arasında güçlü bağ var | Tek ilçe, henüz açılmamış hat, sayısal ölçüm yok | Benim 39 ilçelik yüzeysel bakışımın tersi: tek ilçeye derinlemesine bakıyor, tamamlayıcı |

Her kaynağın daha ayrıntılı notu [`rapor/okuma_notlari.md`](rapor/okuma_notlari.md) dosyasında.
Künyeler [`rapor/kaynaklar.bib`](rapor/kaynaklar.bib) dosyasında BibTeX biçiminde tutuluyor.

### Literatürün özeti

Okuduğum altı kaynak, raylı sistem erişiminin kent içinde eşit dağılmadığının hem İstanbul'da hem
başka şehirlerde tekrar tekrar bulunan bir sonuç olduğunu gösteriyor. İstanbul'u inceleyen
çalışmalardan Cihan ve Üstündağ (2025) Fatih, Şişli, Beşiktaş ve Kadıköy'ü sürekli yüksek skorlu
ilçeler olarak sayıyor; benim 100.000 kişiye düşen istasyon sıralamamda da bu ilçeler ilk 8'de çıktı
(Fatih, Şişli, Kadıköy ve Beşiktaş sırasıyla 1., 5., 6. ve 8.). Öztaşkın ve Levend (2023) ise Avrupa
yakasında oturanların raylı sisteme Anadolu yakasındakilerden daha iyi eriştiğini buluyor. Yurt dışı
çalışmalar da (Zhu ve Rui 2025, Li ve ark. 2025) merkez ile çeper arasında benzer bir fark gösteriyor.

Nüfusla ilişki konusunda Gökçe'nin (2024) bulgusu benim açımdan en önemlisi. İstasyon çevresindeki
nüfusun %1 artması yolcu sayısını yalnızca %0,10 artırıyor, işyeri sayısı ise iki kat etkili.
Yazarın kendi ifadesiyle nüfusla paralel bir yolcu artışı yok. Aynı çalışmada Avrupa yakasında olmak
da anlamlı bir fark yaratmıyor. Bu iki sonuç benim bulgularımla aynı yönde: ben de nüfus ile istasyon
sayısı arasında anlamlı bir ilişki ve iki yaka arasında anlamlı bir fark bulamadım. Ama H1'in p değeri
0,05'e yakın (0,100) ve kararlarıma duyarlı, bunu 13. bölümde açıkça yazdım.

Bir noktada literatürle çelişiyor gibi görünüyorum ve bunu açıkça yazmam gerekiyor. Öztaşkın ve
Levend (2023) Avrupa yakasının raylı sisteme Anadolu yakasından daha iyi eriştiğini söylüyor.
Benim H2 testim ise iki yaka arasında anlamlı fark bulmadı. Bu çelişki göründüğü kadar derin değil:
benim verimde de Avrupa yakasının medyanı (2,14) Anadolu'nunkinin (1,08) yaklaşık iki katı, yani
betimsel olarak aynı yöndeyim. Fark sadece istatistiksel olarak anlamlı çıkmadı ve 25'e 14 ilçeyle
testin gücü zaten düşük. Ayrıca onlar erişimi yürüme mesafesiyle, ben istasyon sayısıyla ölçüyorum.
Gökçe (2024) de regresyon modelinde Avrupa yakası değişkenini anlamsız buluyor, yani bu konuda
literatür kendi içinde de tek ses değil.

Yöntem açısından en çok Zhu ve Rui (2025) ile Li ve ark. (2025) işime yarıyor. İkisi de eşitsizliği
Gini katsayısıyla tek bir sayıya indiriyor. Bu ölçüyü kendi verime uyguladım ve Gini katsayısını
0,500 buldum.

**Dikkat:** Bu sayıyı Zhu ve Rui'nin Hangzhou için bulduğu 0,425 ile doğrudan karşılaştırmıyorum.
İki çalışma farklı birim (onlar trafik analiz zonu, ben ilçe) ve farklı erişilebilirlik ölçüsü
(onlar yürüme mesafesiyle ağırlıklı erişim endeksi, ben istasyon sayısı) kullanıyor. Farklı
koşullarda hesaplanmış skorları eşdeğer saymak yaygın bir hata. Gini'yi buradan bir yöntem olarak
aldım, kıyaslanacak bir hedef değer olarak değil.

Kaynakların ortak bir sınırlılığı var ve bu benimkiyle örtüşüyor: hiçbiri sefer sıklığını, bilet
maliyetini ve yolculuk konforunu hesaba katmıyor. Öztaşkın ve Levend (2023) bunu açıkça gelecek
çalışmalara bırakıyor. Yani "ilçede istasyon var" demek "o ilçede yaşayan herkes raylı sisteme
erişebiliyor" demek değil. Benim ölçütüm de bunu ölçmüyor ve sınırlılıklar bölümünde bunu yazdım.

## 13. İlk bulgular

Aşağıdaki sayılar [`analiz/analiz.ipynb`](analiz/analiz.ipynb) not defterinin çıktısıdır. Tablolar
[`veri/islenmis/`](veri/islenmis/) klasöründe. Bunlar ön bulgu; yorumlarını #9, #10 ve #11 numaralı
Issue'larda raporlaştıracağım.

### Problem cümlesinin cevabı

**Gini katsayısı = 0,500.** Tam orantılı bir dağılımda bu sayı 0 olurdu. Değişim katsayısı 1,125,
yani 100.000 kişiye düşen istasyon sayısının standart sapması ortalamasından büyük. Erişimi en
düşük ilçelerde yaşayan nüfusun yarısı, İstanbul'daki istasyonların yalnızca **%16,8'ine** sahip.

Yani **istasyonların ilçelere dağılımı nüfusla orantılı değil.** Dağılım belirgin biçimde
dengesiz.

![Lorenz eğrisi](rapor/sekiller/sekil4_lorenz.png)

### Alt problem 1 ve 2: betimsel istatistik

| Ölçüt | Değer |
|---|---|
| Analize giren istasyon sayısı | 317 |
| Hiç istasyonu olmayan ilçe sayısı | 10 |
| 100.000 kişiye düşen istasyon, ortalama | 2,17 |
| 100.000 kişiye düşen istasyon, medyan | 1,67 |
| En yüksek | Fatih, 11,09 (39 istasyon) |
| En düşük | 10 ilçede 0,00 |

Hiç istasyonu olmayan ilçeler: Adalar, Avcılar, Beykoz, Beylikdüzü, Büyükçekmece, Esenyurt, Silivri, Sultanbeyli, Çatalca, Şile. Esenyurt dikkat
çekici: 1.003.905 kişiyle İstanbul'un en kalabalık ilçesi ve hiç raylı sistem istasyonu yok.

Erişimi en yüksek beş ilçe sırasıyla Fatih (11,09), Bakırköy (9,17), Beyoğlu (6,02), Eyüpsultan (4,94), Şişli (4,58).

![İlçelere göre raylı sistem erişimi](rapor/sekiller/sekil1_ilce_erisim.png)

### Alt problem 3 (H1): nüfus ile istasyon sayısı

Pearson r = 0,149 (p = 0,366), Spearman r = 0,267 (p = 0,100). p değerleri 0,05'ten büyük olduğu
için H0 reddedilemedi. Bu "ilişki yoktur" demek değil; bu veriyle bir ilişki gösterilemedi demek.

**Ama bu sonuç sınırda.** Aşağıdaki duyarlılık analizinde verdiğim kararları değiştirince Spearman
p değeri 0,049 ile 0,113 arasında oynuyor ve bir senaryoda 0,05'in altına iniyor. Bu yüzden H1 için
"desteklenmedi" demek yerine "bu veriyle kesin olarak gösterilemedi" diyorum.

### Alt problem 4 (H2): yakalar arası fark

| Yaka | İlçe sayısı | Ortalama | Medyan |
|---|---|---|---|
| Avrupa | 25 | 2,69 | 2,14 |
| Anadolu | 14 | 1,25 | 1,08 |

Avrupa yakasının medyanı Anadolu'nunkinin yaklaşık iki katı. Ama Mann-Whitney U testinde U = 230,0 ve
p = 0,108 çıktı, yani fark istatistiksel olarak anlamlı değil. H0 reddedilemedi. Gözlem sayısının
azlığı (25 ve 14 ilçe) bu sonuçta etkili olabilir. Bu sonuç duyarlılık analizinin tüm
senaryolarında aynı kaldı (p = 0,084 ile 0,170 arası).

### Duyarlılık analizi

Verdiğim kararların sonucu ne kadar değiştirdiğini kontrol ettim. Tam tablo
[`veri/islenmis/duyarlilik_analizi.csv`](veri/islenmis/duyarlilik_analizi.csv) dosyasında.

| Senaryo | İstasyon | Sıfır ilçe | Gini | Spearman r | Spearman p | Mann-Whitney p |
|---|---|---|---|---|---|---|
| 1. Ana analiz | 317 | 10 | 0,500 | 0,267 | 0,100 | 0,108 |
| 2. Koordinat kontrolü yok (İBB ilçe kaydı olduğu gibi) | 317 | 10 | 0,519 | 0,258 | 0,113 | 0,170 |
| 3. Koordinat her zaman kazanır (sınır payı 0 m) | 317 | 10 | 0,491 | 0,317 | 0,049 | 0,108 |
| 4. Sınır payı 500 m | 317 | 10 | 0,500 | 0,295 | 0,069 | 0,108 |
| 5. Aynı yer yarıçapı 500 m | 319 | 10 | 0,500 | 0,271 | 0,095 | 0,114 |
| 6. Aynı yer yarıçapı 2000 m | 309 | 10 | 0,500 | 0,258 | 0,113 | 0,084 |
| 7. Teleferik, füniküler, Tünel ve nostaljik tramvay hariç | 310 | 10 | 0,491 | 0,300 | 0,063 | 0,108 |

Gini katsayısı yedi senaryoda da 0,491 ile 0,519 arasında kaldı, yani "dağılım nüfusla orantılı değil" sonucu
kararlı. H2'nin sonucu da kararlı (p her zaman 0,05'in üstünde). H1'in p değeri ise 0,05 civarında
oynuyor ve bir senaryoda eşiğin altına iniyor; yani bu sonuç verdiğim kararlara bağlı. O yüzden H1
hakkında kesin bir şey söylemiyorum.

### İBB'nin ilçe kaydında yaptığım düzeltmeler

İstasyonların ilçesini koordinatla doğrulayınca 17 istasyonun ilçesi değişti (örneğin Ispartakule
Bakırköy'den Başakşehir'e, M8'in Parseller, İmes, Huzur ve Modoko istasyonları Maltepe'den Ümraniye'ye).
Tam liste ve nedenleri [`veri/README.md`](veri/README.md) dosyasında. Bu düzeltmeyi yapmasaydım Gini
0,519 çıkacaktı (senaryo 2).

### Bu sonuçlar ne anlama geliyor?

Dağılım nüfusla orantılı değil (Gini 0,500), ama bu dengesizliği açıklayan şey nüfus gibi
görünmüyor (korelasyon zayıf, ama sınırda). Literatür bunun nedenini işaret ediyor olabilir: Gökçe
(2024) istasyon çevresindeki işyeri sayısının nüfustan iki kat etkili olduğunu buluyor, Cihan ve
Üstündağ (2025) ise merkez ilçelerin sürekli avantajlı kaldığını gösteriyor. Dağılımı belirleyen şey
nüfus değil, ilçenin kent merkezine ve istihdam alanlarına göre konumu olabilir. Bu bir tahmin, bu
çalışmada sınanmadı.

## 14. Nasıl çalıştırılır

**Google Colab'da (önerilen):** Üstteki *Colab'da aç* düğmesine ya da [şu bağlantıya](https://colab.research.google.com/github/yunusyegen/istanbul-rayli-sistem-erisim/blob/main/analiz/analiz.ipynb) tıklayın,
sonra *Çalışma zamanı → Tümünü çalıştır* deyin. Defter üç veri dosyasını kaynağından kendisi indiriyor
(yaklaşık yarım dakika) ve sonuçları tek bir `sonuclar.zip` dosyası olarak indirtiyor. Hiçbir hesaba
giriş yapılmıyor, Drive'a bağlanılmıyor. İBB sunucusuna ulaşılamazsa (Colab'daki denememde İBB sunucusu zaman aşımına uğradı) defter depodaki yedek özet tabloyu (`veri/istasyon_ozet.csv`) kullanıyor ve sonuçlar aynı çıkıyor. Başka bir indirme başarısız olursa yalnızca o dosyayı elle seçmeniz isteniyor.

**Kendi bilgisayarınızda:** Depoyu klonlayın, `pip install pandas numpy scipy matplotlib shapely jupyter`
ile kütüphaneleri kurun ve `analiz/analiz.ipynb` dosyasını Jupyter'de çalıştırın. Veri dosyaları yoksa
defter `veri/ham/` klasörüne indiriyor. Sonuçlar `veri/islenmis/` ve `rapor/sekiller/` klasörlerine yazılıyor.

Defter yaklaşık 5 saniyede çalışıyor ve aynı veriyle her seferinde aynı sonucu veriyor. Boş bir
klasörde, Colab ortamını taklit ederek de çalıştırdım; üretilen tablolar ve şekiller bilgisayardaki
çalıştırmayla birebir aynı çıktı.

## 15. Klasör yapısı

```
istanbul-rayli-sistem-erisim/
├── README.md               proje özeti, bulgular ve günlük
├── veri/
│   ├── README.md           veri kaynakları, lisanslar ve indirme bağlantıları
│   ├── ilce_nufus.csv      39 ilçenin yakası ve TÜİK nüfusu
│   ├── istasyon_ozet.csv   İBB verisinin altı sütununun özeti (yedek)
│   ├── ham/                indirilen ham dosyalar (depoya yüklenmiyor)
│   └── islenmis/           ilce_erisim.csv, istasyon_listesi.csv, duyarlilik_analizi.csv
├── analiz/
│   └── analiz.ipynb        Google Colab not defteri
├── rapor/
│   ├── kaynaklar.bib       BibTeX künyeleri
│   ├── okuma_notlari.md    kaynak okuma kartları
│   └── sekiller/           4 grafik (sütun, saçılım, kutu, Lorenz)
├── uml/                    UML diyagramları (.mmd kaynak + .png)
└── sunum/                  sunum dosyaları
```

## 16. UML diyagramları

Sistemin yapısını ve işleyişini kodlamaya geçmeden önce modelledim. Üç diyagram
[`uml/`](uml/) klasöründe, ayrıntılı açıklamalarıyla birlikte: [`uml/README.md`](uml/README.md).

| Diyagram | Ne gösteriyor |
|---|---|
| [Use Case](uml/1_use_case.png) | Sistemi kimin kullandığı ve hangi işlemleri yaptığı. Aktörler: araştırmacı, analizi yeniden çalıştıran başka bir araştırmacı, veri sağlayıcı olarak İBB, TÜİK ve geoBoundaries |
| [Activity](uml/2_activity.png) | Veri indirmeden ilçe erişim tablosuna giden süreç. İstasyonun ilçesini koordinatla doğrulama kararları dahil altı karar noktası ve iki farklı bitiş (normal ve hata) içeriyor |
| [Class](uml/3_class.png) | Not defterindeki fonksiyonları sınıflara taşıyan tasarım önerisi. Kalıtım, bileşim, birleşim ve bağımlılık ilişkilerini gösteriyor |

Diyagramların kaynağı Mermaid biçiminde tutuluyor, bu yüzden metin olarak sürümlenebiliyor ve
GitHub'da doğrudan görüntüleniyor. PNG çıktıları rapora eklemek için üretildi.

Sınıf diyagramı için bir not: analiz not defteri şu an fonksiyonel yazılmış, içinde sınıf yok.
O diyagram kodu sınıflara taşıdığımda nasıl olacağını gösteren bir tasarım önerisi.

## 17. Hedef çıktı (MVP)

39 ilçe için 100.000 kişiye düşen istasyon sayısını gösteren bir tablo ve bir sütun grafiği.
Bu çıktı tamamlandı (bkz. 13. İlk bulgular).

## 18. Proje günlüğü

| Hafta | Yaptıklarım |
|---|---|
| 1 | Konu seçildi, ders planı ve değerlendirme ölçütleri incelendi |
| 2 | Git ve VS Code kuruldu, GitHub hesabı hazırlandı, problem cümlesi ve hipotezler yazıldı |
| 3 | Veri kaynakları belirlendi, İBB ve TÜİK dosyaları indirildi |
| 4 | GitHub deposu kuruldu, README yazıldı, veri temizlendi ve ilk analiz yapıldı, 15 Issue ile Kanban panosu hazırlandı, 6 kaynak okunup literatür tablosu dolduruldu, Gini katsayısı ve duyarlılık analizi eklendi |
| 5 | Use Case, Activity ve Class diyagramları hazırlandı ve depoya eklendi |
| 6 | Not defteri Colab'da tek tıkla çalışacak şekilde yeniden düzenlendi (veriyi kaynağından kendisi indiriyor). İstasyonların ilçesi koordinatla doğrulandı ve 13 belirsiz istasyon sorunu çözüldü (#6). Toplam/ortalama tablosu ve yorum eklendi. Veri güvenliği ve lisans kontrolü yapıldı. Defteri gerçek Colab'da denediğimde İBB sunucusunun zaman aşımına uğradığını gördüm, bu yüzden yedek özet tablo eklendi. Yedek yol Colab'da çalıştı |

## 19. Proje yönetimi

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

| Issue | İş | Öncelik | Durum |
|---|---|---|---|
| #6 | Birden fazla ilçeye kayıtlı 13 istasyonu koordinatla kontrol et | Must | Tamamlandı. İstasyonların ilçesi koordinatla doğrulandı |
| #7 | En az 5 güvenilir kaynak bul, oku ve literatür tablosunu doldur | Must | Review/Test: 6 kaynak bulundu, okuma sürüyor |
| #8 | Kaynakları Zotero'ya ekle ve kaynaklar.bib dosyasını üret | Must | In Progress |
| #9 | Betimsel istatistikleri yorumla (alt problem 1 ve 2) | Must | To Do |

### Sprint 2

**Hedef:** Sprint 1'den devreden literatür işleri (#7, #8, #9) bitsin, bulguların yorumu tamamlansın,
şekiller rapora uygun hâle gelsin ve LaTeX araştırma önerisi başlasın.

**Süre:** 1 hafta (son tarih 15.11.2026)

| Issue | İş | Öncelik | Durum |
|---|---|---|---|
| #16 | Colab not defterini ödev 6'ya göre tamamla | Must | Tamamlandı |
| #7 | En az 5 güvenilir kaynak bul, oku ve literatür tablosunu doldur (Sprint 1'den devir) | Must | Review/Test |
| #8 | Kaynakları Zotero'ya ekle ve kaynaklar.bib dosyasını üret (Sprint 1'den devir) | Must | In Progress |
| #9 | Betimsel istatistikleri yorumla (Sprint 1'den devir) | Must | To Do |
| #10 | H1'i yorumla: nüfus ile istasyon sayısı arasındaki ilişki | Must | Backlog |
| #11 | H2'yi yorumla: Avrupa ve Anadolu yakası karşılaştırması | Must | Backlog |
| #12 | Şekilleri rapora uygun hâle getir | Should | Backlog |
| #13 | LaTeX araştırma önerisini Overleaf'te yaz | Must | Backlog |

**Bitti sayılma koşulu (Definition of Done):** İş depoya commit edildi, Issue'daki kabul
kriterlerinin hepsi işaretlendi, not defteri baştan sona hatasız çalışıyor ve değişiklik README'ye
yansıtıldı.

## 20. Yapay zekâ kullanım beyanı

Bu projede yapay zekâ aracı olarak Claude (Anthropic) kullandım. Dersin kuralı gereği hangi işte
kullandığımı ayrıntılı yazıyorum.

**Yapay zekâyı kullandığım yerler:**

- README.md, veri/README.md ve uml/README.md dosyalarının yazılması ve düzenlenmesi
- Analiz not defterindeki Python kodunun yazılması
- İBB veri setindeki sorunların (aynı istasyonun birden çok adı, hatalı ilçeler, bozuk koordinat
  yazımı) fark edilmesi ve bunları düzelten temizleme ile koordinatla ilçe doğrulama yönteminin
  geliştirilmesi
- Literatür taramasında kaynak adaylarının aranması, tam metinlerinin indirilmesi ve künyelerin
  Crossref ile yayıncı sayfaları üzerinden doğrulanması
- Okuduğum kaynakların karşılaştırma tablosuna ve okuma notlarına aktarılmasında taslak metin
- UML diyagramlarının Mermaid kodunun yazılması
- Bulguların yorumunun taslağı

**Kendi yaptıklarım:**

- Konunun, problem cümlesinin, alt problemlerin, değişkenlerin ve hipotezlerin belirlenmesi
- Veri setlerinin İBB ve TÜİK portallarından indirilmesi
- Yapay zekânın hazırladığı metinlerin, kodun, sayıların ve yorumun okunup kontrol edilmesi ve
  benimsenmesi
- Kaynakların tam metinlerinin okunması ve tablodaki bilgilerin kaynakla karşılaştırılarak
  kontrol edilmesi

Yapay zekâ bir kaynak olmadığı için kaynakçada yer almıyor ve metinde ona atıf yapılmadı.
Kaynakçadaki bütün künyeleri DOI veya yayıncı sayfası üzerinden ayrıca doğruladım.
