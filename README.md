# Müşteri Segmentasyonu ve Tahmin Modeli

Bu proje, bir müşteri veri setini analiz ederek müşteri davranışlarını anlamayı ve bu davranışlara göre müşterileri belirli segmentlere ayırmayı amaçlamaktadır. Proje kapsamında, `loyal`, `budget` ve `impulsive` olmak üzere üç farklı müşteri segmenti için bir sınıflandırma modeli geliştirilmiştir.

![Python](https://img.shields.io/badge/Python-3.9-3776AB.svg?style=flat&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=flat&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-006699.svg?style=flat&logo=xgboost&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)

##  Projenin Amacı

Projenin temel amacı, demografik bilgiler, web/uygulama kullanım alışkanlıkları ve satın alma geçmişi gibi verileri kullanarak müşterileri doğru bir şekilde segmentlere ayırabilen yüksek performanslı bir makine öğrenmesi modeli oluşturmaktır. Bu segmentasyon, pazarlama stratejilerinin kişiselleştirilmesi, müşteri memnuniyetinin artırılması ve kaynakların daha verimli kullanılması için kritik öneme sahiptir.

## Proje Yapısı

```
.
├── Customer_Segments.ipynb    # Veri analizi, modelleme ve değerlendirme adımlarını içeren ana Jupyter Notebook
├── customer__full.csv         # Tüm veriyi içeren ana CSV dosyası
├── customer_train.csv         # Modelin eğitimi için kullanılan veri seti
├── customer_test.csv          # Modelin performansını test etmek için kullanılan veri seti
├── environment.yml            # Proje için gerekli Python kütüphanelerini içeren Conda ortam dosyası
└── README.md                  # Bu dosya
```

## Kullanılan Teknolojiler

Proje, aşağıdaki kütüphaneler ve teknolojiler kullanılarak geliştirilmiştir:

- **Veri Analizi ve İşleme:** Pandas, NumPy
- **Veri Görselleştirme:** Matplotlib, Seaborn
- **Makine Öğrenmesi:** Scikit-learn, XGBoost
- **Dengesiz Veri Yönetimi:** Imbalanced-learn (SMOTE tekniği için)

##  Kurulum ve Çalıştırma

Projeyi yerel makinenizde çalıştırmak için aşağıdaki adımları izleyebilirsiniz.

1.  **Projeyi Klonlayın:**
    ```bash
    git clone [https://github.com/kullanici_adiniz/proje_adiniz.git](https://github.com/kullanici_adiniz/proje_adiniz.git)
    cd proje_adiniz
    ```

2.  **Conda Ortamını Oluşturun:**
    Proje için gerekli tüm kütüphaneler `environment.yml` dosyasında belirtilmiştir. Aşağıdaki komut ile Conda ortamını oluşturup aktive edebilirsiniz.
    ```bash
    conda env create -f environment.yml
    conda activate CustomerEnv
    ```

3.  **Jupyter Notebook'u Başlatın:**
    Gerekli ortamı aktive ettikten sonra, Jupyter Notebook'u başlatarak `Customer_Segments.ipynb` dosyasını açabilirsiniz.
    ```bash
    jupyter notebook
    ```

## Metodoloji

Proje aşağıdaki adımlardan oluşmaktadır:

1.  **Veri Keşfi ve Ön İşleme:**
    - Veri setleri yüklendi ve birleştirildi.
    - Eksik değerler (`NaN`) stratejik olarak dolduruldu.
    - Kategorik değişkenler (ör. `country`, `device_os`) sayısal formata dönüştürüldü (One-Hot Encoding).

2.  **Özellik Mühendisliği:**
    - Müşteri etkileşimini daha iyi temsil eden yeni özellikler (`engagement_score`, `channel_ratio` vb.) oluşturuldu.

3.  **Dengesiz Veri Yönetimi:**
    - Eğitim veri setindeki segmentler arası dengesizliği gidermek için **SMOTE** (Synthetic Minority Over-sampling Technique) tekniği uygulandı. Bu, özellikle azınlık sınıfı olan `impulsive` segmentinin model tarafından daha iyi öğrenilmesini sağladı.

4.  **Modelleme:**
    - Müşteri segmentlerini tahmin etmek için **Optimize Edilmiş bir XGBoost (Extreme Gradient Boosting)** modeli geliştirildi. Model, yüksek doğruluğu ve performansı nedeniyle tercih edildi.

5.  **Model Değerlendirme:**
    - Modelin performansı; doğruluk (accuracy), F1 skoru, ve karmaşıklık matrisi (confusion matrix) gibi metrikler kullanılarak test verisi üzerinde değerlendirildi.

## Sonuçlar

Geliştirilen Optimize Edilmiş XGBoost modeli, test veri seti üzerinde **%97.38'lik genel doğruluk** oranına ulaşmıştır.

- **Karmaşıklık Matrisi Analizi:**
  - Model, en kalabalık sınıf olan **`budget`** segmentini %99 gibi çok yüksek bir başarı oranıyla tahmin etmiştir.
  - **`loyal`** segmenti için de %71'lik bir geri çağırma (recall) ve %88'lik bir kesinlik (precision) oranı elde edilmiştir.
  - Veri setindeki aşırı dengesizlik nedeniyle en zorlayıcı sınıf olan **`impulsive`** segmentinde ise model, mevcut örneklerin yarısını doğru tahmin edebilmiştir.

## Sonuç ve Gelecek Çalışmalar

Bu proje, müşteri verilerini kullanarak başarılı bir segmentasyon modelinin nasıl oluşturulabileceğini göstermektedir. SMOTE tekniğinin kullanılması, modelin azınlık sınıflarını öğrenme kapasitesini artırmada kritik bir rol oynamıştır.

**Öneri:** Gelecekte `impulsive` gibi az veriye sahip segmentlerin tahmin performansını daha da iyileştirmek için;
- Bu segmente ait daha fazla veri toplanması,
- Daha gelişmiş "few-shot learning" (az örnekle öğrenme) tekniklerinin araştırılması faydalı olacaktır.
