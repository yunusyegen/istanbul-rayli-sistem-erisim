# Okuma notları

Okuduğum her kaynak için bir kart tutuyorum. Kartlar dolunca README'deki karşılaştırma
tablosuna kısaltarak aktarıyorum.

## Nerede ne aranır?

| Ne arıyorum | Makalenin neresinde | Ctrl+F ile aranacak kelimeler |
|---|---|---|
| Problem | Giriş bölümünün son paragrafı | amaç, bu çalışmada, bilinmemektedir, aim, objective |
| Veri | Yöntem bölümünün başı | veri, veri seti, materyal, data, dataset, TÜİK, İBB |
| Yöntem | Yöntem bölümü | yöntem, analiz, method, korelasyon, regresyon, CBS, GIS |
| Temel bulgu | Özetin son cümleleri ve Sonuç bölümü | bulgu, sonuç, result, finding, %, p =, r = |
| Sınırlılık | Tartışma ve Sonuç bölümünün sonu | sınırlılık, limitation, gelecek çalışma, future research |
| Projeme katkısı | Hiçbir yerde. Bunu ben yazarım. | - |

## Üç geçişli okuma

1. **Birinci geçiş (10 dakika):** Başlık, özet, sonuç. Soru: bu makale benim soruma cevap veriyor
   mu? Vermiyorsa bırak.
2. **İkinci geçiş:** Yöntem bölümü. Hangi veriyi hangi analizle incelemişler?
3. **Üçüncü geçiş:** Tartışma ve sınırlılıklar. Neyi yapamamışlar?

---

## 1. Öztaşkın ve Levend (2023)

Toplu Taşıma Duraklarının Erişilebilirliği: İstanbul Örneği.
*Türk Uzaktan Algılama ve CBS Dergisi*, 4(2), 301-318. doi:10.48123/rsgis.1299707

- **Problem:** İstanbul'un toplu taşıma sistemi sürdürülebilir değil ve yazarlara göre bunun temel
  nedeni duraklara erişimin yetersiz olması. Türkiye'de erişilebilirlik üzerine bilimsel çalışma az.
- **Veri:** İBB Ulaşım Dairesi'nden alınan hat ve durak verisi (yaklaşık 15.000 lastik tekerlekli
  durak, raylı sistem istasyonları, deniz iskeleleri) ve 2020 yılına ait, her binada kaç kişi
  yaşadığını gösteren bina verisi. Toplam nüfus 15.462.452.
- **Yöntem:** CBS. ArcGIS Network Analyst'teki Servis Alanı Analizi ile her durağın 0-5, 5-10 ve
  10-15 dakikalık yürüme mesafesindeki alanı çıkarılmış, sonra bu alanda kalan binalardaki nüfus
  toplanmış. Yazarlar tampon (buffer) analizi yerine servis alanı analizini seçtiklerini, bunun daha
  nesnel olduğunu belirtiyor.
- **Temel bulgu:** Lastik tekerlekli duraklara nüfusun %89,87'si 5 dakikada ulaşıyor. Raylı sistem
  istasyonlarına 5 dakikada ulaşan oran yalnızca %2,88, 15 dakikaya kadar çıkınca %32,58. Deniz
  iskelelerinde bu oran %0,17. Avrupa yakasında oturanların raylı sisteme erişimi Anadolu
  yakasındakilerden daha iyi. M4 Kadıköy-Tavşantepe hattının istasyonlarına erişim, hat E-5'e
  paralel gittiği için zayıf.
- **Sınırlılık:** Yalnızca fiziksel ve mekânsal erişim ölçülmüş. Yazarlar konfor, maliyet ve sefer
  sıklığı gibi ölçütlerin analize girmediğini, gelecek çalışmaların bunları da içermesi gerektiğini
  söylüyor.
- **Projeme katkısı:** Avrupa ile Anadolu yakası arasındaki farkı benim gibi sorguluyor ama erişimi
  yürüme mesafesiyle ölçüyor, ben istasyon sayısıyla ölçüyorum. İkisinin farkını tartışma bölümünde
  yazacağım. Sefer sıklığını ölçememe sınırlılığı benimkiyle birebir aynı, bunu sınırlılıklar
  bölümünde kaynak göstererek kullanacağım.

---

## 2. Gökçe (2024)

Büyüyen Raylı Toplu Taşıma Sistem Ağında Hatlar ve İstasyonlar: İstanbul Örneği.
*METU Journal of the Faculty of Architecture*, 41(1), 1-21. doi:10.4305/METU.JFA.2024.1.1

