# Şarap Kalitesi Tahmin Projesi

## İçindekiler
1. [Proje Hakkında](#proje-hakkında)
2. [Başlarken](#başlarken)
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
10. [Kurulum ve Çalıştırma](#kurulum-ve-çalıştırma)

## Proje Hakkında

Bu proje, beyaz şarapların kimyasal özelliklerini kullanarak kalitelerini analiz eder ve tahmin eder. Veri seti, beyaz şarapların çeşitli kimyasal özelliklerini ve kalite puanlarını içermektedir.

## Başlarken

Projeyi yerel makinenizde çalıştırmak için aşağıdaki adımları izleyin:

```bash
# Projeyi klonlayın
git clone https://github.com/gkseelbngl/white-wine-quality-prediction

# Proje dizinine gidin
cd sarap-kalitesi-tahmini
```

## Veri Seti

Veri Seti: Beyaz Şarap Kalitesi Veri Seti
Örnek Sayısı: 4898
Özellik Sayısı: 11
Hedef Değişken: Kalite (0-10 arası)
