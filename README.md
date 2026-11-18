Şimdiye kadar, düşük değerlendirme puanlarını en çok açıklayan faktörün `wait_time` olduğunu gördük; ancak kötü yorumların içeriklerini incelemek, bazı olumsuz değerlendirmelerin satıcıların kendileriyle ilişkili olduğunu da gösterdi.

💡 Sürekli kötü yorum alan ve pazar içinden çıkarılması gereken satıcıları sayısal olarak belirleyebiliriz; bu sayede kâr marjını artırmayı hedefleyebiliriz.

Aşağıdaki not defterini (`sellers.ipynb`) açın:
- Her satıcı hakkında mümkün olan tüm bilgilerle, her satırın bir satıcıya karşılık geldiği temiz bir eğitim seti oluşturacağız.
- Ardından, hangi satıcıların diğerlerine göre tekrarlı olarak düşük performans gösterdiğini analiz edip nedenlerini anlamaya çalışacağız.
- Son olarak, Olist platformunda kaliteli tedariki artırmak için kullanabileceğimiz ilk hipotezleri ve kalıpları oluşturacağız.

## Çalışma Notları

Bu proje, Olist verisinde her satırı bir satıcı olan bir veri seti kurar, her satıcı için puan, teslimat ve problemli sipariş metriklerini hesaplar ve platform ortalamasından istatistiksel olarak kötü performans gösteren satıcıları gruplar. Şablon yönerge notebook'u yerine kendi notebook'um (`Sellers-Analysis.ipynb`) kullanıldı. Metrikler önceki ünitedeki `olist` paketi yerine doğrudan notebook içinde hesaplandı.

1. Ortam: `workintech` sanal ortamı. Proje klasöründe `pyenv local workintech` ile etkinleştirilir. `statsmodels` ve `seaborn` yoksa `pip install statsmodels seaborn` ile kurulur.
2. Olist veri setinin 4 CSV dosyasını (`olist_orders`, `olist_order_items`, `olist_order_reviews`, `olist_sellers`) `data/` klasörüne koy. CSV dosyaları `.gitignore` içindedir, repoda yoktur.
3. `jupyter notebook` ile notebook'u aç ve hücreleri sırayla çalıştır. Tüm notebook birkaç saniyede çalışır.

Özet: Satıcı tablosu 2967 satır, medyan puan 4.21 (şablon testinin beklediği değerler). Satıcı puanını en çok `wait_time` açıklıyor (R² = 0.19), satıcının büyüklüğü ve platformdaki süresi anlamlı değil, eyaletin `wait_time` dışında anlamlı bir etkisi bulunmadı. Binom testi ve FDR düzeltmesiyle 42 satıcı platform ortalamasından anlamlı derecede fazla 1-2 yıldız alıyor. Bunlardan 14'ü teslimat süreleriyle açıklanamayacak kadar kötü yorum alıyor (kaldırma/inceleme adayı, satışların %2.2'si), 40 satıcının sorunu ise ağırlıklı olarak lojistik. Kötü yorumların %80'i normal satıcılardan geldiği için satıcı kaldırmak sınırlı etkili, asıl kaldıraç teslimat süresi. Ayrıntılar ve sınırlılıklar notebook'un sonuç bölümünde.