- **Problem:** İstanbul'un raylı sistem ağı hızla büyüyor. Ağa eklenen her istasyonun yolcu sayısına
  katkısı, istasyonun ağdaki konumuna (düğüm özelliği) ve yakın çevresine (yer özelliği) göre
  değişiyor. Yazar, bu değişimi zaman içinde inceleyen bir çalışma olmadığını söylüyor.
- **Veri:** 186 istasyona ait beş zaman noktasında (2013, 2015, 2017, 2019, 2022) aralık ayı ikinci
  haftasının yolcu sayıları, toplam 745 gözlem. Her istasyonun 1 km yarıçapındaki nüfus ve işyeri
  sayısı. İstanbul il sınırları dışındaki Marmaray istasyonları (Gebze-Tuzla) modele alınmamış.
- **Yöntem:** Rastgele etkiler panel veri doğrusal regresyonu. Bağımlı değişken yolcu sayısının
  doğal logaritması. Bağımsız değişkenler: 1 km'deki nüfus ve işyeri sayısı, raylı sisteme transfer
  sayısı, metrobüs transferi, istasyon sırası, hat tipi, Avrupa yakasında olma, güney-kuzey hattı
  olma.
- **Temel bulgu:** İstasyon çevresindeki nüfusun %1 artması yolcu sayısını yalnızca %0,10 artırıyor.
  İşyeri sayısının %1 artması ise %0,20 artırıyor, yani iki katı etkili. En güçlü etken transfer
  olanağı (katsayı 0,910). Avrupa yakasında olmak anlamlı bir fark yaratmıyor (t = 0,68).
  Model R² = 0,401. Yazarın kendi cümlesi: nüfusla paralel yolcu artışı olmadığı görülüyor.
- **Sınırlılık:** Panel veri setinde yıllara göre eksik gözlemler var ve yazar bunun model
  kalitesini etkileyebileceğini belirtiyor. Ayrıca bazı gözlemsel etkilerin modelle
  yakalanamadığını söylüyor.
- **Projeme katkısı:** İki bulgusu benim sonuçlarımı destekliyor. Birincisi, nüfusla raylı sistem
  kullanımı paralel artmıyor; ben de nüfus ile istasyon sayısı arasında anlamlı ilişki bulamadım.
  İkincisi, Avrupa yakası değişkeni anlamlı çıkmıyor; benim H2 testim de iki yaka arasında anlamlı
  fark bulmadı. Ayrıca İstanbul dışındaki Marmaray istasyonlarını dışarıda bırakma kararı benim
  veri temizliğimle aynı, bu da kararımın yerinde olduğunu gösteriyor.

---

## 3. Cihan ve Üstündağ (2025)

A Sustainable Accessibility Approach in Transportation Planning: The Case of Istanbul.
*Planlama Dergisi*, 35(3), 343-363. doi:10.14744/planlama.2025.90958

- **Problem:** İstanbul'da toplu taşımayla istihdama erişimin bugünkü düzeyi ve planlanan ulaşım
  yatırımları tamamlandığında ne olacağı bilinmiyor. Yazarlar ayrıca bu erişimin mekânsal olarak
  adil olup olmadığını soruyor.
- **Veri:** İstanbul Ulaşım Ana Planı kapsamında yapılan anketler ve İBB Ulaşım Planlama Şube
  Müdürlüğü'nün dört aşamalı ulaşım modeli. 1307 trafik analiz zonu (TAZ), 2022 yılı istihdam
  verisi ve bütün planlanan yatırımların bittiği varsayılan 2040 senaryosu.
- **Yöntem:** Kümülatif olanaklar yöntemi. 30, 60 ve 90 dakikalık seyahat süresi eşiklerinde her
  TAZ'dan ulaşılabilen istihdam miktarı hesaplanmış ve CBS ortamında haritalanmış.
- **Temel bulgu:** 60 dakikada istihdama erişim ortalaması 2022'de %24,41 iken 2040 senaryosunda
  %32,55'e çıkıyor. 90 dakikalık eşikte en düşük değer belirgin biçimde iyileşiyor. Ama 30 dakikalık
  eşikte en düşük değer hiç değişmiyor, yani bazı çeper bölgelerde kısa sürede işe ulaşmak hâlâ
  mümkün değil. Fatih, Şişli, Beşiktaş ve Kadıköy gibi merkez ilçeler sürekli yüksek skor alıyor.
