# Şarap Kalitesi Tahmin Projesi

## İçindekiler
1. [Proje Hakkında](#proje-hakkında)
2. [Kurulum ve Çalıştırma](#kurulum-ve-çalıştırma)
3. [Veri Seti](#veri-seti)
4. [Kullanılan Yöntemler](#kullanılan-yöntemler)
5. [Veri Analizi ve İşleme](#veri-analizi-ve-işleme)
   - [Eksik Değerler](#eksik-değerler)
   - [Hedef Değişkenin Dağılımı](#hedef-değişkenin-dağılımı)
   - [Korelasyon Analizi](#korelasyon-analizi)
6. [Model Eğitimi ve Değerlendirme](#model-eğitimi-ve-değerlendirme)
   - [Aykırı Değer Temizliği](#aykırı-değer-temizliği)
   - [Eğitim ve Test Verisi](#eğitim-ve-test-verisi)
   - [Model Seçimi](#model-seçimi)
   - [Performans Değerlendirme](#performans-değerlendirme)
   - [ROC Eğrisi](#roc-eğrisi)
7. [Sonuçlar](#sonuçlar)
8. [Video Açıklama](#video-açıklama)
9. [Grafikler ve Görseller](#grafikler-ve-görseller)

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

## Kullanılan Yöntemler

Bu projede, üç farklı makine öğrenimi algoritması kullanılmıştır:

1. **Lojistik Regresyon:** Basit ve hızlı bir modeldir. Ancak, karmaşık verilere çok iyi uyum sağlamayabilir.
2. **Karar Ağaçları:** Veriyi sınıflandırmak için ağaç yapısını kullanır, ancak aşırı uyum riski vardır.
3. **Rastgele Orman:** Karar ağaçlarının birleşiminden oluşan bir ansamble yöntemidir ve genellikle daha iyi performans gösterir.

---
# Veri Analizi ve İşleme

## Eksik Değerler

Eksik değerler kontrol edilmiştir ve veride herhangi bir eksik değer bulunmamaktadır.

```python
missing_values = data.isnull().sum()
print("\nEksik Değerler:")
print(missing_values)
```

## Hedef Değişkenin Dağılımı

Hedef değişken **quality**'nin dağılımını görselleştirerek, sınıfların dengeli olup olmadığını kontrol ettik.

```python
plt.figure(figsize=(8, 5))
sns.countplot(data=data, x="quality", hue="quality", legend=False, palette="viridis")
plt.title("Hedef Değişkeni Dağılımı: Kalite")
plt.xlabel("Kalite")
plt.ylabel("Sayım")
# Çubukların üzerine değerleri yazdır
for i in plt.gca().containers:
    plt.gca().bar_label(i, padding=2)
plt.tight_layout()
plt.show()
```

## Korelasyon Analizi

Veri setindeki özellikler arasındaki korelasyonları analiz ettik ve ısı haritası ile görselleştirdik.

```python
plt.figure(figsize=(12, 8))
data_corr = data.corr()
sns.heatmap(data_corr, annot=True, fmt=".2f", cmap="coolwarm")
plt.title("Korelasyon Isı Haritası")
plt.show()
```
---
# Model Eğitimi ve Değerlendirme

## Aykırı Değer Temizliği

Veri setindeki aykırı değerler, IQR (Çeyrekler Arası Aralık) yöntemi ile temizlendi.

```python
Q1 = data.quantile(0.25)
Q3 = data.quantile(0.75)
IQR = Q3 - Q1
alt_sinir = Q1 - 1.5 * IQR
ust_sinir = Q3 + 1.5 * IQR
cleaned_data = data[~((data < alt_sinir) | (data > ust_sinir)).any(axis=1)]
```

## Eğitim ve Test Verisi

Veriyi eğitim ve test setlerine böldük.

```python
X = cleaned_data.drop('quality', axis=1)
y = cleaned_data['quality']
X_train, X_test, y_train, y_test = train_test_split(X_scaled, y, test_size=0.2, random_state=42)
```

## Model Seçimi

3 farklı model kullanıldı: Lojistik Regresyon, Karar Ağaçları ve Rastgele Orman.

```python
log_model = LogisticRegression(random_state=42)
log_model.fit(X_train, y_train)
y_pred_log = log_model.predict(X_test)
```

## Performans Değerlendirme

Her modelin performansı, karışıklık matrisi ve sınıflandırma raporu ile değerlendirildi.

```python
def evaluate_model(y_test, y_pred, model_name):
    print(f"\nModel: {model_name}")
    cm = confusion_matrix(y_test, y_pred)
    sns.heatmap(cm, annot=True, fmt="d", cmap="Blues")
    plt.title(f"Karışıklık Matrisi: {model_name}")
    plt.xlabel("Tahmin Edilen")
    plt.ylabel("Gerçek")
    plt.show()
    
    print("\nSınıflandırma Raporu:")
    print(classification_report(y_test, y_pred))

evaluate_model(y_test, y_pred_log, "Lojistik Regresyon")
```

## ROC Eğrisi

Farklı modellerin performansları, ROC eğrisinde karşılaştırıldı.

```python
plt.figure(figsize=(10, 7))
for model, pred, name in zip([log_model, tree_model, rf_model], [y_pred_log, y_pred_tree, y_pred_rf], ["Lojistik Regresyon", "Karar Ağaçları", "Rastgele Orman"]):
    fpr, tpr, _ = roc_curve(y_test, model.predict_proba(X_test)[:, 1])
    plt.plot(fpr, tpr, label=f"{name} (AUC = {roc_auc_score(y_test, model.predict_proba(X_test)[:, 1]):.2f})")
plt.plot([0, 1], [0, 1], linestyle='--', color='gray')
plt.title("ROC Eğrisi")
plt.xlabel("Yanlış Pozitif Oranı")
plt.ylabel("Doğru Pozitif Oranı")
plt.legend()
plt.show()
```
---
## Sonuçlar

Üç modelin performans karşılaştırması sonucunda:

* **Lojistik Regresyon:** Basit ve hızlı ancak karmaşık verilere uyum sağlamakta zorluk çekebilir. (AUC = 0.79)
* **Karar Ağaçları:** Overfitting riski bulunuyor, ancak doğru parametre ayarları ile daha iyi sonuçlar elde edilebilir. (AUC = 0.77)
* **Rastgele Orman:** En yüksek genel performansı ve genelleme yeteneğini gösterdi. (AUC = 0.91)

