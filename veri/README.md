# Veri

Bu klasörde verinin nereden geldiği ve nasıl kullanıldığı anlatılıyor.

## Klasörler

- `ham/` : Kaynaklardan indirilen dosyalar. Bu dosyalar depoya yüklenmiyor (biri 14 MB, biri 16 MB).
  Not defteri bunları kaynağından kendisi indiriyor. Elle indirmek isterseniz aşağıdaki
  bağlantıları kullanın.
- `islenmis/` : Not defterinin ürettiği tablolar (bkz. 4. bölüm).
- `ilce_nufus.csv` : 39 ilçenin yakası ve TÜİK nüfusu. Elle dolduruldu.
- `istasyon_ozet.csv` : İBB dosyasının analizde kullanılan altı sütununun, aynı değerlere sahip satır
  sayılarıyla özetlenmiş hâli (135.783 satır yerine 382 satır, 33 KB). İBB sunucusuna ulaşılamazsa not
  defteri bunu kullanıyor.

## 1. Raylı sistem istasyon verisi (İBB)

- **Veri seti:** Raylı Sistemler İstasyon Bazlı Yolcu ve Yolculuk Sayıları
- **Veri sağlayıcı:** İBB Bilgi İşlem Dairesi Başkanlığı
- **Veri seti sayfası:** https://data.ibb.gov.tr/dataset/rayli-sistemler-istasyon-bazli-yolcu-ve-yolculuk-sayilari
- **Lisans:** İBB Açık Veri Lisansı. Metni: https://data.ibb.gov.tr/license
- **İndirilen dosya:** `2025-yl-rayl-sistemler-istasyon-bazl-yolcu-ve-yolculuk-saylar.csv`
- **Doğrudan indirme bağlantısı:** https://data.ibb.gov.tr/dataset/ae3b2e4b-073a-48d0-8ef3-f28f19bcb19c/resource/cce8e138-686a-4b8d-bac0-c2a0ab294a6e/download/2025-yl-rayl-sistemler-istasyon-bazl-yolcu-ve-yolculuk-saylar.csv
- **Veri yılı:** 2025
- **Portaldaki kaydın son güncellenme tarihi:** 03.02.2026
- **İndirme tarihi:** 24.10.2026
- **Dosya büyüklüğü:** yaklaşık 14 MB, 135.783 satır
- **Ayraç:** noktalı virgül (`;`)

Dosyayı elle indirirseniz adını `istasyon_verisi.csv` yapıp `ham/` klasörüne koyun.

Dosyadaki sütunlar:

| Sütun | Açıklama | Projede kullanıldı mı? |
|---|---|---|
| `transaction_year`, `transaction_month`, `transaction_day` | İşlem tarihi | Hayır |
| `line` | Hat adı | Evet |
| `station_name` | İstasyon adı | Evet |
| `station_number` | İstasyon kodu | Evet (aynı istasyonun salonlarını ve farklı yerlerdeki aynı adları ayırmak için) |
| `town` | İBB'nin yazdığı ilçe | Evet (koordinatla doğrulanarak) |
| `longitude`, `latitude` | Konum | Evet (ilçeyi doğrulamak için) |
| `passage_cnt`, `passanger_cnt` | Geçiş ve yolcu sayısı | Hayır |

Bu projede yolcu sayısı değil, istasyonun kendisi kullanılıyor: adı, hattı, kodu, İBB'nin yazdığı
ilçe ve koordinatı. Dosyada kişiye ait bilgi yok: kayıtlar istasyon ve gün bazında toplulaştırılmış
sayılar ile istasyon konumlarından oluşuyor. Ad, kimlik, adres gibi bir alan bulunmuyor.