- **Sınırlılık:** Kümülatif olanaklar yönteminde bütün olanaklar eşit ağırlıklı sayılıyor. Yazarlar
  bunu yöntemin önemli bir sınırlılığı olarak belirtiyor.
- **Projeme katkısı:** Merkez ilçelerin yüksek, çeper ilçelerin düşük çıkması benim tablomla birebir
  örtüşüyor. Fatih, Şişli, Beşiktaş ve Kadıköy benim 100.000 kişiye düşen istasyon sıralamamda da
  üst sıralarda. Ayrıca erişimi "işe kaç dakikada gidiyorum" diye ölçmeleri, benim istasyon
  saymamın ne kadar kaba bir ölçüt olduğunu gösteriyor; bunu sınırlılıklarıma ekleyeceğim.

---

## 4. Zhu ve Rui (2025)

Spatiotemporal Dynamics and Multi-Scale Equity Evaluation of Urban Rail Accessibility:
Evidence from Hangzhou. *ISPRS International Journal of Geo-Information*, 14(9), 361.
doi:10.3390/ijgi14090361

- **Problem:** Metro ağları hızla büyürken hizmetin mekânsal olarak eşit dağılıp dağılmadığı iyi
  ölçülemiyor. Yazarlara göre mevcut yöntemlerin üç eksiği var: gerçek yol ağını hesaba katmamak,
  tek bir ölçekte bakmak ve eşitliği sayısallaştıran bir mekanizmadan yoksun olmak.
- **Veri:** Hangzhou'nun merkez kentsel alanı. 2019 ve 2023 yıllarına ait metro ağı, yol ağı
  topolojisi ve nüfus dağılımı verisi. Üç ölçekte bakılmış: sokak, 500x500 metre grid ve TAZ.
