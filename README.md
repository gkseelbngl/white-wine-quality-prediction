# Şarap Kalitesi Tahmin Projesi

## İçindekiler
1. [Proje Hakkında](#proje-hakkında)
2. [Kurulum ve Çalıştırma](#kurulum-ve-çalıştırma)
3. [Veri Seti](#veri-seti)
4. [Veri Analizi ve İşleme](#veri-analizi-ve-işleme)
   - [Eksik Değerler](#eksik-değerler)
   - [Hedef Değişkenin Dağılımı](#hedef-değişkenin-dağılımı)
   - [Korelasyon Analizi](#korelasyon-analizi)
5. [Model Eğitimi ve Değerlendirme](#model-eğitimi-ve-değerlendirme)
   - [Aykırı Değer Temizliği](#aykırı-değer-temizliği)
   - [Eğitim ve Test Verisi](#eğitim-ve-test-verisi)
   - [Model Seçimi](#model-seçimi)
   - [Performans Değerlendirme](#performans-değerlendirme)
6. [Sonuçlar](#sonuçlar)
7. [Video Açıklama](#video-açıklama)
8. [Grafikler ve Görseller](#grafikler-ve-görseller)
9. [Gereksinimler](#gereksinimler)

## Proje Hakkında

Bu proje, beyaz şarapların kimyasal özelliklerini kullanarak kalitelerini analiz eder ve tahmin eder. Veri seti, beyaz şarapların çeşitli kimyasal özelliklerini ve kalite puanlarını içermektedir.

## Kurulum ve Çalıştırma

Projeyi yerel makinenizde çalıştırmak için aşağıdaki adımları izleyin:

```bash
# Projeyi klonlayın
git clone https://github.com/gkseelbngl/white-wine-quality-prediction

# Proje dizinine gidin
cd white-wine-quality-prediction

# Gerekli kütüphaneleri yükleyin
pip install pandas numpy matplotlib seaborn scikit-learn
```
Jupyter Notebook'u çalıştırma:

```bash
jupyter notebook winedataset.ipynb
```
Tüm hücreleri çalıştırma:

```bash
# Jupyter Notebook içinde
Kernel > Restart & Run All
```


## Veri Seti

Veri seti, **winequality-white.csv** dosyasından alınmıştır. Veri seti, beyaz şarapların çeşitli kimyasal özelliklerini (alkol oranı, asidite, pH değeri vb.) içermekte ve her şarap için bir kalite puanı (0-10 arası) ile etiketlenmiştir. *(Örnek Sayısı: 4898)*

**Özellikler:**

* **fixed acidity:** Sabit asidite
* **volatile acidity:** Uçucu asidite
* **citric acid:** Sitrik asit
* **residual sugar:** Kalan şeker
* **chlorides:** Klorür
* **free sulfur dioxide:** Serbest sülfür dioksit
* **total sulfur dioxide:** Toplam sülfür dioksit
* **density:** Yoğunluk
* **pH:** pH değeri
* **sulphates:** Sülfatlar
* **alcohol:** Alkol oranı
* **quality:** Kalite (1-10 arası)
