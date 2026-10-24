# Veri

Bu klasörde verinin nereden geldiği ve nasıl kullanıldığı anlatılıyor.

## Klasörler

- `ham/` : Kaynaklardan indirdiğim dosyalar. Bu dosyalar depoya yüklenmiyor, çünkü biri 14 MB
  büyüklüğünde. Aşağıdaki talimatla aynısını indirebilirsiniz.
- `islenmis/` : Not defterinin ürettiği ilçe bazlı özet tablolar.
- `ilce_nufus.csv` : 39 ilçenin yakası ve TÜİK nüfusu. Elle dolduruldu.

## 1. Raylı sistem istasyon verisi (İBB)

- **Veri seti:** Raylı Sistemler İstasyon Bazlı Yolcu ve Yolculuk Sayıları
- **Adres:** https://data.ibb.gov.tr adresinde arama kutusuna "istasyon bazlı yolcu" yazın
- **Lisans:** İBB Açık Veri Lisansı
- **İndirilen dosya:** `2025-yl-rayl-sistemler-istasyon-bazl-yolcu-ve-yolculuk-saylar.csv`
- **Veri yılı:** 2025
- **İndirme tarihi:** 24.10.2026
- **Dosya büyüklüğü:** yaklaşık 14 MB, 135.783 satır
- **Ayraç:** noktalı virgül (`;`)

Dosyayı indirdikten sonra adını `istasyon_verisi.csv` yapıp `ham/` klasörüne koyun.

Dosyadaki sütunlar:

| Sütun | Açıklama | Projede kullanıldı mı? |
|---|---|---|
| `transaction_year`, `transaction_month`, `transaction_day` | İşlem tarihi | Hayır |
| `line` | Hat adı | Evet (kontrol için) |
| `station_name` | İstasyon adı | Evet |
| `station_number` | İstasyon kodu | Hayır |
| `town` | İstasyonun bulunduğu ilçe | Evet |
| `longitude`, `latitude` | Konum | Hayır |
| `passage_cnt`, `passanger_cnt` | Geçiş ve yolcu sayısı | Hayır |

Bu projede yolcu sayısı değil, istasyonun hangi ilçede olduğu kullanılıyor.

### Veride fark ettiğim sorunlar

Dosyayı açtığımda sayımı etkileyen üç durum gördüm. Bunları not ediyorum, çünkü analizde
düzeltilmeleri gerekiyor:

1. **Aynı istasyon birden çok adla yazılmış.** Marmaray'da `Sirkeci-1`, `Sirkeci-2`, `Sirkeci-3`,
   `Sirkeci-4` ayrı ayrı geçiyor. Aynı şey `Üsküdar-1..3`, `Yenikapı-1..3`, `Bakırköy-1..2` için de
   geçerli. M7'de ise `MAHMUTBEY M7 HOL 1` ve `HOL 2` var. Bunlar aynı istasyonun farklı
   girişleri. Hepsini tek istasyon saymazsam bazı ilçelerin istasyon sayısı olduğundan fazla çıkıyor.
2. **Bazı istasyonlar yanlış ilçeye yazılmış.** Örneğin `MAHMUTBEY M7 HOL 1` hem Bağcılar hem
   Esenyurt hem Fatih olarak geçiyor. Bir istasyonu en çok hangi ilçeyle kaydedilmişse o ilçeye
   sayıyorum.
3. **Boş ilçe alanı olan satırlar var.** Bunlar sayıma katılmıyor.

Ayrıca veri setinde Kocaeli'ne bağlı Gebze, Darıca ve Çayırova istasyonları da bulunuyor. Bunlar
Marmaray hattının İstanbul dışında kalan durakları. İstanbul ilçesi olmadıkları için analiz dışında
bırakıldılar.

## 2. İlçe nüfusları (TÜİK)

- **Kaynak:** TÜİK, Adrese Dayalı Nüfus Kayıt Sistemi Sonuçları
- **Tablo:** İl ve İlçelere Göre İl/İlçe Merkezi, Belde/Köy Nüfusu (DF_ADNKS_T22)
- **Adres:** https://data.tuik.gov.tr
- **Yıl:** 2025
- **Kullanılan değer:** Yerleşim yeri türü "Toplam". İstanbul'da belde ve köy nüfusu olmadığı için
  toplam nüfus, ilçe merkezi nüfusuna eşit çıkıyor.
- **Kontrol:** 39 ilçenin toplamı 15.754.053 kişi. Bu sayı TÜİK'in 2025 İstanbul toplamıyla aynı,
  yani eksik ya da fazla ilçe yok.

`ilce_nufus.csv` dosyasındaki `nufus` sütunu bu kaynaktan elle dolduruldu. `yaka` sütununu kendim
ekledim: Avrupa yakasında 25, Anadolu yakasında 14 ilçe var.

## 3. Not defterinin ürettiği dosyalar

| Dosya | Açıklama |
|---|---|
| `islenmis/ilce_erisim.csv` | İlçe, yaka, nüfus, istasyon sayısı ve 100.000 kişiye düşen istasyon sayısı |