**Yedek özet tablo.** Not defterini Colab'da denediğimde İBB sunucusu dört denemede de zaman aşımına
uğradı (`URLError: <urlopen error timed out>`), oysa bilgisayarımdan aynı adres bir saniyede açılıyor.
Nedenini bilmiyorum: bazı kurumsal sunucular yurt dışındaki bulut ortamlarından gelen bağlantıları
kabul etmiyor olabilir, ama bunu doğrulayamadım. Hoca da defteri Colab'dan çalıştıracağı için tek bir
sunucuya bağımlı kalmamak istedim. Yedek yol Colab'da gerçekten çalıştı: İBB zaman aşımına uğradıktan
sonra defter özet tabloyu indirip devam etti. `istasyon_ozet.csv`, İBB dosyasındaki altı sütunu (`station_name`, `town`, `line`,
`station_number`, `longitude`, `latitude`) ve her değer kombinasyonunun kaç satırda geçtiğini (`satir_sayisi`)
içeriyor. Yolcu sayıları ve tarihler yok, bu yüzden kişiye ait bilgi de yok. Not defteri bu tabloyu çoğaltıp
ham tabloyu geri kuruyor ve sonuçların aynı çıktığını iki yolla doğruladım: tablonun geri kurulmuş hâli ham
dosyayla her satır için birebir aynı, iki çalıştırmanın çıktı dosyaları da bayt bayt aynı. İBB Açık Veri
Lisansı kopyalamaya ve uyarlamaya kaynak gösterilerek izin verdiği için bu özeti depoya koydum (5. bölüm).

### Veride fark ettiğim sorunlar

Dosyayı incelerken sayımı bozan beş durum gördüm. Hepsini not defterinin 2. ve 3. adımında ele alıyorum.

1. **Aynı istasyon birden çok adla yazılmış.** Marmaray'da `Sirkeci-1`, `Sirkeci-2`, `Sirkeci-3`,
   `Sirkeci-4` ayrı ayrı geçiyor. Aynı şey `Üsküdar-1..3`, `Yenikapı-1..3`, `Bakırköy-1..2` için de
   geçerli. M7'de ise `MAHMUTBEY M7 HOL 1` ve `HOL 2` var. Bunlar aynı istasyonun farklı girişleri ya
   da salonları. Sondaki `-1`, `HOL 1` gibi ekleri silip adı büyük harfe çevirerek birleştirdim.
2. **Bazı satırların istasyon adı ve kodu boş.** 728 satır, iki nostaljik tramvay hattına ait (T3
   Kadıköy-Moda ve Taksim-Tünel nostaljik tramvayı). Bunları atmak yerine hattın adıyla "adsız
   istasyon" olarak tuttum, çünkü ortada gerçek bir istasyon var.
3. **İlçe sütunu her istasyonda güvenilir değil.** M8 hattının Ümraniye'deki istasyonları (Parseller,
   İmes, Huzur, Modoko) "Maltepe", Ispartakule "Bakırköy", Kayaşehir Merkez "Bağcılar" yazılmış.
   Ayrıca farklı yerlerdeki aynı isimli istasyonlar da var: Marmaray'ın Zeytinburnu istasyonu ile
   M1'in Zeytinburnu istasyonu birbirinden yaklaşık 2,2 km uzakta.
4. **Koordinat sütununun yazımı bozuk.** Aynı sütunda `289.335.555.555.556`, `28.748.805`, `29.097`
   gibi değişik uzunlukta yazımlar var. Noktalar binlik ayracı gibi kullanılmış, asıl ondalık nokta
   kaybolmuş. Üstelik bazı değerler Excel'de bozulmuş: `29.Eyl` (Excel koordinatı tarih sanıp "Eylül"
   yapmış) ve `29.0` gibi yuvarlanmış yer tutucular var. İlk iki rakam her zaman tam kısım olduğu için
   (28 ya da 29 boylam, 40 ya da 41 enlem), ilk iki rakamdan sonra ondalık nokta koyarak gerçek dereceyi
   buldum (`289.335.555.555.556` → 28,9335555555556). 5 rakamdan kısa olan ve tarihe dönüşen
   değerleri kullanmadım.
5. **Kocaeli istasyonları.** Veri setinde Kocaeli'ne bağlı Gebze, Darıca ve Çayırova istasyonları da
   bulunuyor. Bunlar Marmaray hattının İstanbul dışında kalan durakları. İstanbul ilçesi olmadıkları için
   analiz dışında bırakıldılar.

### İlçeyi nasıl belirledim?

Dosyadaki ilçe sütununa körü körüne güvenemediğim için her istasyonu koordinatıyla ilçe sınırlarına
karşılaştırdım (sınırlar için 3. bölüm). Üç kural kullandım:

1. **Aynı yer:** Adı aynı olan ve birbirine 1000 m'den yakın kodlar tek istasyon sayıldı. Aynı
   kompleksin salonları birbirine en fazla yaklaşık 560 m uzaklıkta, gerçekten farklı yerlerdeki aynı
   adlar ise en az yaklaşık 1,2 km uzaklıkta; 1000 m bu boşluğun içinde.
2. **İlçe:** Koordinatı olan istasyonun ilçesi, koordinatın düştüğü ilçedir. Koordinatı olmayan
   istasyonlarda İBB'nin yazdığı ilçe kullanıldı.
3. **İBB'ye güven payı:** Koordinat, İBB'nin yazdığı ilçenin sınırına 200 m'den yakınsa İBB'nin kaydı
   değiştirilmedi, çünkü sınır dosyasının ve koordinatın küçük hataları olabilir.

Sonuç: 322 istasyondan 234 tanesinde koordinat İBB'nin ilçesiyle aynı çıktı, 56 tanesinin
koordinatı yok ya da kullanılamıyor (İBB'nin kaydı kullanıldı), 10 tanesi sınır boyunda olduğu için
İBB'nin kaydı korundu ve 22 tanesinde koordinat farklı bir ilçeyi gösteriyordu; bunların
17 tanesi İstanbul içinde (5 tanesi Kocaeli'ndeki Marmaray durakları). Düzeltilen 17
istasyon 6. bölümde, sınır boyunda korunan 10 istasyon 7. bölümde listeli.

## 2. İlçe nüfusları (TÜİK)

- **Kaynak:** TÜİK, Adrese Dayalı Nüfus Kayıt Sistemi Sonuçları
- **Tablo:** İl ve İlçelere Göre İl/İlçe Merkezi, Belde/Köy Nüfusu (DF_ADNKS_T22)
- **Adres:** https://veriportali.tuik.gov.tr (eski adres `data.tuik.gov.tr` bu adrese yönlendiriyor)
- **Kullanım koşulu:** TÜİK'in yasal uyarı sayfası, kurumun verilerinin kaynak gösterilerek ayrıca
  izin almaya gerek olmadan yeniden kullanılabileceğini söylüyor: https://www.tuik.gov.tr/Kurumsal/Yasal_Uyari
- **Yıl:** 2025
- **Kullanılan değer:** Yerleşim yeri türü "Toplam". İstanbul'da belde ve köy nüfusu bulunmadığından
  toplam nüfus, ilçe merkezi nüfusuna eşit çıkıyor.
- **Kontrol:** 39 ilçenin toplamı 15.754.053 kişi. Bu sayı TÜİK'in 2025 İstanbul toplamıyla aynı,
  yani eksik ya da fazla ilçe yok.

`ilce_nufus.csv` dosyasındaki `nufus` sütunu bu kaynaktan elle dolduruldu. Depoya TÜİK dosyasının
tamamı değil, yalnızca bu tablodan alınan 39 ilçenin toplam nüfus değeri konuldu. `yaka` sütununu
kendim ekledim: Avrupa yakasında 25, Anadolu yakasında 14 ilçe var.

## 3. İlçe sınırları (geoBoundaries, OpenStreetMap kaynaklı)

- **Amaç:** İstasyon koordinatlarının hangi ilçeye düştüğünü bulmak.
- **Kaynak:** geoBoundaries, gbOpen sürümü, Türkiye ilçe (ADM2) sınırları. Sağlayıcının kayıt
  bilgisine göre kaynak veri OpenStreetMap (OSM Boundaries), sınır yılı 2021. Dosyadaki 973 ilçeden
  yalnızca İstanbul ve komşuları kullanıldı.
- **Adres:** https://www.geoboundaries.org/
- **Kayıt bilgisi:** https://www.geoboundaries.org/api/current/gbOpen/TUR/ADM2/
- **Dosya adresi (Git LFS):** https://media.githubusercontent.com/media/wmgeolab/geoBoundaries/9469f09592ced973a3448cf66b6100b741b64c0d/releaseData/gbOpen/TUR/ADM2/geoBoundaries-TUR-ADM2.geojson
- **Lisans:** Sağlayıcının kayıt bilgisinde Open Data Commons Open Database License (ODbL) 1.0
  yazıyor. Metni: https://opendatacommons.org/licenses/odbl/1-0/
- **Atıf:** © OpenStreetMap contributors (https://www.openstreetmap.org/copyright). Runfola, D. ve ark. (2020). geoBoundaries: A global
  database of political administrative boundaries. *PLOS ONE*, 15(4), e0231866. https://doi.org/10.1371/journal.pone.0231866

Sınır dosyası depoya yüklenmedi, not defteri indiriyor. Depodaki tablolar sınır geometrisini
içermiyor, yalnızca bir istasyonun hangi ilçeye düştüğü bilgisini içeriyor. Sınırlar resmî değil
OpenStreetMap kaynaklı olduğu için birkaç on metre sapabilir.

## 4. Not defterinin ürettiği dosyalar

| Dosya | Açıklama |
|---|---|
| `islenmis/ilce_erisim.csv` | İlçe, yaka, nüfus, istasyon sayısı ve 100.000 kişiye düşen istasyon sayısı |
| `islenmis/istasyon_listesi.csv` | Analize giren 322 istasyonun her biri: ilçesi, İBB'nin yazdığı ilçe, ilçe kararının dayanağı, sınıra uzaklık, kodları ve hatları |
| `islenmis/duyarlilik_analizi.csv` | Verdiğim kararları değiştirince sonucun nasıl değiştiği (7 senaryo) |
| `istasyon_ozet.csv` | İBB dosyasındaki altı sütunun satır sayılarıyla özeti. İBB dosyası okunduğunda defter bunu yeniden üretiyor |

## 5. Kaynak gösterimi, lisans ve paylaşım özeti

**Atıflar**

- İstasyon verisi: İBB Bilgi İşlem Dairesi Başkanlığı. *Raylı Sistemler İstasyon Bazlı Yolcu ve
  Yolculuk Sayıları* (2025). İBB Açık Veri Portalı, İBB Açık Veri Lisansı.
  https://data.ibb.gov.tr/dataset/rayli-sistemler-istasyon-bazli-yolcu-ve-yolculuk-sayilari
- Nüfus verisi: Türkiye İstatistik Kurumu. *Adrese Dayalı Nüfus Kayıt Sistemi Sonuçları, 2025*
  (il ve ilçelere göre nüfus tablosu, DF_ADNKS_T22). TÜİK Veri Portalı.
  https://veriportali.tuik.gov.tr
- İlçe sınırları: © OpenStreetMap contributors; geoBoundaries (Runfola ve ark., 2020), ODbL 1.0.
  https://www.geoboundaries.org/

**Lisans koşulları (kaynaklarının sayfalarında okuduğum hâliyle)**

- İBB Açık Veri Lisansı, kaynak gösterilmesi şartıyla veriyi kopyalamaya, yayımlamaya ve
  uyarlamaya izin veriyor. Verideki kişisel verileri kapsam dışı bırakıyor ve veri sağlayıcının
  çalışmayı onayladığı izlenimi verilmesine izin vermiyor. Metin: https://data.ibb.gov.tr/license
- TÜİK'in yasal uyarı sayfası, kurumun verilerinin kaynak gösterilerek izin almadan yeniden
  kullanılabileceğini söylüyor. Metin: https://www.tuik.gov.tr/Kurumsal/Yasal_Uyari
- ODbL 1.0, kaynak (© OpenStreetMap contributors) gösterilmesi şartıyla veriyi kullanmaya ve
  paylaşmaya izin veriyor. Metin: https://opendatacommons.org/licenses/odbl/1-0/

Bu çalışma İBB, TÜİK, OpenStreetMap ya da geoBoundaries tarafından hazırlanmamış ya da onaylanmamıştır.
Sonuçların sorumluluğu bana aittir ve bu kurumların görüşünü yansıtmaz.

**Depoda ne var, ne yok**

| Dosya | Depoda mı? | Neden |
|---|---|---|
| `ham/istasyon_verisi.csv` | Hayır | Boyutu 14 MB. Yukarıdaki bağlantıdan kaynağından indirilebilir. Yerine özeti depoda |
| `istasyon_ozet.csv` | Evet | İBB dosyasının altı sütununun özeti (33 KB), kaynak gösterilerek. İBB sunucusuna ulaşılamazsa kullanılıyor |
| `ham/tuik_ilce_nufus.csv` | Hayır | TÜİK dosyasının tamamı yeniden yayımlanmıyor |
| `ham/ilce_sinirlari.geojson` | Hayır | Boyutu 16 MB ve başkasının verisi. Not defteri kaynağından indiriyor |
| `ilce_nufus.csv` | Evet | TÜİK'ten alınan 39 ilçenin toplam nüfus değeri, kaynak gösterilerek |
| `islenmis/*.csv` | Evet | Bu kaynaklardan kendi hesapladığım tablolar, kaynak gösterilerek |

**Kişisel veri ve gizli bilgi**

- Üç veri setinde de kişiye ait bilgi yok.
- Depoda ve not defterinde şifre, API anahtarı ya da erişim anahtarı yok. Not defteri Google
  Drive'a bağlanmıyor; veriyi açık adreslerden indiriyor, hiçbir hesaba giriş yapmıyor.
  İleride bir anahtar gerekirse Colab'ın Secrets özelliği kullanılacak.
- Depodaki dosyalar ve not defterinin çıktı hücreleri paylaşmadan önce taranarak kişisel yol,
  e-posta ve öğrenci numarası gibi bilgilerin bulunmadığı doğrulandı.

## 6. İlçesi koordinata göre düzeltilen istasyonlar

İBB'nin ilçe sütunu ile koordinat çelişiyor ve koordinat İBB'nin yazdığı ilçenin sınırından 200 m'den
fazla uzakta olduğu için ilçesini değiştirdiğim 17 istasyon:

| İstasyon | İBB'nin yazdığı ilçe | Koordinata göre ilçe | İBB ilçesinin sınırına uzaklık (m) |
|---|---|---|---|
| Ispartakule | Bakırköy | Başakşehir | 10.486 |
| Haznedar | Bağcılar | Bahçelievler | 1.706 |
| İlkyuva | Bağcılar | Bahçelievler | 733 |
| Kayaşehir Merkez | Bağcılar | Başakşehir | 6.632 |
| Haliç Güney | Fatih | Beyoğlu | 239 |
| Haliç Kuzey | Fatih | Beyoğlu | 239 |
| Alibeyköy Metro | Fatih | Eyüpsultan | 4.124 |
| Mahmutbey M7 | Güngören | Bağcılar | 3.705 |
| Mevlana | Maltepe | Ataşehir | 1.409 |
| Huzur | Maltepe | Ümraniye | 4.656 |
| Modoko Keyap | Maltepe | Ümraniye | 2.950 |
| Parseller | Maltepe | Ümraniye | 5.616 |
| İmes | Maltepe | Ümraniye | 2.225 |
| Atatürk Oto Sanayi Güney | Şişli | Sarıyer | 3.986 |
| Atatürk Oto Sanayi Kuzey | Şişli | Sarıyer | 3.986 |
| İTÜ Güney | Şişli | Sarıyer | 2.772 |
| İTÜ Kuzey | Şişli | Sarıyer | 2.772 |

## 7. Sınır boyunda İBB'nin kaydını koruduğum istasyonlar

Koordinat başka bir ilçeyi gösterse de İBB'nin yazdığı ilçenin sınırına 200 m'den yakın olduğu için
İBB'nin kaydını değiştirmediğim 10 istasyon:

| İstasyon | Kullandığım ilçe | İBB ilçesinin sınırına uzaklık (m) |
|---|---|---|
| Boğaziçi | Sarıyer | 19 |
| Merter | Güngören | 14 |
| Taşköprü | Bayrampaşa | 11 |
| Baştabya | Esenler | 9 |
| Ümraniye | Üsküdar | 9 |
| Çukurçeşme | Bayrampaşa | 4 |
| Cumhuriyet | Esenler | 3 |
| Keresteciler | Güngören | 3 |
| Mehmetakif | Güngören | 2 |
| T4 Kiptaş Venezia | Gaziosmanpaşa | 0 |
