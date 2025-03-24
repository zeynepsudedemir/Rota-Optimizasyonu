# Rota Optimizasyonu
Bu proje, Ankara'daki belirli metro hatları ve durakları arasında en az aktarma ile en kısa sürede ulaşımı sağlamak için rotayı ve süreyi bulmayı amaçlayan bir algoritma tabanlı uygulamadır. Kullanıcılar, başlangıç ve varış noktalarını belirleyerek en uygun güzergahı görebilirler.

## 📌Kullanılan Teknolojiler ve Kütüphaneler
- **Python 3+:** Proje, Python programlama dili ile geliştirilmiştir.

- **heapq:** A* algoritması için öncelikli kuyruk yönetimi sağlamak amacıyla kullanılmıştır.

- **collections.deque:** BFS algoritmasında kuyruk yapısını kullanarak işlemleri hızlı bir şekilde gerçekleştirmek için tercih edilmiştir.
- 
## Algoritmaların Çalışma Mantığı
- **BFS Algoritması:** En az aktarma yapılan rotayı bulmak için kullanılmıştır. BFS, bir grafı katman katman tarayarak en kısa düğüm sayısına sahip yolu belirler.
- İlk olarak, ilk istasyon kuyruğa eklenir
- İstasyon komşuları ziyaret edilir
- Hedefe ulaşırsa yol tamamlanmış olur ve en uygun rota çizilir
- **A* Algoritması:**En kısa süreli güzergahı bulmak için kullanılmıştır. Bu algoritma, Dijkstra ve Best-First Search (En İyi Öncelikli Arama) yaklaşımlarını birleştirerek çalışır.
- Bir değerlendirme fonksiyonu ile her düğümün toplam maliyeti hesaplanır.
- En düşük maliyetli düğüm önce işleme alınır.
- Hedefe en kısa sürede ulaşan yol bulunur.
- **Neden Bu Algoritmalar Kullanıldı?**
- BFS, düğüm sayısını minimize ederek en az aktarma yapılan güzergahı bulmada etkilidir.
- A*, yolculuk süresini optimize etmek için en iyi seçenektir.