- **Yöntem:** Yürüme yollarını ve mesafeyle azalmayı hesaba katan ağ tabanlı tampon azalma modeliyle
  her istasyonun hizmet nüfusu hesaplanmış. Eşitlik ölçümü için Gini katsayısı ve Lorenz eğrisi,
  ayrıca küresel ve yerel mekânsal otokorelasyon (Moran's I), ağırlık merkezi kayması ve standart
  sapma elipsi kullanılmış.
- **Temel bulgu:** Ağ 3 hattan 12 hatta çıkınca TAZ ölçeğinde Gini katsayısı 0,56'dan 0,425'e
  düşmüş, yani eşitsizlik azalmış. Ama 500 metrelik grid ölçeğinde Gini 0,404'te kalmış. Merkez
  "yüksek-yüksek", çeper "düşük-düşük" kümeler oluşturuyor. Yazarların sonucu: eşitliği artırmak
  için ağı büyütmek tek başına yetmiyor.
- **Sınırlılık:** Makalede ayrı bir sınırlılık bölümü yok. Kendi gördüğüm sınırlılıklar: tek bir
  şehir ve yalnızca iki yıl inceleniyor. Yazarlar tartışma bölümünde, kullandıkları erişilebilirlik
  endeksinin yürüme mesafesi ve sefer sıklığını tek çerçevede birleştirdiği için merkezi alanları
  yapısal olarak kayırdığını kendileri söylüyor.
- **Projeme katkısı:** "Nüfusla orantılı mı" sorusunu tek bir sayıyla cevaplamanın yolunu
  gösteriyor: Gini katsayısı ve Lorenz eğrisi. Benim 100.000 kişiye düşen istasyon sayım 39 ilçeye
  yayılmış bir dağılım, bu dağılımın eşitsizliğini Gini ile ölçebilirim. Projenin sonraki aşamasına
  bunu ekleyeceğim.

---

## 5. Li ve ark. (2025)

Study on Spatial Distribution and Inequity of Rail Transit Travel Accessibility under
Multi-modal Traveling: A Case Study of Beijing. *Scientific Reports*, 15(1), 15823.
doi:10.1038/s41598-025-97066-4

- **Problem:** Pekin'de raylı sistem istasyonu çevrelerinin erişilebilirliği ile nüfus yoğunluğu
  arasındaki uyumsuzluk ve bu dağılımın adil olup olmadığı.
- **Veri:** Pekin'in 6. Çevre Yolu içinde kalan alan. Gaode Map servis API'sinden dört ulaşım türü
  (yürüme, bisiklet, otomobil, toplu taşıma) için seyahat süreleri, istasyon konumları ve nüfus
  dağılımı verisi.
- **Yöntem:** Gauss tabanlı iki aşamalı yüzen hareketli alan yöntemiyle (2SFCA) erişilebilirlik
  hesaplanmış. Eşitlik için Gini katsayısı, iki değişkenli yerel mekânsal korelasyon ve
  Önem-Performans Analizi (IPA) kullanılmış.
- **Temel bulgu:** Kent merkezinde ve alt merkezlerde erişim bütün ulaşım türlerinde diğer
  bölgelerden yüksek. Gini katsayısına göre erişim en adil otomobil ve bisikletle, en adaletsiz
  yürüyerek ve toplu taşımayla. Bisiklet ve otomobil, yürüme ve toplu taşımaya göre kent
  merkezindeki eşitliği iyileştiriyor.
- **Sınırlılık:** Yazarlar üç sınırlılık yazıyor. Birincisi, veri toplama zorluğu yüzünden farklı
  özellikteki nüfus gruplarının (yaş, cinsiyet) erişim farkları hesaba katılmamış. İkincisi, günün
  farklı saatlerindeki trafik yoğunluğunun erişime etkisi tartışılmamış. Üçüncüsü, çalışma yalnızca
  6. Çevre Yolu içiyle sınırlı, daha uzak banliyölere genellenip genellenemeyeceği belirsiz.
- **Projeme katkısı:** Erişimi ilçe benzeri alt bölgeler düzeyinde karşılaştırıyor ve eşitsizliği
  Gini ile ölçüyor, yani yöntem olarak benim yapmak istediğim şeye yakın. Ayrıca "nüfus yoğunluğu
  ile erişim arasındaki uyumsuzluk" diye kurdukları soru, benim problem cümlemin başka bir
  anlatımı. Merkez-çeper farkı bulmaları benim bulgumla aynı yönde.

---

## 6. Alp (2022)

İstanbul'da Raylı Sistem Yatırımlarının Kentin Gelişimi ve Arazi Kullanımı Üzerindeki Etkileri:
Arnavutköy İlçesi Örneği. Yüksek lisans tezi, İstanbul Sabahattin Zaim Üniversitesi, Kent
Çalışmaları ve Yönetimi. Danışman: Dr. Öğr. Üyesi Şahika Özdemir. 106 sayfa.

- **Problem:** Raylı sistem yatırımları kentlerin kırsal kesimlerini fiziksel, ekonomik ve sosyal
  olarak dönüştürüyor. Arnavutköy'e ilk kez raylı sistem geliyor ve bu yatırımın ilçedeki arazi
  kullanımına, nüfusa ve arazi değerlerine etkisi bilinmiyor.
- **Veri:** Arnavutköy ilçesinin planlama belgeleri, ulaşım sistemi bilgileri, nüfus verileri ve
  yapım aşamasındaki Halkalı-İstanbul Havalimanı raylı sistem hattının proje bilgileri. Ayrıca
  istasyon çevrelerindeki mevcut mekânsal kullanımlar incelenmiş.
- **Yöntem:** Nitel ağırlıklı durum incelemesi. Literatür taraması, belge incelemesi ve istasyon
  çevrelerinin yer seçimi ölçütleri üzerinden değerlendirilmesi. İstatistiksel bir test yok.
- **Temel bulgu:** Ulaşım yatırımlarıyla arazi kullanımı ve gayrimenkul değerleri arasında güçlü
  bir bağ var. Hattın tamamlanması hâlinde istasyon çevrelerinde ticaret ve hizmet sektörünün
  gelişeceği, kentsel büyümenin hat güzergâhına paralel ilerleyeceği değerlendiriliyor.
- **Sınırlılık:** Tek ilçeyle ve henüz açılmamış bir hatla sınırlı. Etkiler gerçekleşmiş değil,
  beklenen etkiler olarak değerlendiriliyor. Sayısal bir ölçüm ve karşılaştırma yok.
- **Projeme katkısı:** Benim çalışmamın tam tersi bir yaklaşım: ben 39 ilçeye yüzeysel bakıyorum, bu
  tez tek ilçeye derinlemesine bakıyor. İkisinin birbirini tamamladığını tartışma bölümünde
  yazabilirim. Ayrıca Arnavutköy benim tablomda 6 istasyonla orta sıralarda; bu tez o istasyonların
  neden ve ne zaman geldiğini açıklıyor.
