# Rota Optimizasyonu
Bu proje, Ankara'daki belirli metro hatları ve durakları arasında en az aktarma ile en kısa sürede ulaşımı sağlamak için rotayı ve süreyi bulmayı amaçlayan bir algoritma tabanlı uygulamadır. Kullanıcılar, başlangıç ve varış noktalarını belirleyerek en uygun güzergahı görebilirler.

## 📌Kullanılan Teknolojiler ve Kütüphaneler
- **Python 3+:** Proje, Python programlama dili ile geliştirilmiştir.

- **heapq:** A* algoritması için öncelikli kuyruk yönetimi sağlamak amacıyla kullanılmıştır.

- **collections.deque:** BFS algoritmasında kuyruk yapısını kullanarak işlemleri hızlı bir şekilde gerçekleştirmek için tercih edilmiştir.
  
## Algoritmaların Çalışma Mantığı

Bu projede, bir metro ağı modellemesi ve iki farklı rota bulma algoritması (en az aktarma ve en hızlı rota) kullanılarak, bir şehirdeki metro hatları ve istasyonları arasındaki bağlantılar hesaplanıyor. Şimdi, kullanılan algoritmaların çalışma mantığını ve işleyişini daha ayrıntılı şekilde açıklayacağım.

### 1. **İstasyonlar ve Bağlantılar**
İlk olarak, metro istasyonları ve hatları tanımlanır. Her istasyon bir Istasyon sınıfı ile modellenir. Her istasyon:

-idx: İstasyonun benzersiz kimliği

-ad: İstasyonun adı

-hat: İstasyonun ait olduğu metro hattı

-komsular: İstasyonun bağlı olduğu komşu istasyonlar ve bu bağlantının süresi

İstasyonlar, MetroAgi sınıfı altında birleştirilir.Bu sınıf, tüm istasyonları ve her hattın istasyonlarını tutan iki ana veri yapısını içerir.
Her iki istasyon arasındaki bağlantılar da baglanti_ekle fonksiyonu ile eklenir.


### 2. **BFS Algoritması: En Az Aktarma Algoritması**
  En az aktarma yapılan rotayı bulmak için kullanılmıştır. BFS, bir grafı katman katman tarayarak en kısa düğüm sayısına sahip yolu belirler.

- **İşleyişi:**
  - İlk olarak, başlangıç istasyonu kuyruğa eklenir.
  - İstasyon komşuları ziyaret edilir.
  - Eğer hedef istasyon bulunursa, yol tamamlanmış olur ve en uygun rota çizilir.

### 3. **A-Star Algoritması: En Hızlı Rota Algoritması**
  En kısa süreli güzergahı bulmak için kullanılmıştır. Bu algoritma, Dijkstra ve Best-First Search (En İyi Öncelikli Arama) yaklaşımlarını birleştirerek çalışır.

- **İşleyişi:**
  - Her düğüm için bir değerlendirme fonksiyonu ile toplam maliyet hesaplanır.
  - En düşük maliyetli düğüm önce işleme alınır.
  - Hedefe en kısa sürede ulaşan yol bulunur.
### 4. **Neden Bu Algoritmalar Kullanıldı?**
- **BFS**, düğüm sayısını minimize ederek en az aktarma yapılan güzergahı bulmada etkilidir. BFS, başlangıç noktasından hedef noktaya giderken, her bir istasyonun komşularını sırayla ziyaret eder. Bu sayede, en kısa düğüm sayısına sahip (en az aktarmalı) rotayı bulur.
- **A***, yolculuk süresini optimize etmek için en iyi seçenektir.Bu algoritma ile aha hızlı ve verimli sonuçlar sağladık.

## 4. **Örnek Kullanım ve Test Sonuçları**
 **1.Örnek:AŞTİ'den OSB'ye:**
 - ```python
   rota = metro.en_az_aktarma_bul("M1", "K4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("M1", "K4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
- **1.Örnek Cevabı:**
 - ```python
   1. AŞTİ'den OSB'ye:
   En az aktarmalı rota: AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB
   En hızlı rota (25 dakika): AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB
 **2.Örnek:Batıkent'ten Keçiören'e:**
 - ```python
   print("\n2. Batıkent'ten Keçiören'e:")
    rota = metro.en_az_aktarma_bul("T1", "T4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("T1", "T4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
- **2.Örnek Cevabı:**
 - ```python
   2. Batıkent'ten Keçiören'e:
   En az aktarmalı rota: Batıkent -> Demetevler -> Gar -> Keçiören
   En hızlı rota (21 dakika): Batıkent -> Demetevler -> Gar -> Keçiören
**3.Örnek: Keçiören'den AŞTİ'ye:**
 - ```python
   rota = metro.en_az_aktarma_bul("T4", "M1")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("T4", "M1")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
- **3.Örnek Cevabı:**
 - ```python
   3. Keçiören'den AŞTİ'ye:
   En az aktarmalı rota: Keçiören -> Gar -> Gar -> Sıhhiye -> Kızılay -> AŞTİ
   En hızlı rota (19 dakika): Keçiören -> Gar -> Gar -> Sıhhiye -> Kızılay -> AŞTİ
  
  
  


## 5. **Projeyi Geliştirme Fikirleri**
- Görsel Arayüz: Komut satırı yerine, kullanıcıların rota arayabileceği bir kullanıcı arayüzü eklenebilir.
- Gerçek Zamanlı Veri: Metro ağına ait duraklar ve tren bilgileri gerçek zamanlı verilerle entegre edilebilir. Böylece gecikme gibi problemlerde kullanıcıya farklı kombinasyonlar sunulabilir.
- Yapay Zeka Optimizasyonu: Makine öğrenimi kullanarak, kullanıcı tercihlerine göre en uygun rotalar önerilebilir.
- Mobil Uygulama: Proje, mobil platformlar için geliştirilerek kullanıcının rahatlıkla günlük yaşamda kullanabileceği bir proje olur.




